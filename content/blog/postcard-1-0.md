+++
title = "Postcard 1.0.0 Release"
date = 2022-06-21
draft = false
in_search_index = true
template = "blog_post.html"
+++

Quoting from the README:

> Postcard is a #![no_std] focused serializer and deserializer for Serde. Postcard aims to be convenient for developers in constrained environments, while allowing for flexibility to customize behavior as needed.

I first published [`postcard`] back in 2019, as a way to get "all the good stuff from [Serde]" in a format that would work for embedded systems. Since then, people all over Rust are using Postcard as a general purpose, [compact], and flexible Serde format, not just embedded folks! Now, 3 years later or so, **it has reached 1.0.0**!

As of yesterday, June 20th, [`postcard`] v1.0.0 has been released.

This blog post is an extended overview of the changes since the last stable release, v0.7.3.

This work was made possible thanks to [sponsorship] from the [Mozilla Corporation], and I'd like to thank them again for their support!

[sponsorship]: https://jamesmunns.com/blog/postcard-1-0-run/#sponsorship
[Mozilla Corporation]: https://www.mozilla.org
[Serde]: https://serde.rs
[`postcard`]: https://docs.rs/postcard
[compact]: https://github.com/djkoloski/rust_serialization_benchmark

<!-- more -->

## `varint` all the things!

The largest user-visible change is that more integers are now variably encoded on the wire.

### Background

Previously, only [enum discriminants] and the length of slices were variably encoded.
This was typically an "easy win" for enums as it is rare to have enums with more than 127 variants,
which meant saving three bytes per enum on the wire.
Additionally it was generally a positive for slices, as it is also rare to send slices with counts close to
the max `usize` amount.
All other integers were sent as an array of little-endian bytes, basically what you'd get if you called
the `.to_le_bytes()` function on that integer.

However, there was a subtle compatibility issue here: `serde` doesn't actually have a wire type for `usize` or `isize`.
This means when you serialize a `usize` on a 64-bit platform, it is eight bytes on the wire.
When you serialize a `usize` on a 32-bit platform, it is four bytes on the wire.

Since [`postcard`] is designed to facilitate communication between dissimilar systems, especially embedded
systems and desktops/servers, this was a real problem!

[enum discriminants]: https://doc.rust-lang.org/std/mem/fn.discriminant.html

### The actual change

In order to resolve this, postcard now encodes ALL integers larger than one byte as a variable length integer.
Enum discriminants and slice lengths are still encoded as variable length integers.
This includes `u16`, `u32`, `u64`, `u128`, `i16`, `i32`, `i64`, and `i128`.
Now, we still encode `varint(usize)` as a `varint(u32)` on a 32-bit platform, but with variable length encoding,
we can also now detect when a "larger system" is sending too big of a number to a "smaller" system.
This detection now correctly leads to a reported error while decoding.

As a specific example, here's how some `u32`s would be encoded in postcard 0.7 and 1.0:

| Number        | Hex           | Postcard 0.7                  | Postcard 1.0                      |
| ---:          | :---:         | :---:                         | :---:                             |
| 64            | `0x0000_0040` | `[0x40, 0x00, 0x00, 0x00]`    | `[0x40]`                          |
| 69420         | `0x0001_0f2c` | `[0x2C, 0x0F, 0x01, 0x00]`    | `[0xAC, 0x9E, 0x04]`              |
| 2000000000    | `0x7735_9400` | `[0x00, 0x94, 0x35, 0x77]`    | `[0x80, 0xA8, 0xD6, 0xB9, 0x07]`  |

In *most* cases (whenever your number is not at the very top of the integer range), this will translate
to either a reduction or neutral change in wire size. Performance impact has been measured and is minimal
(+/- single digit percentages in benchmarks) due to the simple nature of the encoding and decoding scheme.

More details on the encoding scheme and additional examples are provided in the [Unsigned Integer Encoding]
section of the format specification.

[Unsigned Integer Encoding]: https://postcard.jamesmunns.com/wire-format.html#unsigned-integer-encoding

### Zigzag Encoding

One issue with this encoding scheme is that two's compliment signed numbers use the **most** significant bit to store the sign.
This means that a small negative number like `-1_i32` would be encoded as `0xFFFF_FFFF`, the WORST case for this encoding scheme!

To address this, signed integers are first [Zigzag encoded], then encoded with variable length.
Zigzag encoding stores the sign bit in the LEAST significant bit of the integer, rather than the MOST significant bit.
This means that signed integers of low absolute magnitude (e.g. 1, -1) can be encoded using a much smaller space.

For example, the following 16-bit signed numbers would be encoded as follows:

| Dec       | Hex\*     | Zigzag (hex)      |
| ---:      | :---      | :---              |
| 0         | `0x00_00` | `0x00_00`         |
| -1        | `0xFF_FF` | `0x00_01`         |
| 1         | `0x00_01` | `0x00_02`         |
| 63        | `0x00_3F` | `0x00_7E`         |
| -64       | `0xFF_C0` | `0x00_7F`         |
| 64        | `0x00_40` | `0x00_80`         |
| -65       | `0xFF_BF` | `0x00_81`         |
| 32767     | `0x7F_FF` | `0xFF_FE`         |
| -32768    | `0x80_00` | `0xFF_FF`         |

`*`: This column is represented as a sixteen bit, two's compliment form

Comparing Postcard 0.7 to 1.0:

| Dec       | Postcard 0.7      | Postcard 1.0          |
| ---:      | :---:             | :---:                 |
| 0         | `[0x00, 0x00]`    | `[0x00]`              |
| -1        | `[0xFF, 0xFF]`    | `[0x01]`              |
| 1         | `[0x01, 0x00]`    | `[0x02]`              |
| 63        | `[0x3F, 0x00]`    | `[0x7E]`              |
| -64       | `[0xC0, 0xFF]`    | `[0x7F]`              |
| 64        | `[0x40, 0x00]`    | `[0x80, 0x01]`        |
| -65       | `[0xBF, 0xFF]`    | `[0x81, 0x01]`        |
| 32767     | `[0xFF, 0x7F]`    | `[0xFF, 0xFF, 0x02]`  |
| -32768    | `[0x80, 0x00]`    | `[0xFF, 0xFF, 0x03]`  |

[Zigzag encoded]: https://en.wikipedia.org/wiki/Variable-length_quantity#Zigzag_encoding

More details on the encoding scheme and additional examples are provided in the [Signed Integer Encoding]
section of the format specification.

[Signed Integer Encoding]: https://postcard.jamesmunns.com/wire-format.html#signed-integer-encoding

### An escape hatch

In some cases, it is not desirable to always use variable length encoded data. In particular, I've had reports from
users that have serialized 16-bit floating point numbers (`fp16`) as `u16`s, which often hit the "worst case" encoding
size, increasing their message sizes by 50%.

Additionally, although postcard has always encoded data in little-endian format, some users have asked for the ability
to encode big-endian data, often for zero-copy purposes or compatibility with other message formats.

For this reason, [`postcard`] has added a pair of convenience wrapper types, `FixintLE<T>` and `FixintBE<T>`, which
do not use the encoding schemes described above, and are provided for all 16-128 bit integer types.

As a specific example, here's how some `u32`s would be encoded using these types:

| Number        | Hex           | `FixintLE<u32>`               | `FixintBE<u32>`            |
| ---:          | :---:         | :---:                         | :---:                      |
| 64            | `0x0000_0040` | `[0x40, 0x00, 0x00, 0x00]`    | `[0x00, 0x00, 0x00, 0x40]` |
| 69420         | `0x0001_0f2c` | `[0x2C, 0x0F, 0x01, 0x00]`    | `[0x00, 0x01, 0x0F, 0x2C]` |
| 2000000000    | `0x7735_9400` | `[0x00, 0x94, 0x35, 0x77]`    | `[0x77, 0x35, 0x94, 0x00]` |

As a note, these were (accidentally) not included in the postcard 1.0.0 release, but will be released shortly
as part of postcard v1.0.1.

Additionally, as `postcard` is "just another" serde backend, it is always possible to override the default serialization
and deserialization methods for your types if you find that the default options do not suit you well. Under the hood, these
types just implement the `Serialize` and `Deserialize` traits manually as such:

```rust
impl Serialize for FixintLE<u32> {
    #[inline]
    fn serialize<S>(&self, serializer: S) -> Result<S::Ok, S::Error>
    where
        S: Serializer,
    {
        self.0.to_le_bytes().serialize(serializer)
    }
}

impl<'de> Deserialize<'de> for FixintLE<u32> {
    #[inline]
    fn deserialize<D>(deserializer: D) -> Result<Self, D::Error>
    where
        D: serde::Deserializer<'de>,
    {
        <_ as Deserialize>::deserialize(deserializer)
            .map(u32::from_le_bytes)
            .map(Self)
    }
}
```

## A written and stable wire specification

Although postcard's wire format has rarely changed over the years, it has never officially had a "stable" wire format.
This has led to some questions, particularly for folks interested in using it more formally, or looking to write protocol
implementations in other languages.

Postcard now has a documented and tested wire specification, located in the [in the repository], and in a [hosted format].

This specification is available under a [CC-BY-SA 4.0 license], and is written in markdown using [mdBook].

The specification includes two main parts:

* An [elaborated definition] of the upstream [Serde Data Model], which describes the fundamental types that can be serialized or deserialized.
* The [Postcard Wire Format], which describes how each type is encoded to the wire, or decoded from the wire.

Starting with postcard 1.0.0, breaking changes to the wire format are also considered breaking changes to the library,
and will require a version bump to postcard 2.0.0.

[in the repository]: https://github.com/jamesmunns/postcard/tree/main/spec
[hosted format]: https://postcard.jamesmunns.com
[CC-BY-SA 4.0 license]: https://github.com/jamesmunns/postcard/blob/08e38e65567028b7328c685ecf38005f1a84b614/spec/LICENSE-CC-BY-SA
[mdBook]: https://github.com/rust-lang/mdBook
[elaborated definition]: https://postcard.jamesmunns.com/serde-data-model.html
[Serde Data Model]: https://serde.rs/data-model.html
[Postcard Wire Format]: https://postcard.jamesmunns.com/wire-format.html

## Revamped "Flavors"

Postcard has had a concepts of "flavors", which acted as "middlewares" for the serialization process. This enabled
certain functionality, such as encoding the serialized data using the [COBS encoding scheme], as the data was serialized.

This was convenient, as multiple steps could be done during serialization, without requiring additional temporary buffers.

However, I had not previously been able to find a good way to bring this functionality to the deserialization side.

Luckily, with spending time on the Postcard interface during the 1.0 release process, I was able to find one!
As of postcard 1.0, postcard now supports both [Serialization Flavors] as well as [Deserialization Flavors].

There are some trade-offs for using flavors when compared to doing each step of the process (generally a speed
vs memory usage trade-off), so make sure you take a look at the docs if you have questions!

[COBS encoding scheme]: https://en.wikipedia.org/wiki/Consistent_Overhead_Byte_Stuffing
[Serialization Flavors]: https://docs.rs/postcard/latest/postcard/ser_flavors/index.html
[Deserialization Flavors]: https://docs.rs/postcard/latest/postcard/de_flavors/index.html

## Updated `cobs`

Historically, [`postcard`] has used a fork of the `cobs` crate, due to some necessary features
that had not been merged upstream.
A few months ago, I took over maintenance of the `cobs` crate, and have [released a few] `v0.2.x`
versions that have integrated the changes that `postcard` needed, which means the forked
`postcard-cobs` crate is no longer necessary!

There are generally no functional changes from a `postcard` perspective, however a few functions are
now more robust (they do not panic when handed unexpected or malformed data), and the
[`take_from_bytes_cobs`] function, which was [generally incorrect] has been fixed.

Thanks to [Allen Welkie] for sharing the `cobs` crate with me!

[released a few]: https://crates.io/crates/cobs
[`take_from_bytes_cobs`]: https://docs.rs/postcard/latest/postcard/fn.take_from_bytes_cobs.html
[generally incorrect]: https://github.com/jamesmunns/postcard/issues/50#issuecomment-1155759142
[Allen Welkie]: https://github.com/awelkie/

## Get back `#[inline]`!

While validating performance, I noticed that I was missing `#[inline]` attributes on most serialization
and deserialization functions, which means that without LTO, it would not be possible to inline these
often very small functions. This is particularly important, as they are called by serde functions,
greatly increasing the overhead.

In benchmarks, this **significantly** increased the serialization performance by up to 5x,
and deserialization performance by up to 2x. There was a slight improvement in builds that already
used LTO (common in embedded builds), but far less dramatic.

Note, that these are NOT `#[inline(always)]` markers, which means that the compiler will still make inlining
decisions based on its own heuristics. This means in typical release builds, which are `opt-level = 3`, some
increase in code size is expected. However, when changing the optimization level to `opt-level = 's'`, the code
returns to typical sizes seen in postcard v0.7.

## Experimental Features

Finally, thanks to the efforts of [Lachlan S.], this release also included two [experimental features]:

The first is a [`MaxSize`] derive macro and trait, which allows for automatically calculating the maximum
serialized size of a postcard message. This was an often asked for feature, especially in embedded use
cases where it is important to have suitably sized serialization and deserialization buffers.

The second is a [`Schema`] derive macro and trait, which renders a description of the schema of
the message, including all data contained by any given type. This is intended to be used for two
main purposes: producing a human readable format, suitable for inclusion in documentation, and
producing a machine readable format (such as JSON), which can be used to generate serialization,
deserialization, or parsing code, in order to better support other languages and verification
efforts.

These features are behind the `experimental-derive` feature, and do NOT yet have stability guarantees
behind them. That being said, I expect them to land in the next releases of postcard with only minor
improvements and tweaks. Give them a try, and let me know what you think!

[Lachlan S.]: https://github.com/lachlansneff/
[experimental features]: https://docs.rs/postcard/latest/postcard/experimental/index.html
[`MaxSize`]: https://docs.rs/postcard/latest/postcard/experimental/max_size/index.html
[`Schema`]: https://docs.rs/postcard/latest/postcard/experimental/schema/index.html

## Wrapping up

Thank you all for using postcard over the years! It started as a way for me to learn and scratch my
own itches, and it has been great to hear how it has helped others now too.

Enjoy the release!

🍾
