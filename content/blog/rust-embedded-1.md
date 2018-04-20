+++
title = "Rust <3's Embedded"
date = 2017-05-23T14:30:00+02:00
draft = false
# tags = ["tag1", "tag2"]
# category = "rust"
aliases = []
in_search_index = true
template = "blog_post.html"
+++

As a note, this will be the first in a series of posts exploring content I will be presenting to the **Rust DC** group on June 15th, where I will be integrating Rust code on the [nRF52 Development Kit](https://www.nordicsemi.com/eng/Products/Bluetooth-low-energy/nRF52-DK) to create a Rust-Powered Bluetooth Peripheral. See [the meetup event](https://www.meetup.com/RustDC/events/239115658/) for more information. This post will serve as the first introduction to a few topics, and I will be building on this information as I later discuss exact techniques that can be used to get Rust on more and more embedded systems. In general, I will be focusing on integrating Rust into existing C and C++ ecosystems, to reduce the barrier to entry for Embedded Rust Developers.

<!-- more -->

# What are Embedded Systems?

So, this is a hard question to start with. Generally today, "Embedded Systems" have come to mean more or less any computer you don't sit in front of (like a laptop or a PC). This includes things like fitness trackers, digital signs, the electronics in your car or airplane, the circuits that control toys, or even large industrial machines. This covers a wide range of systems, but the primary thing these systems have in common is that they are designed for a specific purpose, and typically are constrained on one way or another. A constraint could be battery life, reliability, processing power, memory or storage constraints, or many more. In this area, the most common systems are often either Linux based at the high end, down to "bare metal" - or without an OS at the low end.

## What is Embedded Linux?

For projects where extremely high reliability and hard-realtime capabilities are not essential (for example, a digital sign vs. avionics), and development time is a hard constraint, embedded linux systems are commonly put in place. These systems are still relatively constrained compared to desktop PCs, often featuring a <1-GHz ARM CPU, with 256MB to 1GB of RAM, and often only a few hundred MB or single digit GB of flash based storage, however are still capable of running a full distribution of linux like Debian or Ubuntu, or a lighter weight variety like LEDE or OpenWRT.

These devices can take advantage of the Linux OS for scheduling and task management, as well as management techniques such as remote control with SSH, or upgrade management with tools like apt-get or opkg. They also typically have full network communication abilities (for better or worse), which often makes them targets for malicious purposes when they are not properly secured.

These devices can also take advantage of a wide variety of general purpose open source libraries for tasks such as displaying information, encryption libraries for secure communications via SSH or SSL/TLS, and data processing and storage libraries.

As devices such as Smartphones and Tablets have gotten more and more popular, the economies of scale have allowed Embedded Linux devices to become cheaper and more available. For example, the Raspberry Pi family is based on a chipset from Broadcom that was used in Android Smartphones in the early days of Android, and benefited from the low cost of these chips, and support in the Linux kernel contributed for Android consumption.

These devices support nearly every programming language supported on desktop computers, however for anything computationally or memory intensive, these devices tend to favor C/C++ due to the ability to control and optimize when necessary. Programs written in Node, Python, or other high level languages will typically struggle with memory, CPU, or storage constraints if scaled too large.

## What is Bare Metal Embedded?

For projects where cost per unit has to be minimized (high volume consumer devices), hard-realtime promises have to be made (safety critical devices), or low power consumption is needed (batteries lasting months to years, or only occasional access to unreliable power such as solar panels), microcontroller based systems are the typical choice.

For these targets, "Bare Metal" may be a bit of a misnomer. Bare Metal is typically used to describe systems without an operating system, and only run a single application firmware which directly manages all hardware necessary to be controlled. Today, microcontroller devices running a lightweight operating system designed for microcontrollers, such as Contiki, FreeRTOS, RIOT-OS, Zephyr, or even non-OS software libraries which provide an abstraction of the underlying hardware are also typically referred to as Bare Metal.

These systems tend to be incredibly diverse, as they are highly specialized for their particular use cases. This means that it is difficult to write libraries which can be widely used, as many platforms may have different CPU architectures (ARM, MIPS, Atmega, PIC, etc.), different CPU register or memory address widths (8-bit, 16-bit, 32-bit, or 64-bit), they may or may not have hardware-accelerated Floating Point Units, let alone hardware accelerated functions used commonly for encryption or signing data.

Because of this, many devices and the libraries needed to operate them are developed from scratch, and with less widespread usage per-library, these libraries tend to be less general purpose, hard to configure, and often introduce programming or logic errors that have already been solved in other instances of the libraries.

# What is Rust?

Rust is a systems language, which puts it in the neighborhood of abilities and design trade offs typically made with languages such as C and C++. It provides many modern language conveniences found in higher level languages such as an excellent package manager and build system, strong guarantees on memory safety, functional programming tools such as iterators, and the ability to use tools like map() and collect(), and available and high quality libraries for many common actions such as serialization/deserialization, interfacing with databases, interfacing or even providing web services, and far more. Rust does all this, while still allowing powerful control over memory allocation, and compiling down to an efficient and fast binary, without any heavy runtime.

Additionally, Rust does support interoperability with libraries written with C bindings, meaning they can interact bidirectionally between C code, either at compile time (e.g. compiling a C library together with Rust code), or at runtime (using a dynamically linked library written in C with Rust code).

Rust is based on the LLVM compiler, which generally means that any platform that is supported by the LLVM compiler (including x86, ARM Cortex-A, and ARM Cortex-M processors, and a variety of flavors of MIPS, among others), can be used with Rust. This does not necessarily mean that all libraries will work "out of the box" on these devices, but the core of the language will. In a later post, I will discuss this divide a little deeper.

## Why Rust on Embedded?

For devices where code size, speed, or control is a must, Rust can provide these levels of control while also providing tools and comforts that are typically fairly painful in C or C++. Rust won't be replacing C or C++ completely any time soon, due to their long histories and number of active and proficient developers, but there is a movement starting now to provide Rust as a viable alternative for embedded platforms.

In software it is critical to use the "right tool for the job", as opposed to trying to define "which tool is best" in a global sense. In my opinion, Rust is an excellent tool for many challenges faced by embedded developers, especially where quality, robust error handling, and memory safety are a must-have.

In the short term, my focus will be on integrating Rust into existing C and C++ ecosystems, so that Rust developers can leverage existing high quality libraries, and focus on developing new functionality in Rust, rather than attempting to reinvent the wheel by rewriting everything in Rust. This could mean integrating Board Support Packages from manufacturers like Nordic Semi, TI, or STMicro, software libraries such as [mbed TLS](https://tls.mbed.org/), or even embedded operating systems like [RIOT-OS](https://riot-os.org/), [Apache MyNewt](https://mynewt.apache.org/), or [Zephyr](http://zephyrproject.org/).

This technique of getting Rust and C/C++ working together seamlessly on embedded will be the primary focus of my upcoming talk, particularly for "Bare Metal" embedded devices. I plan to cover tools like [Bindgen](https://github.com/servo/rust-bindgen), which allow the automatic generation of Rust interface code to C and C++ libraries, as well as Rust-focused tooling such as the [Cortex-M](https://github.com/japaric/cortex-m) and [svd2rust](https://github.com/japaric/svd2rust) libraries which allow for native integration of Rust onto embedded platforms.

I believe that more and more, developers like [Japaric](http://blog.japaric.io/) and many others will help to build a Rust-first ecosystem, which will have many long term benefits. Until manufacturers begin supporting Rust as a first-choice target, I want to help more and more developers getting Rust into production today, rather than waiting for a completely Rust-based ecosystem to materialize.

Check back soon for more details, and let me know if you have any topics you'd like me to cover, either on twitter [@bitshiftmask](https://twitter.com/bitshiftmask), or my email at the bottom of the page.

[Discuss on Reddit](https://www.reddit.com/r/embedded/comments/6cv2ey/rust_3s_embedded/)