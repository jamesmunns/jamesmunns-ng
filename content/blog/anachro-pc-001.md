+++
title = "Anachro-PC - The Anachronistic Personal Computer"
date = 2020-07-30
draft = false
in_search_index = true
template = "blog_post.html"
+++

> TL;DR - These are my notes for a potential computer hobbyist personal computer architecture. Someone called it "Minix for motherboards".

This roughly describes an architecture of off the shelf microcontroller components that can be used to create a basic standalone PC, somewhere in the neighborhood of performance of an old 286/386 DOS style PC.

If I build this, it will almost certainly be done in Rust. I do hope to specify the protocol/operational semantics well enough that you could create a component that was written in Micro/Circuit Python, C/C++, Ada, or maybe even as an embedded linux PC.

I currently am working on other projects, but I feel like this would be a fun project to stream, or maybe even write a book about learning embedded systems, or learning Rust with embedded systems?

**If you'd be interested in taking a class building/using a system like this, or supporting patreon/GH sponsors style for me to do this, [send me a message](mailto:james.munns@ferrous-systems.com).**

<!-- more -->

## Project Goals

The goal of this project is to design a PC-ish architecture that makes it easy for people learning embedded systems to build a single component. This includes:

1. Making the system resistant to failure of a single component
2. Use only protocols/components that can be easily purchased
3. Be adaptive to allow for variety of components used
4. Value simplicity over performance
5. Make the steps to initial success very short
6. Make this fun for me and other collaborators to work on

## Project Anti-Goals

1. Designing something that is wholly useful in commercial deployments

## Interesting Ideas

These are ideas that I think will help make the project successful.

### Every Component is a Microcontroller - Any Microcontroller.

The idea is to have every part (or **Component**) of the system be its own standalone microcontroller system. Honestly, this is how most computers work today anyway, but the idea is to be able to use almost any microcontroller, from 8051, to Arm Cortex-M, to RISC-V parts, for any piece of the PC. At some point, I can see people even making parts of the PC out of FPGAs as well.

This includes all of the following PC parts:

* The Main CPU/Processor
* An input controller (Keyboard/Mouse/Touch)
* A network interface (Ethernet/Wi-Fi/LPWAN)
* A storage controller (SSD/SD/HDD/RAMFS/USB)
* A Sound Card
* A graphics card (framebuffer, shaders)

The system should use a protocol that almost every device has support for, and is forgiving. For that reason, I plan to use SPI for system communication.

### The Bus Protocol - SPI, but weird.

So, SPI is a simple, fast, and reliable protocol, but the trick is that it is WAY easier to write a SPI Controller, rather than a SPI peripheral. Since I want things to be simplest for the people writing the Components, they should be the SPI Controllers. But this leaves us with a problem, how do we make a PC with N SPI Controllers work with a single SPI peripheral? Here is where it gets weird.

1. Every Component is a SPI Controller, with SCK, COPI, and CIPO pins wired to a central **Arbitrator**.
2. Every Component also has two GPIOs:
    * An output that is a "Request" line. This signals to the Arbitrator that the Component would like to talk
    * An input that is a "Go-Ahead" line. This signals to the Component to begin talking to the Arbitrator

In this system, the Arbitrator will either support being a SPI Peripheral for a lot of lines, or will handle MUXing the SCK/COPI/CIPO pins as necessary.
The Arbitrator will decide which component it wants to talk to, and for how long.
When a Component pulls its Request line low, the arbitrator will eventually acknowledge this by pulling the Component's Go-Ahead line low.
The Component can begin clocking SPI data at whatever speed it feels like, up to the maximum speed supported by the Arbitrator.
When the Component is done sending/receiving data, it checks whether the Go-Ahead line is still low.
If so, then the message was "accepted" by the arbitrator.
If the Go-Ahead line is released high before the Component releases the Request line, this means that the arbitrator has "hung up" on the Component, meaning either an error or timeout has occurred.

### The Arbitrator - Basically a Northbridge chip

The Arbitrator has two primary tasks:

1. Arbitrating the Bus Protocol as described above, servicing and discovering components that have been connected
2. Managing memory allocations used to communicate between devices

I've already described the lowest level of the protocol above - we'll use an awkward SPI communication. However I haven't described how the higher protocol layers work.

All devices will communicate through a mailbox system.
The arbitrator will take data from the Components, and place them in an in-memory object store.
Each created item will be assigned a UUID, which will be returned to the Component on creation.
This UUID can then be placed in a mailbox to another component, sending access to the data to that component.
Each item is read-only.

Example (psuedocode):

```
// A binary RPC messages are sent from Component to the Arbitrator
// The format will probably be binary, but maybe with an alternative
// command to use the following REPL format?
//
// Components are also assigned a UUID on boot. This Component has
// the own-address of 9ea8b6a7-2967-4db8-98b8-d4577548ed04.

// Data can be stored to the Arbitrator memory space. Data can then be
// referenced as inter-device storage using UUIDs as a reference. Data
// is allocated on a FIFO basis, with oldest memory items becoming
// dropped.
//
// The arbitrator may choose to limit the rate, maximum size or other
// parameters of creating memory items based on configuration.
CREATE(
    // number of bytes to write, can be set to zero for dynamic
    // length using something like COBS or when the Request
    // line is de-asserted
    13,

    // The payload of the data
    "Hello, world!",

    // No UUID provided to send to another component, just return
    // the newly created UUID. If provided, this would place
    // the created UUID into the mailbox of another component
    None,
)
// The following UUID is returned to the Component on success
-> Result<3b2fd5d1-ae16-46af-afc1-f60241d0a5b6, CreateError>

// You can send data by reference to another component you know's
// mailbox. Mailboxes are provided as a Component's address. Mailboxes
// are a FIFO queue of UUIDs that can be loaded by that Component
SEND_MAILBOX(
    // The data reference to send
    3b2fd5d1-ae16-46af-afc1-f60241d0a5b6,

    // The destination address
    56c3dbda-c762-4107-be58-855dc8e5aa92,
)

// The other device can receive messages on a FIFO basis, and can view
// the item at the top of the stack without removing it
PEEK_MAILBOX(
    // You can provide Some(usize) as a max message size, or None for
    // anymessage size. Messages larger than the usize value will
    // instead return an Error
    Some(32),
)
-> Result<(13, "Hello, world!"), GetError>

// The other device can receive messages on a FIFO basis, and can view
// and remove the item at the top of the stack. If the Controller
// ends the message before all bytes are received, the item is still
// removed from the FIFO. Thiscan be used to simply drop the item on
// the top of the FIFO.
POP_MAILBOX(
    // You can provide Some(usize) as a max message size, or None for
    // any message size. Messages larger than the usize value will
    // instead return an Error
    Some(32),
)
-> Result<(13, "Hello, world!"), GetError>

// TODO: How to have a "clone and modify" operation that isn't hard
// because of re-allocs? Insertions would suck unless I used some kind
//  of rope structure, which might be too complex to implement
```

You can also use the SPI interface for certain communications directly to the arbitrator

```
// Register ourself using an enumerated type ID
//
// TODO: What to do when calling this more than once?
REGISTER_TYPE(
    IO_CONTROLLER,
) -> Result<9ea8b6a7-2967-4db8-98b8-d4577548ed04, GetError>

// Get the ID of ourself. Matches ID given on registration
GET_OWN_ID()
-> Result<9ea8b6a7-2967-4db8-98b8-d4577548ed04, GetError>

// Get limits of the arbitrator interface
GET_ARBITRATOR_LIMITS()
-> {
    min_speed_hz: 125_000,     // What is the minimum SPI clock rate?
    max_speed_hz: 8_000_000,   // What is the maximum SPI clock rate?
    exp_polls_per_sec: 100,    // What is the expected poll frequency?
    request_line_shared: false,// Is the request line open drain?
    total_memory: 524288,      // 512KiB
    max_files: 512,            // Max number of records alive at once
}

// Get limits for message creation
GET_CREATE_LIMITS()
-> {
    max_bytes: 512,             // Largest message can be 512 bytes
    max_bytes_per_second: 4096, // Running resource limits
    messages_per_second: 10,    // Running resource limits
}
```

> TODO: How to register multiple addresses/logical addressing? e.g. for keyboard that has a mouse and touchpad?
> Could add a "from" field to every message, but then I'm adding a routing layer?

### An easy bootloader

Write a simple bootloader that can enumerate on the bus, take an image, and reboot? PXII boot style? Would need to enumerate type
and maybe even serial number or something to load the right firmware to the right place.

## The First Implementation

These are ideas for possible first implementation of the PC architecture described above

### A Simulator with real-world hooks

I could create a simulated environment for these components, using no_std libraries and using TCP over localhost to emulate the SPI target environment, basically providing an I/O library or a "HAL" for simulating each component inside of a system. Maybe even port RTIC to the simulated environment, or even just use QEMU, using Semihosting for simulated SPI/GPIOs?

With a little work, I could also probably have an arbitrator or even just a simple SPI controller sit outside of the PC, bridging one or more simulated components to a shared network with physical components.

This would allow me to bring up multiple devices quickly, both from a Component software perspective as well as a CPU support for the Anachro-PC architecture.

### Using an nrf52840-dk as an arbitrator

Since the nRF52 already has an internal pin mux, I could use an nRF52840, which has like 36-48 GPIOs, to act as a physical arbitrator. Assuming you need the following pins for each component:

1. SCK
2. COPI
3. CIPO
4. REQUEST
5. GO-AHEAD

That means we could probably support 5-8 devices? Maybe more if the request lines are shared? Maybe less if I want external QSPI memory for storage? Then you could just hand-wire the dev boards together, which would be tedious, but possible without me buying new hardware.

Downside is that the nrf52840 only supports a max speed of 8mbps as a SPI peripheral.

### Make an arbitrator board

I could put an nrf52840 or something on a PCB, then break out all the pins to \~8 pin headers. That would allow you to easily wire a harness for each external component, or even do something silly like run the lines over an RJ45 or something.

I could also make simple adapters for common footprints, like PJRC's Teensy, Adafruit's Feather, or the Arduino Uno R3 format. These would be no-component PCBs, with thru-hole solderable headers that you could use dupont headers, or some kind of standard 2x4 ribbon cable.

### Mix and match

To start, I'll probably make everything with nRF52s to start, because I have a lot of them at hand. In the future, I'll probably start adding

### Make a microATX (or smaller) motherboard?

Once I have a design that works, I could make a jumbo sized PCB with full motherboard-ish components. This would be REALLY cool, but also probably REALLY expensive or time consuming to do in tiny quantities
