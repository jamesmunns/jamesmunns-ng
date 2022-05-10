+++
title = "The run-up to v1.0 for Postcard"
date = 2022-05-10
draft = false
in_search_index = true
template = "blog_post.html"
+++

Quoting from the README:

> Postcard is a #![no_std] focused serializer and deserializer for Serde. Postcard aims to be convenient for developers in constrained environments, while allowing for flexibility to customize behavior as needed.

I first published [`postcard`] back in 2019, as a way to get "all the good stuff from [Serde]" in a format that would work for embedded systems. Now, 3 years later or so, it's about time to take it to v1.0. Since then, people all over Rust are using Postcard as a general purpose, [compact], and flexible Serde format, not just embedded folks!

Thanks to a bunch of accumulated experience over the years, and a generous sponsor, I'll be releasing the 1.0 version of Postcard in June of 2022.

Read on for more details on what's planned!

[Serde]: https://serde.rs
[`postcard`]: https://docs.rs/postcard
[compact]: https://github.com/djkoloski/rust_serialization_benchmark

<!-- more -->

## Sponsorship

Earlier in the year, I mentioned that I was interested in taking Postcard to v1.0. A couple of folks reached out to me,
and after some discussion, I got in contact with the folks at Mozilla, who were interested in the work. Specifically:

> Work towards the Postcard Specification and portions of the Postcard 1.0 Release has been sponsored by Mozilla Corporation.

Thank you to the folks at Mozilla for sponsoring this work! I'm always excited to work on tools/libraries/applications that I've written,
and if any of y'all out there are interested in any of my other works, please feel free to get in touch and [send me an email]!

[send me an email]: mailto:james@onevariable.com

## What's on the table for 1.0?

There's a couple things that **definitely** will happen for v1.0, and a couple things that **I hope** will be possible in that time.

The "Must" list includes:

* Writing an official "wire format specification" of Postcard, in order to make it more possible to use the same format outside of Rust and/or Serde.
* Writing a validation test suite against the "wire specification", to show that it is a stable format, and to prevent any regressions on future changes
* Addressing the `usize`/`isize` limitation of the [Serde Data Model], which can cause portability problems when communicating between 16/32/64-bit platforms (see below for more details/applicability of this!)
* Fixing any (other) open known defects of Postcard

[Serde Data Model]: https://serde.rs/data-model.html

The "Maybe" list includes, in order of my preference + possibility thoughts:

* Removal or simplification of the ["Flavors"] API, which allowed for serialization "middlewares", like [COBS encoding] or Checksumming without multiple explicit steps
* Looking at alternative "variable length encoding" techniques, such as those used by [`vint64`], rather than my current [`LEB128`] or ["varint"]-style encoding
* Provide a way to determine "maximum message size" when encoded, which can be used to properly reserve space for serialization/deserialization
* Provide a way to produce the "wire format" for a given datatype

["Flavors"]: https://docs.rs/postcard/latest/postcard/#example---flavors
[COBS encoding]: https://en.wikipedia.org/wiki/Consistent_Overhead_Byte_Stuffing
[`vint64`]: https://crates.io/crates/vint64
[`LEB128`]: https://en.wikipedia.org/wiki/LEB128
["varint"]: https://developers.google.com/protocol-buffers/docs/encoding

Outside of this list, but semi-related, I've been granted ownership of the [`cobs`] crate, and intend for it to reach 1.0 as well. Postcard has traditionally used a [fork of `cobs`], but these changes will be merged back "upstream".

[`cobs`]: https://docs.rs/cobs/latest/cobs/
[fork of `cobs`]: https://docs.rs/postcard-cobs/latest/postcard_cobs/

## The "Must Do" items

This section outlines some of the details and motivation behind the items on the Must Do part of the push to 1.0. These items will definitely be included in the 1.0 release.

### Writing an official "Wire Format Specification"

In this context, the "wire format" is generally "what will the data look like when serialized".

At the moment, there is no comprehensive documentation of what Postcard data looks like on the wire. It is generally assumed (or tacitly required) that you have Rust, Serde, and Postcard on both ends of the wire. I have also never explicitly given stability guarantees on Postcard's wire format, though as far as I am aware, it has not changed since the original 0.1 release.

Once specified for 1.0, I would consider any non-backwards-compatible changes or extensions to this wire format a "breaking change".

#### A little history

Postcard's current wire format was heavily inspired by the [`bincode`] and [`ssmarshal`] crates. At least at the time when postcard was first written, both of these formats had limitations that made them unreasonable to use on embedded. [`bincode`] had limited (or no? I can't remember) support for `no_std` targets like embedded, and while [`ssmarshal`] did support `no_std`, it was limited to `repr(C)` types, meaning no `enum`s or slices, and could not encode arrays longer than 255 items.

[`bincode`]: https://docs.rs/bincode/latest/bincode/
[`ssmarshal`]: https://docs.rs/ssmarshal/latest/ssmarshal/

The main differences/"innovations" that postcard introduced were:

* The use of ["varint"]s to describe enum variants, meaning in most cases where you had less than 127 variants of an enum, it would always be encoded with a single byte
* The use of ["varint"]s to describe slice and array lengths, meaning that if you had 127 or less items, length would only be one byte, and if you had 16383 or less items, length would only be two bytes
* Data is always encoded in Little Endian order, which matches the vast majority of desktop, server, and embedded CPUs today.

Similar to `bincode` and `ssmarshal`, `postcard` is not a self-describing format, which means both the serializing and deserializing need to know the schema ahead of time. This is typically done by having them share a common crate which defines the "wire types" as Rust datatypes.

#### Approaching Spec Writing

As postcard is largely based on the Serde crate, the majority of the specification will be specifying how the 29 unique types defined in the [Serde Data Model] are encoded into a serialized format. Additionally, I will need to define how any other postcard-specific behaviors, such as ["varint"]-style numbers, are defined to be serialized or deserialized.

Although users can always implement custom versions of `Serialize` or `Deserialize` in their data models and formats, implementors are still limited within the bounds of using the 29 possible types, based on the APIs of the `Serializer` and `Deserializer` types.

I don't plan to do anything particularly special for this, the specification will be captured in markdown, specifcally in an [mdBook]. Each unique element of the specification (or "requirement", using more formal terms) will have a unique and stable ID, allowing me to ensure that all requirements are implemented in the code, and covered by the regression test suite. This is a concept known as ["traceability"], in the safety-critical world. The specification will live in the main postcard repository, and will be published under the terms of the [CC-BY-SA 4.0 license].

[CC-BY-SA 4.0 license]: https://creativecommons.org/licenses/by-sa/4.0/

Since the scope here is relatively small, I plan to do this traceability review manually, but may use it as a reference example later, as I [have some thoughts] on how to build a requirements traceability tool for Rust. If that interests you (or your company), feel free to [send me an email]! I'd love to work on it, but it may not fit within this scope.

[mdBook]: https://github.com/rust-lang/mdBook
["traceability"]: https://en.wikipedia.org/wiki/Requirements_traceability
[have some thoughts]: https://twitter.com/bitshiftmask/status/1485748121644814337

### Testing the wire format

The plan for testing is fairly straightfoward: Make sure there is at least one test for every requirement in the wire specification. This will include writing unit and integration tests within Rust's built-in testing framework.

I'm likely to go above and beyond this minimum, particularly making sure that robustness cases are covered, and correct error codes are returned for specific incorrect serialization/deserialization behaviors.

### Address the `usize`/`isize` limitation

As of now (May 2022), the [Serde Data Model] does *not* have type definitions for Rust's `usize` or `isize` type, which are defined as [the size of a pointer], typically 32 bits on 32-bit machines (such as many microcontrollers), or 64 bits on 64-bit machines (such as most consumer PCs and servers).

[the size of a pointer]: https://doc.rust-lang.org/std/primitive.usize.html

Instead: on 32-bit machines, Serde serializes `usize` as a `u32`, and `isize` as an `i32`; and on 64-bit machine, Serde serializes `usize` as a `u64`, and `isize` as an `i64`. Unfortunately, it does this without providing this context to format libraries like `postcard`, which means `postcard` *can't* know the difference between "`u32` that's really a `usize`", and "just a `u32`".

Because of this limitation, if you use `usize` or `isize` today with postcard, and send data between a 32-bit and 64-bit machine, that data will always fail to be deserialized correctly.

Also, note that this DOESN'T apply to the `usize` used to encode the length of a slice, as this is already handled by encoding that data in a ["varint"] style format, which is portable across 32 and 64 bit machines (though deserialization will gracefully fail if sending a slice with more than u32::MAX items to a 32-bit system, but that isn't really an issue in practice).

I am not yet sure *exactly* how I will address this, but my current plan is to change the encoding format of all integers larger than 16-bits to a variable length encoding. The main potential downside to this approach is in serialization/deserialization speed. Right now these numbers are basically copied directly to/from the serialized data. Adding an encoding step could negatively impact performance, but if the impact is not major, this approach will be taken. In general, postcard prefers correctness to performance.

I am open to other suggestions on how to address this, prior to the 1.0 release.

### Fixing open defects

I'll be triaging and addressing any [open issues] on the postcard issue tracker. If you know of anything not listed there, please open an issue ASAP!

[open issues]: https://github.com/jamesmunns/postcard/issues

## The "Nice To Have" items

The following are items that have been on my to-do list for postcard for a while. I may not be able to handle all/any of them for the 1.0 release, but if I can, I will! If not, I'll do my best to make sure they can be done without a breaking change post-1.0.

### Removing "Flavors"

The ["Flavors"] API was intended to act as a way to introduce "middlewares" for postcard, to allow you to perform multiple steps while serializing or deserializing.

For example, typical serialization looks like this (Rust data in, Postcard format bytes out):

```
[Rust Data]
    -> [Postcard Format Bytes]
```

Flavors were intended to let you do multiple steps without allocating temporary buffers, allowing you to process serialized data as a stream.

This would allow you to do something like the following, getting serialized + CRC32 checksummed + COBS encoded data:

```
[Rust Data]
    -> [Postcard Format Bytes]
    -> [Postcard Format Bytes][ CRC32 Checksum ]
    -> [COBS Encoded Data w/ CRC32 Checksum    ]
```

Although this *does* work today, at least for Serialization, it has some pretty major limitations:

* It only works for serialization, I could never come up with a good API for "Deserialization Flavors"
* It leans *really* heavily on [generics and recursive types], for example the above would be something like `Cobs<Crc32<Slice>>`
* To my knowledge, no one has ever used the `Flavor` system, except for postcard itself, primarily for the `from_cobs` and `to_cobs` methods
* In general, I've found in practice (if you can spare the extra scratch space), actions like serializing + cobs encoding is actually *faster* when you do it in two steps, instead of both steps in a stream oriented manner. For deserialization of cobs, you need to buffer the whole message at once anyway to properly decode, which means doing the steps simultaneously doesn't get you any benefit!

I'll take a fresh look at it to see if there is a better approach, but generally I plan to remove flavors entirely.

[generics and recursive types]: https://github.com/jamesmunns/postcard/blob/3b3bfc7ba6c835f186c0e29b55256caf4e9f9db7/src/ser/mod.rs#L286-L297

### Looking at Variable Length Encoding

Right now I use a fairly straightforward "varint"/"leb" encoding technique in Postcard. Recently I've started using a technique similar to that used in [`vint64`], which doesn't require a loop to encode or decode, and should lead to smaller/more efficient code, especially on CPUs with a branch predictor (e.g. desktop/server/laptops), with a negligible difference for MCU systems that don't.

Additionally, if I start encoding signed types, like `i32` or `i64`, I will need to handle these efficiently, for example using ["zigzag encoding"].

["zigzag encoding"]: https://en.wikipedia.org/wiki/Variable-length_quantity#Zigzag_encoding

### Determine maximum message size

Since postcard often has a different "on the wire" size than "rust data in memory" size, it can be difficult to predict how much space is "enough" to hold a whole message. For certain types, like borrowed slices of bytes or strings, this number is actually unlimited, so the maximum size is unknowable.

However with a little bit of trait magic, and perhaps some explicit annotations in the case of borrowed types, it should be possible to calculate the largest possible size on the wire.

In fact, there is [already an open experimental PR](https://github.com/jamesmunns/postcard/pull/54) to add this to postcard! I hope to merge this in time for the 1.0 release.

### Emit a message schema

At the moment, there is little way to consume postcard messages outside of Rust, without using FFI to wrap the "first party" Rust code.

I hope to find some "easy" way to emit the schema for a given message. My two best guesses on how to do this would be:

* Provide some kind of method, like `postcard::encoding_of<MyFancyType>()`, which would collect and print the schema to a string
* Provide some kind of derive/procedural macro like `#[derive(PostcardSchema)]`, which could emit the schema to the build directory

Having easy access to this schema could aid with multiple things, including:

* Verifying Postcard itself (ensuring the types under test produce the right schema)
* Projects aiming to avoid changes to message protocols defined with postcard
* Projects looking to generate non-Rust code to serialize/deserialize postcard types

## Wrapping up

Whew! This was a lot of context and details!

Thanks again to everyone who has used postcard (288,087 downloads on crates.io, at the time of this writing!), and thanks again to Mozilla Corporation for sponsoring this work!

Feel free to [send me an email] if you have any questions.
