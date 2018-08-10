+++
title = "Working on the Embedded Rust Book"
date = 2018-08-04
draft = false
in_search_index = true
template = "blog_post.html"
+++

**TL;DR:** Up to now, I haven't had as much time or motivation as I would have like to contribute to the Embedded Rust Book. However, I am excited to see the initial version of the book launch with the 2018 edition of Rust (which will ship with stable support for embedded)!, so I will be committing to write one chapter per two weeks, until the end of the year.

Read below for my plan, and how you can help!

<!-- more -->
<hr>

So, in general, we have around 18 weeks until the release of Rust 2018 (which is December 6th, Calendar Week 49), and currently there are 9 chapters defined in our [coordination issue]

[coordination issue]: https://github.com/rust-lang-nursery/embedded-wg/issues/115

This gives me about two weeks per chapter to write, have it reviewed, make any corrections necessary. Hopefully, as momentum starts, more people will be able to join in and help with contributions.

At the moment, I am close to landing the [introduction chapter], so hopefully I can use that "extra" two weeks as a bit of a buffer time in case new sections come up.

[introduction chapter]: https://github.com/rust-lang-nursery/embedded-wg/pull/133

I don't necessarily plan to work on this in order, and the first two sections I would like to tackle are `static guarantees`, as this is more or less the content of my upcoming [RustConf talk], and `interoperability` between Rust and C/C++ (in an embedded context), as I have some experience with this through my previous work with the [teensy3] and the [nrf52dk].

[RustConf talk]: http://rustconf.com/program.html#somethingfornothing
[teensy3]: https://github.com/jamesmunns/teensy3-rs
[nrf52dk]: https://github.com/jamesmunns/nrf52dk-sys

If you're interesting in helping, check in on the [coordination issue], and I'd be happy to have your help!
