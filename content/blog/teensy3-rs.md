+++
title = "Easier Rust Development on the PJRC Teensy 3"
date = 2016-09-26
draft = false
# tags = ["tag1", "tag2"]
# category = "rust"
aliases = ["update/2016/09/26/teensy3-rs.html"]
in_search_index = true
template = "blog_post.html"
+++

I've written a bit about embedded devices, and a bit about Rust in the past, but I wanted to share something I've been working on (wtih the help of some really smart people) for the last few weeks. Today I was able to publish a crate called [teensy3](https://crates.io/crates/teensy3), which contains most of the boilerplate necessary to get started using Rust on the Cortex M4 based [PJRC Teensy 3.1 or 3.2](https://www.pjrc.com/teensy/index.html), as well as (unsafe) Rust binding for the **entire** Teensyduino API/HAL. Additionally, we have a demo repository containing [everything necessary](https://github.com/jamesmunns/teensy3-rs-demo/) to get started.

<!-- more -->

<img src="../images/rust.png" alt="Rustlang Logo">
<img src="../images/teensy32.jpg" alt="Teensy 3.2 Development Board">

There are a number of other far more advanced embedded efforts being pushed for a fully native experience for embedded Rust, such as [Zinc.rs](https://github.com/hackndev/zinc), [Tock](https://github.com/helena-project/tock), all of [Japaric's work](https://github.com/japaric/copper), and probably lots more that I haven't even found yet. However, until the embedded Rust ecosystem stabilizes, hopefully [coming soon](https://github.com/rust-lang/rfcs/pull/1645), there is a bit of a vacuum for "low barrier to entry" effort of trying Rust on a microcontroller. By providing bindings to the Arduino API/HAL, hopefully it will be possible to write semi-portable, and easily usable Rust application level code for platforms like the Teensy.

## How we got here

In the ramp up for [Rustfest Berlin 2016](http://www.rustfest.eu/), there were plans for an Embedded Focused workshop room, and I wanted to build on some Rust-on-the-Teensy tutorials that I found that had gotten a basic blinky-light going for the platform. Before the conference I met up with [@SimonSapin](https://twitter.com/SimonSapin), a member of the Servo team, who had already been working on porting an older C based project to Rust, using a Teensy. He had ran Servo's branch of [rust-bindgen](https://github.com/servo/rust-bindgen), which added support for C++, against the [Teensyduino libraries](https://github.com/PaulStoffregen/cores) provided by PJRC. Based on this code, as well as some of the blinky led tutorials for the Teensy, he got SPI, I2C and Serial communication working already!

At the time, he had included this in his [Teensy Clock](https://github.com/SimonSapin/teensy-clock) repo, but was having a few problems getting the code cleaned up without breaking functionality. After a bit of working before Rustfest, I wanted to make it a goal to have a Teensy 3.2 library that would meet the following goals:

* Be included like any other Cargo Crate, not copy pasted into every new project
* Minimize the boilerplate necessary to get started
* Build process mainly driven by Cargo, rather than a Makefile
* Rust as the core of the binary, e.g. `fn main() {}`

Throughout that day, as well as a few free hours since then, we've gotten the crate published, and in an initial form that is ready for general consumption. We've broken those items into two crates:

* `teensy3-sys`: containing the C++ code, `build.rs` file used for compilation, and the bare Rust bindings for the Teensyduino code
* `teensy3`: Our abstraction layer above the unsafe bindings, allowing for more ergonomic usage of the code (as necessary), as well as a few boilerplate items necessary to get code running on an embedded system.

## Technical highlights

### Using Servo's Bindgen Against an Existing Embedded Library

In my opinion, this is the most exciting part. This shortens the manual work necessary to get started development using Rust on an Embedded Platform. It also opens up some hope for cross-platform portability, as long as the Arduino API/HAL is available on each platform.

We haven't yet documented or automated the process necessary to repeat the bindgen process, but for posterity, here is the command that generated the code currently in `teensy3-sys`:

```bash
PATH="/home/simon/projects/servo/ports/geckolib/binding_tools/rust-bindgen/target/debug:$$PATH" bindgen --no-type-renaming --match teensy3 bindings.h -o src/bindings.rs -- -I/usr/lib/clang/3.8.1/include -x c++ -std=gnu++11 -target thumbv7em-none-eabi -DF_CPU=48000000 -DUSB_SERIAL -DLAYOUT_US_ENGLISH -DUSING_MAKEFILE -D__MK20DX256__ -DARDUINO=10600 -DTEENSYDUINO=121
```

Hopefully we can automate/clean that up soon.

### Getting an Embedded Crate on crates.io

This was a bit of an exercise, including getting `cargo package` and `cargo publish` [working](https://github.com/rust-lang/cargo/issues/3119) on a custom target-triple, as well as getting docs.rs to add support for `arm-none-eabi-gcc`. I hope that this pushes some conversation on how to package embedded libraries which can be extremely target specific, and how to reach the level of usability that other larger targets enjoy.

## A call for help

Right now, there are already a few issues to clean up, but more than anything else, getting more people using this would be extremely helpful. In particular, the `safe` abstraction layer provided by `teensy` is really just a proof of concept, and could use a ton of suggestions, and pull requests. I will be putting as much effort as possible in the near future to extend this, but more hands would be appreciated! Feel free to reach out to me on [github](https://github.com/jamesmunns) or [twitter](https://twitter.com/bitshiftmask) if you have any questions.

Discuss on:

* [Hacker News](https://news.ycombinator.com/item?id=12584086)
* [reddit.com/r/rust](https://www.reddit.com/r/rust/comments/54ly72/using_servo_bindgen_to_get_rust_on_an_embedded/)