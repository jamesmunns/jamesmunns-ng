+++
title = "Interfacing with Rust - Playing nice with others"
date = 2016-08-04T13:00:00+02:00
draft = false
# tags = ["tag1", "tag2"]
# category = "rust"
aliases = ["update/2016/08/04/interfacing-with-rust.html"]
in_search_index = true
template = "blog_post.html"
+++

One of my goals for this month is working in rust every day. One thing that I am interested in is getting Rust talking with other languages. Having this knowledge will help me interface with existing libraries, rewrite tools in Rust, and hopefully learn a little along the way.

<!-- more -->

So far I have the following goals, in no particular order:

- C calling Rust (statically linked)
- Rust calling C (statically linked)
- C calling Rust (dynamically linked)
- Rust calling C (dynamically linked)
- Python calling Rust (dynamically linked)

None of this is particularly new, and there are lots of guides out there for how to do this, however I wanted to document my learning process.

You can track my progress (now and later) on my GitHub repo [here](https://github.com/jamesmunns/rust-linking)
