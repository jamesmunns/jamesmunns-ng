+++
title = "Panic is Unreasonably Expensive for Embedded Rust"
date = 2019-12-08
draft = false
in_search_index = true
template = "blog_post.html"
+++

As a (late) part of the [#rust2020] request, I wanted to talk about one of the papercuts that has become decently problematic for new and experienced users of Embedded Rust:

The size costs of formatting, including `format!()`, `write!()`, `panic!()`, and even `unwrap()`, are unreasonably expensive for users of Rust on bare metal embedded systems.

[#rust2020]: https://twitter.com/hashtag/rust2020

<!-- more -->

## The Situation

> Disclaimer: I have not been able to find a good written overview of how the formatting machinery currently works. If you know of one, please [let me know](https://twitter.com/bitshiftmask/status/1203750321572470784)!

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">It’s dark and ancient magic. I don’t think anyone knows it very well, never mind documentation</p>&mdash; nrc (@nick_r_cameron) <a href="https://twitter.com/nick_r_cameron/status/1203753952329650176?ref_src=twsrc%5Etfw">December 8, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

As of December 2019, the machinery in the Rust language for formatting is generally optimized for two things:

1. User flexibility (to format whatever and however)
2. Compile time complexity (don't blow up build times)
3. Run time speed (printing should't be slow)

This design tradeoff works well for most users: It allows for maximum flexibility and dynamic-ish behavior for users at the cost of slightly larger (in the order of 10s-100s of KiB) or more complex (trait objects, recursion) generated code.

However for embedded users, size is a primary concern. Often we only have 32-128KiB for all code, as well as 16-64KiB of RAM (or less).

There is currently no way to disable, configure, or replace the provided formatting machinery, or to customize it in any way. Formatting can be invoked in unexpected places, and can be difficult to remove consistently.

## Examples

All examples provided below are based from [this repository]. On each commit, there is is a file called `size.txt`, which contains the output of `arm-none-eabi-size` demonstrating the total size of the code, as well as `cargo bloat`, which generally shows the Rust components that make up the total size.

[this repository](https://github.com/jamesmunns/tiny-nrf52/)

All examples have been compiled with `opt-level = "sz"`, though the `core`/`std` library was not recompiled from source, so those components will be at `opt-level = 3`.

### Baseline

For our baseline, we use a fairly "normal" embedded Rust example. This firmware image will periodically blink a light and output text to a serial port, and it uses the `panic-persist` crate, which stores panic messages to RAM and reboots the device in the case of a panic.

Here is the firmware in its entirety:

```rust
#![no_std]
#![no_main]

// Panic provider crate
use panic_persist as _;

// Used to set the program entry point
use cortex_m_rt::entry;

// Provides definitions for our development board
use dwm1001::{
    nrf52832_hal::prelude::*,
    DWM1001,
};

#[entry]
fn main() -> ! {
    let mut board = DWM1001::take().unwrap();
    let mut timer = board.TIMER0.constrain();
    let mut toggle = false;

    loop {
        // board.leds.D10 - Bottom LED BLUE
        if toggle {
            board.leds.D10.enable();
        } else {
            board.leds.D10.disable();
        }

        toggle = !toggle;

        // nRF52 requires data to be in RAM, not Flash
        const MSG: &[u8] = "Hello, world!\r\n".as_bytes();
        let mut buf = [0u8; MSG.len()];
        buf.copy_from_slice(MSG);

        board.uart.write(&buf).unwrap();

        timer.delay(1_000_000);
    }
}
```

Unfortunately, this generates a 14.2KiB binary, which isn't probitively large, but somewhat unreasonable for the limited functionality.

```text
   text    data     bss     dec     hex filename
  14512       0       4   14516    38b4 target/thumbv7em-none-eabihf/release/tiny-nrf52

===============

File  .text   Size            Crate Name
0.2%   9.7%   812B              std <char as core::fmt::Debug>::fmt
0.2%   9.4%   790B              std core::str::slice_error_fail
0.2%   8.7%   728B              std core::fmt::Formatter::pad
0.2%   7.6%   634B        [Unknown] main
0.1%   6.6%   550B              std core::fmt::Formatter::pad_integral
0.1%   6.3%   530B              std core::fmt::write
0.1%   5.9%   490B              std core::slice::memchr::memchr
0.1%   4.3%   360B nrf52_hal_common <nrf52_hal_common::uarte::Error as core::fmt::Debug...
0.1%   4.3%   360B              std core::fmt::num::<impl core::fmt::Debug for usize>::fmt
```

Here we see that our actual code (`main`) is only the 4th largest item in the binary at 634 bytes, and nearly every other item at the top of the list is a component of formatting, or a `Debug` trait implementation.

### `panic-reset`

As an initial comparison, we can use a panic provider crate that **doesn't** use the panic output message at all, and hope that the optimizer is smart enough to discard any undesired panic formatting entirely.

You can see the changes necessary in the [silent panic diff], but without changing the functionality of our code at all (we still blink a light and print text to the UART, and reboot on a panic condition), we see a huge difference:

```text
   text    data     bss     dec     hex filename
   1176       0       4    1180     49c target/thumbv7em-none-eabihf/release/tiny-nrf52

===============

File  .text Size       Crate Name
0.3%  72.5% 618B   [Unknown] main
0.1%  13.1% 112B cortex_m_rt Reset
0.0%   4.5%  38B    cortex_m cortex_m::peripheral::scb::<impl cortex_m::peripheral::SCB...
0.0%   0.7%   6B panic_reset rust_begin_unwind
0.0%   0.7%   6B cortex_m_rt ResetTrampoline
0.0%   0.7%   6B         std core::result::unwrap_failed
0.0%   0.7%   6B         std core::panicking::panic
0.0%   0.7%   6B         std core::panicking::panic_fmt
0.0%   0.7%   6B         std core::panicking::panic_bounds_check
0.0%   0.2%   2B cortex_m_rt HardFault_
0.0%   0.2%   2B cortex_m_rt DefaultPreInit
0.0%   0.2%   2B cortex_m_rt DefaultHandler_
```

The output of `cargo-bloat` is now the **entirety** of our produced binary, eighing in at 1.2KiB, or a 92% reduction in size.

[silent panic diff]: https://github.com/jamesmunns/tiny-nrf52/compare/04586a1..9af8686

Unfortunately this is a very "all or nothing" proposition, and it still requires the optimizer to intelligently recognize that we never use any of the formatting machinery.

But where did this come from? We never print, we never format, where does the size come from?

### Swallowing errors

The spoiler is that we call `.unwrap()` in two places in the code. When you hit the error case of `unwrap` (either a `None` or an `Err(T)`), formatting code is used to display the `Debug` representation of the error case. Depending on the data returned, this can be pretty big.

Here, rather than entirely discarding the panics by switching to `panic-reset`, we instead handle the errors by wrapping the functionality in main:

```rust
#[entry]
fn main() -> ! {
    let _ = inner_main();
    panic!();
}

fn inner_main() -> Result<(), ()> {
    // The old contents of main
}
```

Additionally we use `ok_or` and `map_err` to replace the error cases previously handled by `.unwrap()` to instead return an empty tuple:

```diff
-    let mut board = DWM1001::take().unwrap();
+    let mut board = DWM1001::take().ok_or(())?;

-        board.uart.write(&buf).unwrap();
+        board.uart.write(&buf).map_err(drop)?;
```

You can see the entirety of the changes in the [swallow error diff] which still uses `panic-persist` and has some formatting, but the savings are still significant:

[swallow error diff]: https://github.com/jamesmunns/tiny-nrf52/compare/04586a1..1e250d3

```text
   text    data     bss     dec     hex filename
   4708       0       4    4712    1268 target/thumbv7em-none-eabihf/release/tiny-nrf52

===============

File  .text   Size         Crate Name
0.2%  19.4%   728B           std core::fmt::Formatter::pad
0.2%  16.4%   616B    tiny_nrf52 tiny_nrf52::inner_main
0.2%  15.7%   588B           std core::fmt::num::imp::fmt_u32
0.1%  14.1%   530B           std core::fmt::write
0.1%   6.0%   224B panic_persist <&T as core::fmt::Display>::fmt
0.1%   5.5%   208B panic_persist <&mut W as core::fmt::Write>::write_char
0.0%   3.0%   112B   cortex_m_rt Reset
0.0%   2.8%   104B     [Unknown] __aeabi_memcpy
```

We were able to knock nearly 10KiB off of the binary size, just by replacing two `.unwrap()` statements!

## Workarounds

* `panic-halt`, `panic-reset`
    * Still relies on the optimizer
    * Loses all context for users or logging errors
* Manually avoiding formatting, unwraps, and complex panic statements
    * Doesn't help if it's in 3rd party code
    * use never-panic to check
* `ufmt`
    * Not a drop in replacement
    * Doesn't help with 3rd party code

## Long term Solutions

* Alternative panic implementations
* Configuration to formatting
* Replacable
