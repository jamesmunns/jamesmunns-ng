+++
title = "CI for Embedded Systems"
date = 2017-05-07
draft = false
# tags = ["tag1", "tag2"]
# category = "rust"
aliases = ["update/2017/05/07/hardware-ci-overview.html"]
in_search_index = true
template = "blog_post.html"
+++

> I was wondering what solutions exist for CI in the embedded space. I'm trying to streamline and speed up project development ... and feel CI might help in that process. I come from a higher level language background and have seen tools like TeamCity and Vagrant manage the build-test-deploy pipeline, and was wondering if this is a thing in the embedded world too.
> - Vignesh Sankaran

I recently received this email after talking about CI (Continuous Integration) for Embedded Systems in an IRC room. After a quick response, I thought that the subject was worth posting about. I'll cover a couple different techniques I have used at different companies, and try to list the benefits, challenges, and a little bit of detail for each. This information is knowledge that I have gathered over my years developing and testing embedded systems, ranging from safety critical Avionics, all the way down to rapidly prototyped IoT devices.

<!-- more -->

In the future, I would like to give actual examples on how to set each of these up, but for now, we will start with a high level overview of how each of these approaches are structured, and how they can help your current process. As a note, I expect that you are already using some kind of version control system (such as Git, SVN, Mercurial, etc). If you aren't doing this already, now is the time to start! Heres a quick overview of the different types of CI Testing I will cover:

Technique               | Testing Type                          | Effort Level  | Testing Value
 :--------              | :---                                  | :---          | :---
CI Build                | Smoke Test, Static Analysis           | Low           | High
Non-Host Testing        | Unit Testing, Integration Testing     | Medium        | Medium-High
Host Testing            | Unit Testing, Integration Testing     | Low to High   | Medium
Simulated Host Testing  | Unit Testing, Integration Testing     | ?             | ?
"Native" Host Testing   | Unit Testing, Integration Testing     | Low to High   | Medium-High
HIL (Easy)              | System Testing                        | Low to Medium | High
HIL (Hard)              | System Testing                        | High          | Medium-High


### CI Build

#### What is it?

<img src="../images/ci-build.svg" alt="CI Build Diagram">

CI Building is the process of setting up your compilation process, as well as any static analysis you have set up (such as LINTers, Code Quality or Style checkers, Max Stack usage, etc) to be run on a CI server. Ideally, this build would be triggered on any commit, and run in a textually defined environment such as Docker or Vagrant.

I would highly recommend this form of CI testing for nearly any embedded project.

#### What is the cost?

* Set up your build/analysis process in a docker container. Make sure it builds reliably, and produces valid firmware and analysis reports
* Set up a CI server such as Jenkins, CircleCI, etc.
* Set up a commit or time based trigger to execute the job regularly
* Make sure to capture the outputs (firmware binary, reports).

I would estimate it would take a day or two to get this going, with a bit of additional effort if you aren't familiar with docker or CI tools. This could also take more effort if you don't have "one touch" builds already (e.g. you can just type "make" or "./build.sh").

As a note, if you use proprietary tools such as a compiler that requires a license, you may need to factor in the cost and effort of provisioning your test server to have correct tool access, licenses, etc. Additionally some proprietary tools require more effort to automate on a script-able level (specifically lots of fully integrated IDEs, such as Keil, IAR, and others, particularly on Windows).

#### What is the benefit?

* No more "it builds on my machine!", the CI server is the official pass/fail check
* Immediate feedback whether the build is broken, especially important when working on a team
* It is possible to track metrics like code size, stack usage, code quality, etc. over time using the outputs from your reports
* Testers have access to the newest binaries, without asking developers for specific builds
* It forces you to have "one touch" builds, and forces you to define an official build environment (tools, tool versions, etc), which is critical for any project

### Non-Host Testing

#### What is it?

<img src="../images/ci-non-host.svg" alt="Non-Host Testing Diagram">

Non-Host testing is the action of running any Unit or Integration tests you have, but compiling and running them on a different platform (e.g. compile and run on x86 instead of ARM, MSP, etc). This allows you to test the business logic of your code, without necessarily testing platform-specific behavior. It is also possible to capture other reports, such as Code Coverage reports.

This tends to work fairly well if you have modular code, and are focused on testing code behavior above the Hardware Abstraction Layer. This technique is not well suited for testing very low level code, such as memory-mapped hardware interactions.

You may even decide not to use your primary compiler, and use something like GCC for your tests, rather than something like the IAR compiler. This can be a positive (better tooling, easier automation), but again can force you to have code that is portable between different compilers, which is a good thing, but may require extra effort, at least at the beginning.

Additionally, this technique will not catch any hardware specific integration bugs. For example, unaligned memory reads will work on x86, but not on ARM processors (it will throw a fault). Also be careful about the different pointer widths between x86/x86_64 and embedded platforms (8, 16, 32, or 64 bit pointers, depending on your platform).

I would recommend this testing for any non-trivial embedded project (projects lasting months to years), especially if requirements are not rapidly changing. For green field projects, it is much easier to write portable code which will "play nice" with multiple platforms. For projects with lots of legacy code or legacy tests, it may be worth experimenting to see the effort required to bring the code up to date.

#### What is the cost?

* Requires you to have "one touch" testing builds, e.g. "make test", or "./test.sh"
* Requires you to have at least some tests which can be compiled and run successfully on your CI server's platform
* Set up a CI server
* Set up commit or time based trigger
* Capture the test result outputs

Depending on your current environment, code base, and tools used, this could range from just a few hours to set up, or could require rework of source code or tests to be more portable.

#### What is the benefit?

* Constant testing feedback across all commits and branches
* Testing does not require physical hardware, allowing test runs on nearly any machine

Tests that are run automatically and continuously have a wonderful level of feedback, and prevent unexpected regressions. Even without testing low level behavior, there is a very high level of return on these kind of tests.

### Host Testing

#### What is it?

<img src="../images/ci-host-test.svg" alt="Host Testing Diagram">

Some Unit Testing frameworks are lightweight enough to be run on target hardware. Host testing allows the the CI server to cross compile these tests, load them to the target hardware, run them there, and collect the reports via a serial port or other interface.

This allows unit tests to catch business logic errors, as well as platform specific issues.

I would recommend this form of testing if Non-Host testing is difficult to implement due to portability concerns, or if your platform has "oddities" which have caused you significant pain in the past (such as different sizes of pointers vs ints, code which has to behave differently in extended memory sections, etc).

#### What is the cost?

The largest cost here is setting up the testing to work on the target platform. This introduces some additional restrictions above Non-Host Testing, such as:

* Every test runner requires physical hardware, as well as tools such as a debugger, and a serial port (or adapter) to collect reports.
* The target hardware must have enough resources to store and report test results, as well as additional data such as coverage information. It is common to use a larger version of a processor in the same family, which has additional RAM, Flash, or Peripherals to support testing.

It is also important to note that by requiring physical hardware, you will be limited in the number of tests you can run in parallel. You may need to also buy additional debuggers or tool licenses for each test runner.

If you do not already run tests on your target system, expect a fair amount of effort to get this working for the first time.

#### What is the benefit?

Similar to Non-Host testing, you will get continuous feedback on the test status of your project. By running on the target, you also avoid the "cost" of having to write portable code, and will be able to catch hardware specific integration problems.

### Simulated Host Testing

<img src="../images/ci-host-simulated.svg" alt="Simulated Host Testing Diagram">

Simulated Host Testing is somewhere between Non-Host Testing and Host Testing. Rather than run on physical hardware, you use a tool such as QEMU to simulate your target platform with a high level of accuracy.

Ideally you would get the best of both worlds: Catch logic and integration errors, and not require any physical hardware at testing time.

I have not personally set up this kind of testing, so I cannot comment on how hard or easy this is, or how it compares to Host or Non-Host testing. I would appreciate feedback from any developers out there who are using this technique in practice!

### "Native" Host Testing

<img src="../images/ci-native-host.svg" alt="Native Host Testing Diagram">

#### What is it?

Native Host Testing is the process of replacing hardware drivers below the Hardware Abstraction Layer (HAL) with simulated components which use regular PC interfaces to expose or simulate the components that they replace. For example, the firmware application code uses a HAL for the ethernet controller. Rather than using the low level driver that interfaces between the HAL and the physical ethernet controller, the Native ethernet driver communicates with a simulated linux network interface, so that communication can happen locally. This code is compiled and run entirely within a regular PC domain (for example x86 or x86_64), without the use of Simulators, Emulators, or any target hardware.

This approach requires a modular software design, as well as portable code design, at least down to the HAL, so that the code may be compiled and run on a PC, rather than on the target hardware. Many open source embedded OS/RTOSs, particularly OSs that focus on network communication such as RIOT-OS and Zephyr, already include the tooling and interfaces to provide Native Testing "out of the box", even for simulation of entire networks of devices, as well as simulation of unreliable wireless networks.

For companies with complex systems that typically include multiple interconnected embedded devices (such as Automotive, IoT, Industrial, or Avionics systems), entire networks of dissimilar devices may be simulated to reduce initial integration testing, as well as allowing for the use of automated Continuous Regression Testing, to verify that changes to one firmware do not negatively affect other parts of the system.

Native host testing will not completely replace end-to-end testing with physical hardware, especially with regards to regulatory testing (SIL, DO-178, FCC, or CE certification testing), however it can lead to increased functional confidence between end-to-end tests, as well as a reduction of time spent setting up, running, and debugging hardware tests. Some regulatory agencies will also accept Native testing as an acceptable form of Integration Testing, particularly if backed with end-to-end System Testing with physical hardware.

This approach is highly recommended if your project is based on an RTOS or tooling which already supports some or all functionality already. Additionally I would recommend this approach for long-lived or quality-critical applications with a high level of complexity, or for projects with particularly expensive hardware, or for projects which require expensive equipment to test, analyze, or simulate (such as wireless interfaces, in particular).

A friend and former coworker of mine has written his Diploma Thesis in this topic, specifically for the initial implementation of the Native framework in the RIOT-OS project, and I highly recommend reading it for anyone interested in implementing or understanding this technique. The paper is [Virtualization of the RIOT Operating System](http://cst-pub.imp.fu-berlin.de/knuepfer-diploma-thesis.html) by Ludwig Ortmann/Knüpfer.

#### What is the cost?

For this technique, the cost highly depends on your project. If you do not have a strong isolation between Application code and Hardware Driver components (e.g. a well defined Hardware Abstraction Layer), this technique will have a high barrier to entry. If you have a well isolated HAL, there will still be a fair cost to re-implement your hardware level drivers in a way that facilitates testing, and is an accurate simulation of your target hardware.

However, if your project is based on an RTOS such as RIOT-OS, Zephyr, NuttX, or others where the HAL is already pre-defined, and the OS projects have already defined and implemented the simulation components for OS and common interface components, the cost for this technique is drastically reduced. These RTOS's allow the developer to run their application on an x86 or x86_64 target, and the network interfaces and sensors are made available over virtual serial ports, virtual network interfaces, or TCP/UDP sockets.

There will be additional overhead introduced by maintaining two drivers for your project - one for the actual hardware, and one for the x86 "hardware", so this technique is best approached after the Hardware Abstraction Layer has been well defined, and changes to the low level drivers are relatively infrequent.

#### What is the benefit?

Similar to the entire family of Non-Host testing, this approach trades a higher initial setup cost for testing, for a much greater ease-of-use during application development or maintenance. By not requiring physical hardware to perform reasonably accurate testing, the iteration time between development and integration testing can be drastically reduced.

The most visible and rewarding benefit to this approach is the ability to debug and test at an incredibly rapid pace. Since the application is running on a local development environment, normal debugging tools such as GDB can be used, as well as additional dynamic analysis tools such as Valgrind to track memory allocation (and leaks), GCC instrumentation to measure live stack usage and other runtime checks, and tools like kcov to measure code coverage. Outside of the main application logic, if network or other communication is made over network interfaces or sockets, tools like Wireshark can be used to analyze, record, modify, and replay communication which can contain edge cases and hard-to-reproduce bugs or unusual behavior. These tools also often have extensions or plugins for analyzing non-IP based protocols as well, such as Bluetooth Low Energy. These logs can be stored (sometimes on every test run) to allow for later in-depth offline analysis.

Normally these techniques would require highly specialized (and highly expensive) tools to measure, and would take a high level of planning to support in hardware. By moving into a fully-software domain, free and/or open source tools allow an amazing amount of code introspection, with an incredibly low cost (in both time and money).

### HIL Testing (Easy)

#### What is it?

<img src="../images/ci-hil-easy.svg" alt="Easy HIL Testing Diagram">

HIL or Hardware In the Loop testing entails using your physical hardware target to run high level tests (typically using the "release" or "debug" firmware). The "Easy" version of this can be used when your device uses "normal" interfaces that can interact with a PC. This could include Ethernet, Serial Ports, or even interfaces like CANbus which can be connected via a USB adapter. It is also important that these tests do not require a high level of timing accuracy, as most Desktop PCs cannot respond reliably on the millisecond or below level.

An example of a high level test would be to send some kind of data via an Ethernet interface simulating sensor data, then requesting the processed data output, simulating a display, then comparing the expected and actual results.

If communicating with your device requires custom hardware, or a high level of timing accuracy, see the "Hard" version of HIL testing.

#### What is the cost?

Similar to Host Testing, you will require physical hardware to upload code to, as well as any additional hardware (such as an additional Ethernet interface, or USB to Serial adapter) necessary to communicate with your target. This may be a significant limitation to your test setup or running process.

Additionally you will need a test framework to write and run your tests in. I have used and would recommend PyTest (a testing framework for Python) to handle this, and it works well if Python libraries exist for your needs, such as Requests for HTTP based interfaces, or PySerial for Serial based interfaces.

Timing is always a concern, as you want to avoid excessive timeouts to prevent long running tests, however you also want to avoid tests failing due to minor timeout issues which may be caused by the test runner rather than the target hardware.

I would recommend this form of testing for long lived projects (many months to years), or if you work on many similar projects where the effort put into setting up the test environment and tooling (such as writing a specific library for interactions specific to your device(s)) can be reused. There is a non-trivial setup cost to getting these environments working reliably.

#### What is the benefit?

Unit tests, while valuable, only catch a certain class of errors. Particularly in embedded systems, the really hard to find and fix issues tend to come from integration issues. By having automated system tests using your real hardware from a high level, many of these issues can be caught without expensive human driven QA, and allow regressions to be caught early.

### HIL Testing (Hard)

<img src="../images/ci-hil-hard.svg" alt="Hard HIL Testing Diagram">

This approach builds on top of the easy version of HIL testing, however some devices require unconventional, proprietary, or custom interfaces to interact with. Additionally, some testing requires millisecond or sub-millisecond precision for accurate testing (especially safety critical devices).

For these applications, it may be necessary to offload some behaviors to a "testing coprocessor", which could be a microcontroller such as an Arduino, an embedded linux device such as a Raspberry Pi, or other controllable hardware such as a power supply, logic analyzer, power meter, etc. This typically requires writing much more specific testing drivers, which means a higher level of initial investment.

For example, it would be possible to take your embedded device, replace all buttons with a GPIO driven by an Arduino, replace all LEDs with GPIOs read by an Arduino, and replace an SPI driven screen with an Arduino which captures all SPI data fed into it.

I would recommend this approach only for long lived projects (multiple years) with a high expectation of testing accuracy (such as safety critical systems).

#### What is the cost?

On top of the costs of "Easy" HIL testing, expect a great deal of effort to add support for any custom tools necessary, and expect additional monetary costs for tools such as logic analyzers and power meters that can be remotely controlled.

There are many tools that can be used off of the shelf, or off the shelf tools (like Arduinos/development boards) that can be adapted for testing usage, however be careful to make sure that these tools either work out of the box for your uses, or that you are willing to spend the effort to adapt them to your needs.

Without reuse of this tooling, the development cost of your testing may approach a significant amount of your development effort, perhaps even meeting or exceeding the development effort for your device!

These costs are only typically acceptable when used and/or reused for many years across one or many projects, or where the cost of human/manual testing is very high, or a high level of reliability is an absolute must (again, talking about safety critical devices).

#### What is the benefit?

All of the benefits of Easy HIL testing, with the additional flexibility to test, measure, or log nearly anything that your device does. With enough effort, an incredible amount of hardware testing can be automated.

# Summary

Phew! That was a lot of information. For a TL;DR, I would suggest that ALL embedded projects start using CI for build testing, any non-trivial embedded project looks into Native, Non-Host, Host, or Simulated Host testing, and that any project with a long lifetime, or high quality requirement look into some kind of HIL testing. At the end of the day, it is important to put the right level of testing effort, as under-testing leads to expensive late-caught bugs, and over-testing can have quickly diminishing returns (which makes managers and businesses sad).

If you have any questions, please feel free to reach out to me on twitter @bitshiftmask, or by email (on my About page). I would love to hear any thoughts, corrections, or additional experiences you may have.

[Discuss on HackerNews](https://news.ycombinator.com/item?id=14285787), or [Discuss on Reddit](https://www.reddit.com/r/embedded/comments/69rrku/continuous_integration_for_embedded_systems/)