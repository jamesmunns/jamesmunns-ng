+++
title = "Raumfahrer Projekt - Day Zero"
date = 2018-02-18T12:00:00Z
draft = false
# tags = ["tag1", "tag2"]
# category = "rust"
aliases = []
in_search_index = true
template = "blog_post.html"
+++

Phew, it's been a busy six months or so since I've last posted. So busy, in fact, that I had two weeks of vacation left over from last year that I was able to roll over to this year, but it had to be used by the end of Q1.

Tomorrow (2018-02-19) kicks off my first day of vacation, and I wanted to share what I'm planning on doing for the next two weeks - something I'm calling **The Raumfahrer Projekt**.

<!-- more -->

# Okay, what is it?

The idea is to develop a portable, battery powered device to track people or objects as they move around inside of a room or building.

My design will be based primarily on a module called the [DWM1000](https://www.decawave.com/products/dwm1000-module), which is an Ultra Wide Band (3.5GHz to 6.5GHz) radio module capable of measuring distance between two units at an accuracy of around 10cm. It does this by sending a few pings back and forth between two or more of these radios, and measuring the time elapsed between these pings. Since radio waves propigate at the speed of light, it is possible to measure distance based on the round trip time of messages. In a later post, I'll go a bit more into how exactly this module does this.

I also plan to include a 3 dimensional accelerometer on the board itself, as well as a Cortex M4F processor, which should be capable of doing some [Kalman Filter](http://blog.tkjelectronics.dk/2012/09/a-practical-approach-to-kalman-filter-and-how-to-implement-it/) based [Sensor Fusion](https://en.wikipedia.org/wiki/Sensor_fusion) in order to make the tracking even more accurate.

Oh, and I plan to write the whole firmware in Rust, since I've been looking for a bare metal embedded project to apply some of the other [Embedded](https://github.com/jamesmunns/nrf52dk-sys) [Rust](https://github.com/jamesmunns/teensy3-rs) learning I've worked on in the past. I'm looking forward to incorporate some of the really awesome work [Japaric](http://blog.japaric.io/) has been doing lately with the [RTFM](https://github.com/japaric/cortex-m-rtfm) and [Embedded HAL](https://github.com/japaric/embedded-hal) components, and hopefully contribute back a bit.

# How much do I expect to get done?

Well, I don't expect to have a fully working everything, even with two weeks of full time effort. I'll be learning some new software tools, playing with new hardware, and making happy little mistakes along the way.

My primary goals for the next two weeks are:

* Build a set of prototyping boards capable of fully using the microcontroller, the radio, and maybe the accelerometer (two, so I can develop the ranging stuff)
* Have an inital working driver for the DW1000 radio, so I can add to it incrementally in my free time after these two weeks
* Design the first PCBs for test units, so I can send those off to be manufactured after I have validated the circuit
    * This includes brushing up on my PCB design and layout knowledge, which has been gathering dust for the past few years
* Learn a lot about the state of the art in Embedded Rust
* Document as much of my development and learning process as possible, in the form of blog posts, podcasts, and videos
* Contribute back to the open source projects I use as much as possible

# Wrapping up

Feel free to follow along [on Github](https://github.com/jamesmunns/raumfahrer), and ping me on [Twitter - @bitshiftmask](https://twitter.com/bitshiftmask). I'll also try to post here daily, and may even have some surprise content in the form of video or audio.
