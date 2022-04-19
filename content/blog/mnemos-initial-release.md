+++
title = "MnemOS Initial Release Announcement"
date = 2022-04-19
draft = false
in_search_index = true
template = "blog_post.html"
+++

![Pellgrino Rack](/blog/images/pellegrino-rack.jpg)

Today I'm introducing **MnemOS** v0.1.0, a small, general purpose operating system, written in Rust. MnemOS is designed for constrained hardware, including microcontrollers.

This release includes the v0.1.0 versions of:

* [The MnemOS Kernel](https://docs.rs/mnemos/latest/kernel)
* [The MnemOS Userspace Library](https://docs.rs/mnemos-userspace/latest/userspace/)
* [The MnemOS Common Library](https://docs.rs/mnemos-common/latest/mnemos_common/), which defines the System Call interface shared between userspace and kernel.

Together with the Pellegrino hardware system (pictured above), which is a [Eurorack modular synth] inspired rack system with LEGO mounting rails, it aims to support modular, home-built computer systems.

[Eurorack modular synth]: https://en.wikipedia.org/wiki/Eurorack

Although the capabilities are currently limited, it currently supports a number of features, including:

* [Multiplexed serial ports], allowing for "TCP Port" like addressing of services
* An [RPC-style System Call interface], powered by [serde](https://serde.rs) and [postcard](https://docs.rs/postcard)
* A [block storage interface], useful for loading, storing, and retrieving programs and program data from persistent QSPI flash

[Multiplexed serial ports]: https://mnemos.jamesmunns.com/user-guide/serial.html
[RPC-style System Call interface]: https://mnemos.jamesmunns.com/components/kernel.html#system-calls
[block storage interface]: https://docs.rs/mnemos-common/latest/mnemos_common/porcelain/block_storage/index.html

For more information on what MnemOS is, and how to get started, you can refer to [the MnemOS book], or visit the [GitHub Repository](https://github.com/jamesmunns/pellegrino).

[the MnemOS book]: https://mnemos.jamesmunns.com

<!-- more -->

## What hardware does MnemOS support?

At the moment, the only supported Main CPU is the Nordic nRF52840, specifically on the [Adafruit nRF52840 Feather Express](https://www.adafruit.com/product/4062) development board.

![The Adafruit nRF52840 Feather Express](/blog/images/4062.jpg)

Support for other Main CPUs is possible, but not currently implemented (it's early days!). In particular, it should be pretty straightforward to add [support for the Nordic nRF52840-DK](https://github.com/jamesmunns/pellegrino/issues/3), which is commonly used in Rust-focused learning material, like Ferrous System's [embedded trainings], and [Knurling Sessions].

[embedded trainings]: https://embedded-trainings.ferrous-systems.com/
[Knurling Sessions]: https://knurling.ferrous-systems.com/sessions/

This board has a number of important features, including:

* The nRF52840 Microcontroller, with:
    * a 64MHz CPU
    * 256KiB of RAM
    * 1MiB of Flash
* A Micro USB connector, used for power and as a USB-Serial port
* A 2MiB QSPI Serial Flash chip, used as a Block Storage device for storing data and programs
* A WS2812B RGB LED (also known as a "NeoPixel" or "Smartled") for notifications

The board has many other features, but they are not currently used.

This board can be [purchased directly from Adafruit](https://www.adafruit.com/product/4062), or from a number of resellers.

## Why did I write MnemOS?

**MnemOS** is a "spin off" of part of my previous project, [Powerbus](/blog/nwsltr-2021-12-01/), which is a networked home automation project. It honestly started getting too complicated with too many "crazy ideas" (it's a network stack! and a scripting language! and an operating system!) for one single hobby project. So I split the "networking" part off to a much smaller, simple project (named [Sprocketbus]), and MnemOS, which was more focused on building a single computer system.

[Sprocketbus]: https://twitter.com/bitshiftmask/status/1502479340403146755

This split helped to better focus BOTH parts of the (former) Powerbus system, and may in the future be recombined, when the separate parts have had more time to bake and solidify on their own.

MnemOS is also a spiritual successor to my [Anachro PC project](/blog/anachro-pc-001/), which I talked about at the RustLab conference in late 2020:

<iframe width="100%" height="400" src="https://www.youtube.com/embed/MvcWHmnnMuc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The goal for MnemOS is similar to that of Anachro: Use cheap and modern off-the-shelf hardware to make a PC from scratch that is simple to use. Compared to the original Anachro-PC effort, MnemOS is a more focused, classical-style OS, and benefits from nearly two more years of my learning experience since originally starting work on Anachro.

## Why should I (or you) use MnemOS?

As to "Why should I (or you) use MnemOS?", I don't have a good answer! There is certanly no commercial or technical reasons you would choose MnemOS over any of its peers in the "hobbyist space" (e.g. [Neotron OS], or projects like [RC2014]), or even choose it over existing commercial or popular open source projects (like FreeRTOS, or even Linux). It's mainly for me to scratch a personal itch, to learn more about implementing software within the realm of an OS, which is relatively "high level" (from the perspective of embedded systems), while also being relatively "low level" (from the perspective of an application developer).

[Neotron OS]: https://neotron-compute.github.io/Neotron-Book/
[RC2014]: https://rc2014.co.uk/

At the moment, it has the benefit of being relatively small (compared to operating system/kernel projects like Linux, or [Redox OS]), which makes it easier to change and influence aspects of the OS. I don't think it will ever be anything "serious", but I do plan to use to it to create a number of projects, including a portable text editor, a music player, and maybe even music making/sythesizer components. Some day I'd like to offer hardware kits, to make it easier for more software-minded folks to get started.

[Redox OS]: https://www.redox-os.org/

For me, it's a blank slate, where I can build things that I intrinsically understand, using tools and techniques that appeal to me and are familiar to me. I'd love to have others come along and contribute to it (I am highly motivated by other people's feedback and excitement!), but I'll keep working on it even if no one else ever shows up. By documenting what I do, I'll gain a better understanding (and an easier route to picking it up if I have to put it down for a while), and that work serves to "keep the lights on" for any kindred spirits interested in building a tiny, simple, PC in Rust.

If that appeals to you, I invite you to try it out. I am more than happy to explain any part of MnemOS. Much like the Rust Programming Language project - I believe that if any part of the OS is not clear, that is a bug (at least in the docs), and should be remedied, regardless of your technical skill level.

## What's up next?

Now that I have the initial release out, I plan to move my attention towards expansion cards. I plan to expose expansion cards over a (relatively simple) SPI bus, acting as a sort of "PCI Express"-style backbone.

In particular, I plan next to add support for the [Adafruit Music Maker Featherwing](https://www.adafruit.com/product/3357), which includes a micro-SD card, which I can use for storage of files, as well as a [VLSI VS1053b](https://www.vlsi.fi/en/products/vs1053.html), an audio codec chip capable of playing both WAV/PCM encoded audio (as a "raw audio sink"), as well as a number of standard audio formats, like MP3, OGG, and FLAC lossless audio.

![The Adafruit Music Maker Featherwing](/blog/images/3357-03.jpg)

Additionally, I'd like to add support for some kind of networking hardware. This will likely come in the in the form of Adafruit's [AirLift FeatherWing](https://www.adafruit.com/product/4264), an ESP32-based WiFi peripheral, or their [Ethernet Featherwing](https://www.adafruit.com/product/3201), a [WIZ5500](https://www.wiznet.io/product-item/w5500/) based ethernet controller chip, with a built-in TCP stack.

Feel free to stay tuned, or [open an issue](https://github.com/jamesmunns/pellegrino/issues/new) with your questions or ideas!
