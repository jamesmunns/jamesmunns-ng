+++
title = "Novation Launchpad Mk2 Rust API"
date = 2017-01-15T15:00:00+02:00
draft = false
# tags = ["tag1", "tag2"]
# category = "rust"
aliases = []
in_search_index = true
template = "blog_post.html"
+++

For Christmas, my lovely wife got me a Novation Launchpad Mk2. These are billed as the "iconic grid performance instrument", and some day I hope to actually make some music with it. Until then, its a really cool 9x9 button grid with RGB LEDs. Pefect for playing around with!
<br>
![Launchpad]({{ site.url }}/images/launchpadmk2.jpg "Launchpad")

Luckily for me, this thing is basically perfect for hacking on. It uses MIDI to read button presses and control the lighting, so there is already low level driver support for both OSX and Linux. On top of that, they [provide an API](https://global.novationmusic.com/sites/default/files/novation/downloads/10529/launchpad-mk2-programmers-reference-guide_0.pdf) (pdf) document showing you how to do everything!

I chose the [portmidi-rs](https://github.com/musitdev/portmidi-rs) bindings, because [PortMidi](http://portmedia.sourceforge.net/portmidi/) is multiplatform. Unfortunately, there was a missing library call I needed to send more complex commands, but no worries, after a quick [pull request](https://github.com/musitdev/portmidi-rs/pull/32), we were in business!

So far I've implemented a basic set of commands from the API document, as well as a demo that can be used to check that everything is working. So far I've tested it on OSX and Linux (x86 and on a Raspberry Pi).

Check it out on [Github](https://github.com/jamesmunns/launch-rs), read the [documentation](https://docs.rs/launchpad), or just watch the video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/-4uJweSSkmw" frameborder="0" allowfullscreen></iframe>

I have a few ideas on how to build on this, including:

* Some kind of Notification Board for things like public transit, weather
* Basic grid based boards, such as:
    * Game of Life
    * Battleship
    * Minesweeper

If you have a launchpad, and would like to contribute, please feel free to get in touch!
