+++
title = "Formatting is Unreasonably Expensive for Embedded Rust"
date = 2019-12-08
draft = false
in_search_index = true
template = "blog_post.html"
+++

As a (late) part of the [#rust2020] request, I wanted to talk about one of the paper-cuts that has become decently problematic for new and experienced users of Embedded Rust:

The size costs of formatting in Rust today are unreasonably expensive for users of Rust on bare metal embedded systems.

In particular there are two root issues I can see:

1. Out of the box formatting machinery, including `format!()`, `write!()`, and `panic!()` in Rust is not program space efficient
2. More problematically, there is no way to change or opt-out of this cost, and it can show up in unexpected places that are outside of developer control

**To be clear:** I *don't* think that these issues are a failing of the language, but rather a sign of growth. The current formatting solution has managed to work without issue for most people (and is still okay-ish in edge cases like embedded) for the better part of 4 years. However as we push Rust to more use cases, the language will need to adapt if it would like to fill into these spaces.

This post aims to illuminate the challenges faced today, and attempt to draw an attainable set of paths moving forward.

[#rust2020]: https://twitter.com/hashtag/rust2020

<!-- more -->

## The Situation

As of December 2019, the machinery in the Rust language for formatting is generally optimized for three things:

1. User flexibility and convenience (to format whatever and however, with as little effort as possible)
2. Compile time complexity (don't blow up build times)
3. Run time speed (printing shouldn't be slow)

This design trade off works well for most users: It allows for maximum flexibility and dynamic-ish behavior for users at the cost of slightly larger (in the order of 10s-100s of KiB) and more complex (trait objects, recursion) generated code.

However for embedded users, size is a primary concern. Often we only have 32-128KiB for all code, as well as 16-64KiB of RAM (or less).

There is currently no way to disable, configure, or replace the provided formatting machinery, or to customize it in any way. Formatting (through panics) can be invoked in unexpected places, and can be difficult to remove consistently.

### A quick disclaimer

I have not been able to find a good written overview of how the formatting machinery currently works, or what conversations were had about its design.

My understanding of how it works and the design trade offs that were made is largely informed by previous informal conversations with `rustc` contributors. If you know of a good written reference, please [let me know](https://twitter.com/bitshiftmask/status/1203750321572470784)!

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">It’s dark and ancient magic. I don’t think anyone knows it very well, never mind documentation</p>&mdash; nrc (@nick_r_cameron) <a href="https://twitter.com/nick_r_cameron/status/1203753952329650176?ref_src=twsrc%5Etfw">December 8, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## Examples

All examples provided below are sourced from [this repository]. On each commit, there is is a file called `size.txt`, which contains the output of `arm-none-eabi-size` demonstrating the total size of the code, as well as [`cargo bloat`], which generally shows the Rust components that make up the total size.

[this repository]: https://github.com/jamesmunns/tiny-nrf52/
[`cargo bloat`]: https://github.com/RazrFalcon/cargo-bloat

This project is based on the Nordic nRF52, an Arm Cortex-M based micro-controller. All examples have been compiled with `opt-level = 's'`, though the `core`/`std` library was not recompiled from source, so those components will be at `opt-level = 3`. Additionally, the following settings were made to the `release` profile:

```toml
[profile.release]
lto             = true
panic           = "abort"
debug           = true
incremental     = false
codegen-units   = 1
opt-level       = 's'
```

### Baseline

For our baseline, we use a fairly regular minimal embedded Rust example. This firmware image will periodically blink an LED and output text to a serial port, and it uses the [`panic-persist`] crate, which stores panic messages to RAM and reboots the device in the case of a panic.

[`panic-persist`]: https://crates.io/crates/panic-persist

Here is the reference firmware `main.rs`:

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

        // Delay 1 second (in microseconds)
        timer.delay(1_000_000);
    }
}
```

Unfortunately, this generates a 14.2KiB binary, which isn't prohibitively large, but somewhat unreasonable for the limited functionality demonstrated.

```text
   text    data     bss     dec     hex filename
  14512       0       4   14516    38b4 tiny-nrf52

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

As an initial comparison, we can use a panic provider crate that **doesn't** use the panic output message at all, and hope that the optimizer is smart enough to discard any undesired panic formatting entirely. In this case, we swap [`panic-persist`] for [`panic-reset`]:

[`panic-reset`]: https://crates.io/crates/panic-reset

```diff
 // Panic provider crate
-use panic_persist as _;
+use panic_reset as _;
```

You can see the full changes necessary in the [silent panic diff], but without changing the primary functionality of our code at all (we still blink a light, print text to the UART, and reboot on a panic condition), we see a huge difference:

```text
   text    data     bss     dec     hex filename
   1176       0       4    1180     49c tiny-nrf52

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

The output of `cargo-bloat` is now the **entirety** of our produced binary, weighing in at 1.2KiB, or a **92% reduction in size**.

[silent panic diff]: https://github.com/jamesmunns/tiny-nrf52/compare/04586a1..9af8686

Unfortunately this is a very "all or nothing" proposition, as we no longer have our panic messages available for debugging, and it still requires the optimizer to intelligently recognize that we never use any of the formatting machinery.

But what happened? We never explicitly print, we never explicitly format, so where does the size come from?

### Swallowing errors

The spoiler is that we call `.unwrap()` in two places in our example:

```rust
// Number 1: Unwrapping an Option<T>
let mut board = DWM1001::take().unwrap();

// Number 2: Unwrapping a Result<T, E>
board.uart.write(&buf).unwrap();
```

When you hit the error case of `unwrap` (either a `None` or an `Err(T)`), formatting code is used to display the `Debug` representation of the error case. Depending on the data returned, this can be pretty big.

Here, rather than entirely discarding the panics by switching to [`panic-reset`], we instead handle the errors by wrapping the functionality in main:

```rust
#[entry]
fn main() -> ! {
    let _ = inner_main();

    // We should never get here unless there is
    // an error condition
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

You can see the entirety of the changes in the [swallow error diff] which still uses the original `panic-persist` crate and has some formatting in use, but the savings are still significant:

[swallow error diff]: https://github.com/jamesmunns/tiny-nrf52/compare/04586a1..1e250d3

```text
   text    data     bss     dec     hex filename
   4708       0       4    4712    1268 tiny-nrf52

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

#### A quick interlude

In actuality, the majority of the 10KiB of code comes from unwrapping the error in sending data to the UART. To demonstrate how unpredictable the formatting code size really is, the following example shows what happens to the total code size when changing *just this one line*:

```rust
// A - nrf52_hal_common::uarte::Error
board.uart.write(&buf).unwrap();

// B - ()
board.uart.write(&buf).map_err(drop).unwrap();

// C - i32
board.uart.write(&buf).map_err(|_| 5).unwrap();

// D - &str
board.uart.write(&buf).map_err(|_| "argh").unwrap();

// E - None
board.uart.write(&buf).map_err(|e| <Option<()>>::None ).unwrap();
```

| Size  | Error Type |
| :---  | :--- |
| 14KiB | A - `nrf52_hal_common::uarte::Error` |
|  4KiB | B - `()` |
|  5KiB | C - `i32` |
| 10KiB | D - `&str` |
| 14KiB | E - `None` |

### Bring your own Context

In our last change, we won't get any additional information for errors that could occur, we're just returning an `Err(())`, and we always hit the same `panic!()` message in `main()`, which means we don't know what actually happened, just that there was an error.

We can add back our own context by using human readable error messages to get "just enough context" for our use case. First, we change `main()` to gracefully reboot if `inner_main()` returns `Ok(())`, and to panic with an error if `inner_main()` returns an `Err`:

```diff
 #[entry]
 fn main() -> ! {
-    let _ = inner_main();
-    panic!();
+    match inner_main() {
+        Ok(()) => cortex_m::peripheral::SCB::sys_reset(),
+        Err(e) => panic!(e),
+    }
 }
```

Then we change `inner_main()` to return `Result<(), &'static str>` instead of `Result<(), ()`:

```diff
-fn inner_main() -> Result<(), ()> {
+fn inner_main() -> Result<(), &'static str> {
```

And we change our error cases to return a little context:

```diff
-    let mut board = DWM1001::take().ok_or(())?;
+    let mut board = DWM1001::take().ok_or("Err getting board!")?;

-        board.uart.write(&buf).map_err(drop)?;
+        board.uart.write(&buf).map_err(|_| "Err writing hello!")?;
```

We even take advantage of [`panic-persist`]'s ability to retrieve panic messages from the previous boot:

```rust
if let Some(msg) = panic_persist::get_panic_message_bytes() {
    // write the error message in reasonable chunks
    for i in msg.chunks(255) {
        board
            .uart
            .write(i)
            .map_err(|_| "Err writing error!")?;
    }
}
```

With all of these changes, we've increased the binary size a bit, but still far smaller than our original code. We've even have the same ability to see where the errors occurred. See the [context diff] for all changes, but here's the new size numbers:

[context diff]: https://github.com/jamesmunns/tiny-nrf52/compare/1e250d3..5767c3b

```text
   text    data     bss     dec     hex filename
   4864       0       4    4868    1304 tiny-nrf52

===============

File  .text   Size         Crate Name
0.2%  19.9%   776B     [Unknown] main
0.2%  18.7%   728B           std core::fmt::Formatter::pad
0.2%  15.1%   588B           std core::fmt::num::imp::fmt_u32
0.1%  13.6%   530B           std core::fmt::write
0.1%   5.7%   224B panic_persist <&T as core::fmt::Display>::fmt
0.1%   5.3%   208B panic_persist <&mut W as core::fmt::Write>::write_char
0.0%   2.9%   112B   cortex_m_rt Reset
0.0%   2.7%   104B     [Unknown] __aeabi_memcpy
```

### Wrapping up our examples

We've now been able to bring our code to be roughly equivalent, with a reduction to around 1/3 of the original code size.

For a total summary of code sizes:

```text
   text    data     bss     dec     hex example
  =====    ====     ===   =====    ==== =======
   1176       0       4    1180     49c panic-persist
   4708       0       4    4712    1268 without context
   4864       0       4    4868    1304 with context
  14512       0       4   14516    38b4 original with unwrap
```

## Workarounds

There are a couple workarounds to these issues that are possible today, with various trade offs:

### Using `panic-halt` or `panic-reset`

A user could chose to use an existing panic crate that discards panic messages completely. This helps to handle cases where code size increases were caused by an errant `.unwrap()` or `panic!()`.

This reduces the code size greatly, with extremely minor code changes.

However, this doesn't help with normal formatting cases, and forces the user to do without panic messages of any kind. It also relies on the optimizer to eliminate these code paths, which is not necessarily guaranteed, especially without `codegen-units = 1`, `incremental = false`, and `lto = true` set.

### Manually avoiding formatting, unwraps, etc.

A user could carefully avoid the use of formatting and ensure that they don't use unwrap (as we have done here), however this puts a lot of manual review work on the end developer. Tools like [`panic-never`] can help automate the discovery of these problems, but not assist in fixing them.

[`panic-never`]: https://github.com/japaric/panic-never

Furthermore, `unwrap`s or `panic`s could exist in code provided by another crate, making it difficult to patch directly without waiting for a PR to land, or maintaining a fork of the project.

### Replacing the built-in format machinery

The user could chose to replace their usage of format machinery with libraries like [japaric]'s [`μfmt`], which implements a similar API to the built-in `Display`, `Debug`, `format!()` and `write!()` interfaces, but in a more efficient, if not limited fashion.

[japaric]: https://github.com/japaric
[`μfmt`]: https://github.com/japaric/ufmt

Unfortunately [`μfmt`] is not a drop-in replacement, and won't help with cases where an unexpected `panic` or `unwrap` is the source of code increase, as those still rely on the official `Debug` trait.

This option would combine well with the previous workarounds by avoiding an expensive `panic` while also addressing the needs to format code within a project.

## Long term Solutions

Let's look back at my two problem statements:

1. Out of the box formatting, including `format!()`, `write!()`, and `panic!()` in Rust is not program space efficient
2. More problematically, there is no way to change or opt-out of this cost, and it can show up in unexpected places that are outside of developer control

### Solution 1: Changing Panic

The largest issue in my opinion is that formatting through panic is impossible to completely opt-out of.

It could be imagined that there could be another interface for Panicking that could be opted-in to, one that doesn't invoke any usage of formatting while still giving some context.

The `panic_info_message` feature currently in nightly, [tracking issue here], has a couple of aspects that could make it easier to implement a `no_std` panic handler that doesn't require formatting using the default machinery, though it is still under discussion.

[tracking issue here]: https://github.com/rust-lang/rust/issues/66745

Note that this solution makes no attempt to address the default formatting machinery as it currently stands.

### Solution 2: Tweaking Format

A second option would be to provide two or more implementations of the formatting machinery in `libcore`/`libstd`, and allow the user to select which one is used at compile time. This could show up in the `Cargo.toml` of your application:

```toml
# Options are: 'smol', 'fast', and 'balanced'.
# Defaults to 'balanced'
format-machinery = "smol"
```

This would allow for multiple end-user options, while not being forced to stabilize any component of how formatting works under the hood. However this would require changes to the upstream standard library whenever a new optimization is needed.

This solution does not address the problem of unexpected panics introducing an unwanted formatting cost, but this may be acceptable if the formatting machinery is sufficiently compact.

### Solution 3: Replacing Format

Think "panic handler crates", but instead, "format handler crates". This one is a bit trickier, but in general, it would require:

* Stabilizing certain interfaces for formatting
* Stabilizing a way for crates to implement these interfaces
* Stabilizing a way for applications to select which of these crates to use

I have a feeling this is the best long term solution, however I would expect this solution to be relatively slow to implement for a few reasons:

1. Format handling is fairly "baked in" to the compiler itself
2. Stabilizing low level parts of the compilation process can take time to get right, as seen by the slow push for stable panics and global or local allocators.

## Summing it all up

In general - I think we need all three solutions, and some of the workaround(s). For now, making it easier to make lighter-weight panic handlers (like Solution #1) and using crates like [`μfmt`] can help reduce the cost in the short term, and we should document those patterns.

In the medium term (in 2020), I'd like to see Solution #2 happen, as a way to test out implementing a new formatting handler, but without being forced to stabilize a particular interface yet.

In the long term (2020 and beyond), I'd like to see Solution #3 happen, once we have learned from implementing Solution #2.
