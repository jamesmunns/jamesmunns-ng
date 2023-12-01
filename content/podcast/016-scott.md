+++
title = "016 - Scott Mabin"
date = 2023-12-01T11:00:00+02:00
draft = false
in_search_index = true
template = "podcast_post.html"
+++

James talks with Scott Mabin about how he joined the Espressif team and got involved in embedded Rust, the working culture in chip manufacturing companies and preferences about designing and building mechanical keyboards. 

This episode was recorded on November 8th, 2023. 

<!-- more -->

## Audio

### FLAC

<audio
    controls
    src="https://delivery.jamescdn.com/2023-12-01-scott-mabin.flac">
        Your browser does not support embedding FLAC.
</audio>

[Download as FLAC](https://delivery.jamescdn.com/2023-12-01-scott-mabin.flac)

### M4A

<audio
    controls
    src="https://delivery.jamescdn.com/2023-12-01-scott-mabin.m4a">
        Your browser does not support embedding M4A.
</audio>

[Download as M4A](https://delivery.jamescdn.com/2023-12-01-scott-mabin.m4a)

### MP3

<audio
    controls
    src="https://delivery.jamescdn.com/2023-12-01-scott-mabin.mp3">
        Your browser does not support embedding MP3.
</audio>

[Download as MP3](https://delivery.jamescdn.com/2023-12-01-scott-mabin.mp3)

## Show Notes

- Scott Mabin [website](https://mabez.dev/), [Github](https://github.com/mabezdev)
    - [Blog post “Rust on Espressif chips](https://mabez.dev/blog/posts/esp-rust-espressif/)
    - [Espressif](https://www.espressif.com/en) and on [Github](https://github.com/espressif)
    - Jesse Braham [(jessebraham)](https://github.com/jessebraham) & Ivan Grokhotkov [(igrr)](https://github.com/igrr)
    - [ESP8266](https://en.wikipedia.org/wiki/ESP8266) and on the [Arduino ecosystem](https://arduino-esp8266.readthedocs.io/en/latest/esp8266wifi/readme.html)
    - Xtensa architecture [from Cadence](https://www.cadence.com/en_US/home/tools/ip/tensilica-ip/tensilica-xtensa-controllers-and-extensible-processors.html)
- The path to the job at Espressif
    - Jorge Aparicio [(japaric)](https://github.com/japaric) at [Ferrous](https://ferrous-systems.com/) blog post about [Rust your ARM microcontroller!](https://blog.japaric.io/quickstart/)
    - Smart watch [final project](https://github.com/MWatch/kernel) (from 5 years ago)
    - Jonathan Pallant [theJPster](https://github.com/thejpster), [Monotron](https://github.com/thejpster/monotron)
    - [`mrustc`](https://github.com/thepowersgang/mrustc)
- CPU architectures and [LLVM](https://llvm.org/) backend support
    - [ARM Cortex-M](https://en.wikipedia.org/wiki/ARM_Cortex-M) family microcontrollers
    - [Cadence Tensilica](https://www.cadence.com/en_US/home/tools/ip/tensilica-ip/technologies.html), Tensilica cores: [LX6](https://mirrobo.ru/wp-content/uploads/2016/11/Cadence_Tensillica_Xtensa_LX6_ds.pdf) and [LX7](https://www.cadence.com/content/dam/cadence-www/global/en_US/documents/tools/ip/tensilica-ip/tip-xtensa-lx-pb.pdf)
    - [Clang](https://clang.llvm.org/), [AVR](https://en.wikipedia.org/wiki/AVR_microcontrollers#:~:text=The%20AVR%20is%20a%20modified,program%20memory%20using%20special%20instructions.)
    - [esp-rs](https://github.com/esp-rs)
    - [Teensy](https://www.pjrc.com/teensy/) microcontroller development system
    - Foreign function interface [(FFI) calls](https://en.wikipedia.org/wiki/Foreign_function_interface)
    - [Zinc project](https://github.com/hackndev/zinc) (archived)
    - [ESP-IDF](https://www.espressif.com/en/products/sdks/esp-idf), [FreeRTOS](https://www.freertos.org/index.html)
    - [POSIX](https://en.wikipedia.org/wiki/POSIX) compatibility layer
- How to go from embedded → Rust → embedded Rust
    - [Arduino](https://www.arduino.cc/), [Circuit Python](https://circuitpython.org/)
    - [ESP32 HAL](https://github.com/esp-rs/esp32-hal) (archived)
    - Mabez blog posts getting debugging set up: [Rust on the ESP32](https://mabez.dev/blog/posts/esp32-rust/) and [Rust on the ESP32 - SVD’s, PAC’s and USB flashing](https://mabez.dev/blog/posts/esp32-rust-svd-pac/) 
    - [idf2svd](https://github.com/MabezDev/idf2svd) repository (archived)
    - [Arjan Mels](https://github.com/arjanmels)
    - Mabez blog post [Rust on the ESP32 & ESP8266 - Building an ecosystem](https://mabez.dev/blog/posts/esp-rust-ecosystem/)
    - [STM-RS](https://github.com/stm32-rs/stm32-rs) , [STM32F(2)](https://www.st.com/en/microcontrollers-microprocessors/stm32f2-series.html)
- Fresh ideas from new hires, working at a chip manufacturer vs being a consumer
    - [Zephyr project](https://github.com/zephyrproject-rtos/zephyr) [Zephyr from Nordic](https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/zephyr/index.html)
    - [Broadcom](https://www.broadcom.com/)
    - Dario Nieuwenhuis [(dirbaio)](https://github.com/Dirbaio) from [Embassy](https://github.com/embassy-rs/embassy)
    - Rust community on Espressif: [MabezDev](https://github.com/MabezDev) / [jessebraham](https://github.com/jessebraham) / Björn Quentin [(bjoernQ)](https://github.com/bjoernQ) 
- Hobby project : mechanical keyboard
    - [ESP32-S3](https://www.espressif.com/en/products/socs/esp32-s3)
    - [Tenkeyless keyboard](https://www.daskeyboard.com/blog/what-is-tkl-keyboard/)
    - [nRF52](https://www.nordicsemi.com/Products/Development-hardware/nrf52-dk)
    - Keyberon on [GitHub](https://github.com/TeXitoi/keyberon) or [docs.rs](https://docs.rs/keyberon/latest/keyberon/)
    - [KVM switch](https://en.wikipedia.org/wiki/KVM_switch) and MabezDev tool [M27 KVM switch control](https://github.com/MabezDev/m27q-kvm) 
    - [Multi-platform Tray Indicator (tray-item-rs)](https://github.com/olback/tray-item-rs)
    - [Milky yellow switch](https://www.gateron.co/products/gateron-ks-3-milky-pro-switch-set) vs. [linear red switches](https://www.youtube.com/watch?v=wnDfpSZojts), [Kailh Choc switches](https://www.kailh.net/products/kailh-choc-v2-low-profile-switch-set?_pos=1&_sid=064325642&_ss=r)
    - [Switch types](https://www.mechanical-keyboard.org/switch-types/) and [keyboard switch chart](https://thegamingsetup.com/gaming-keyboard/buying-guides/keyboard-switch-chart-table)
- Designing engineering hardware
    - [EAGLE](https://en.wikipedia.org/wiki/EAGLE_(program)) for electronics design and [KiCad EDA](https://www.kicad.org/)
    - [Adafruit](https://www.adafruit.com/) and [AliExpress](https://www.aliexpress.com/)
    - [JLCPCB](https://jlcpcb.com/easyeda) and [EasyEDA](https://easyeda.com/)
- Goodbye
    - [Scott Mabin Blog](https://mabez.dev/blog/posts/) and [@mabezzzzz on X](https://twitter.com/mabezzzzz)

## Transcript

<details> 

*James Munns*

I've recorded a couple of these. It's been a while and Amanda's actually been helping me go back and go through the edits because I've been pretty bad… I love talking to people and so I'll record these and I've- I have a bunch that just haven't been released and then the editing and then like filling out the show notes and stuff like that has always been the- the challenging thing, so…

*Scott Mabin*

That's yeah, that's the boring part isn't?

*James Munns* 

It's- boring's probably not the right word, but tedious certainly and my brain is weirdly bad at tedious. But I'm trying to think… I went back and I hadn't- I actually didn't look at the date; I meant to go back and look at the date to figure out when, because I knew like the way that I found out that you worked at Espressif now was from the blog post you wrote a while back where where you went from like very community type work to going, “Oops, they hired me!” or not “Oops,” but, “Hooray! They've hired me!” When was that?

*Scott Mabin* 

2021, I believe.

*James Munns*

Okay, so we're coming up- or maybe more than 2 years now?

*Scott Mabin*

Yes, more than 2 years I joined- well, my start date was August the 1st in 2021, so just over 2 years now.

*James Munns*

Very cool. So before we get too far, do you want to give yourself a quick introduction?

*Scott Mabin*

Sure, so my name's Scott Mabin. I'm a software engineer. I've got 5 years professional experience with Rust, and I currently work on the Rust Language Enablement Team at Espressif.

*James Munns*

Very cool. It's been interesting to see because it's probably from learning through your blog posts and talking to you or Jesse or someone else. It's been interesting to, now in retrospect- so I've been aware of Espressif for a very long time, like I think one of my older IoT jobs where we were using the 8266 as a Wi-Fi radio and had some problems with some of the quality of hardware that we were purchasing — not necessarily Espressif’s fault — but learning about them and then seeing sort of that community grow from the outside very quickly where it was — well, this is this very cheap Wi-Fi module. Now they're part of the sort of Arduino ecosystem, where now more and more people are starting to use it, but they're still using it as like a- an external device. It's still just a radio.

*Scott Mabin*

Yep.

*James Munns*

To then people going, “Well, I can run code on this,” and then getting that working, and then seeing sort of a- ah huge proliferation of both, like, hobbyist-embedded-maker-type projects, but then also seeing ESP devices showing up everywhere and then having ESP sort of show up in the Rust world where it went from people going, “Well, can you support this?” and we went, “Well no, that's the Xtensa architecture and there's no LLVM backend for that, so there's not much to be done there…”  and then seeing I believe you started this as mostly a hobby or like open source project.

*Scott Mabin*

Yeah.

*James Munns*

And then some others being hired there, and then Espressif being sort of the first loudest direct contributor to Rust from the Silicon vendor perspective that I've seen. When I was working at Ferrous, my goal was always to try and get someone to be the first. And I think Espressif totally surprised me, because it wasn't anything that I was working on, or the people that I had been pinging or trying to get to support and things like that, and it seems like that's sort of the direction that they've they've always taken where I learned a little bit more about the software folks like Ivan, being hired sort of in the same way. That he was working on one of those other projects that I was talking about, like the Arduino support and people working for it, and it seems like Espressif has a surprisingly good culture around, “Hey, someone's building something cool with our stuff. Let's hire them so that more people can do cool stuff with our stuff.”

*Scott Mabin*

Yeah, exactly. I think you've hit the nail on the head there with what's so great about Espressif: is that I think they had some, I guess good attitudes towards the open source community and- and makers essentially, because there's a lot of silicon vendors around and not everyone has access to actually being able to use them. A lot of them are just, you know, they just have business-to business models. They strictly sell to people who buy the licenses and things like that. Espressif took a completely different approach, and I think that's one that's worked out very well for them, is that they essentially open source 99% of everything they do and try and involve the community where possible and that involves hiring from the community. As well when they when they find people doing great work with their chips, that they like to hire them and that's how I got my job.

*James Munns*

So what was the project that sort of led up to that? So I had certainly seen some of your blog posts and your work on it, and then sort of silence and then surprise hiring. I'm interested to hear sort of like: Where did you come into Rust, and then how did that become Rust on Espressif, and then how did that become your job?

*Scott Mabin*

Yeah. So this actually started when I was back at university— in the UK,  I don't know if there's similar things, there's probably similar things, but you have the option to do a light year in the industry, in between your second and final year. I was working at an embedded company doing embedded C, suffering slightly as a- as a junior who, you know, was tripping over various memory issues. I think yeah, one day I saw on on Reddit a blog post about Rust— not embedded, but just Rust in general, I was like, “Wow, this is kind of incredible. Why is no one talking about this?” So I sort of back-burnered it for a little bit, and then I think… I forget his handle now… japaric?

*James Munns*

Yeah, Jorge.

*Scott Mabin*

Yeah that's it. I think he posted a blog post about Rust on an STM32 I think- I think an F1 board if I remember correctly, and at my placement year job we were using a F2 board and then that's all got the cogs wearing like, “Oh… I wonder… I wonder how doable this would be?” I ended up finishing that year in the industry without actually writing any Rust. But I started learning Rust on the side during my final year, and in my final year we had like a final year project which was worth like 40% of the grade, and I actually chose to do that in Rust, and I chose to do embedded as well. So I made a very- I mean, by today's standards, it's not a smart watch but it was it- it did more than tell the time, basically. 

*James Munns*

Very cool.

*Scott Mabin*

You could actually load some apps on there. So Jonathan from Ferrous Systems, he was working on Monotron at the time and I base my application framework around what he was doing there, so that was really useful. But I basically spent a year learning Rust from embedded, and I can't say I recommend doing that… like, learning Rust is a challenge on its own, and then being constrained by what you're running it on and tool chains and things like that is… a different kettle of fish, but I guess with the deadline that I had set it sort of forced me to do it, so ended up managing to do it. And that project turned out really well, I was really happy with that. When I look back at the Rust code now, I'm not so happy about it, but I think it's just… It's- it's been four or five years…

*James Munns*

It means you've grown. 

*Scott Mabin*

no yeah exactly exactly.

*James Munns*

That's a good signal. If- if you're looking back at your old code and going, “This is the same or better than what I'm doing now,” then that's not a good sign. But if- if you look back and go, “I have learned so much in the last four or five years,” that's always a positive thing. And it's interesting, because I totally remember that project and I hadn't tied that to your name because… I've hung out in the chat rooms or IRC and then Matrix, doing blog posts and running the Twitter for so long, that like I remember so many of these projects and it's so interesting to realize like three years later that that's the same person that I talked to for a lot about that, and- and putting sort of like that historical context to names of people that I talk to decently regularly now.

*Scott Mabin*

Yeah, yeah, that's really cool. So at this point I had graduated… and I've always been interested in embedded systems. It's sort of like my grandfather was a electronic engineer. So I always used to mess around with stuff that he had on his desk so it always interested me. But at this point, I had some ESP32s laying around and obviously I was on a very heavy Rust hype. At this point, I'd seen the power of Rust and didn't want to go back to using C, so I started looking into seeing if it was possible. Obviously I then realized it was the Xtensa architecture. I did have an idea of using — and this is so cursed, I'm glad I never did it — but using `mrustc` to compile Rust and then using the gcc Xtensa toolchain to compile that C to a binary, but I'm glad I didn't have time to do that, because I think if I started looking at that I would have lost my mind, that just sounds like a recipe for hell.

*James Munns*

So for like, some context for people who aren't in this: so there's a bunch of different CPU architectures that are used for microcontrollers and things like that, and today the most common one is ARM, like the Cortex-M family of chips which has become sort of like the default choice for at least the last couple years and probably for the next couple years.  The Xtensa architecture comes from some company that makes IP blocks for hardware and things like that… I can't remember the name of the company, you might know them off top of your head… 

*Scott Mabin*

Uh… Cadence? Or Tensilica? Yeah, yeah.

*James Munns*

Cadence. Yeah it- Tensilica exactly, where they’re a company who designs CPU cores actually a lot like ARM, and licenses them. But these Cadence cores tend to show up in like, chips that you don't realize have a CPU in them but they totally do because they're doing DSP or they're doing things like that. I see these, like the LX6 and the LX7 are specific cores from Tensilica and I see them all the time in other chips as DSP co-processors for these chips, because it's something that when people are making a desktop chip that has to do audio processing like for an Alexa or something like that, if they want to continuously do DSP for audio and they want to have sort of a dedicated chip that's just picking up words or phrases and things like that and… so you see a lot of these chips but you don't really see them sold directly as chips and I think Espressif is one of the few that did do that where were more or less — I'm sure there's a lot of design and engineering that went into all the other stuff, because a CPU is just a CPU. But it was probably one of the most direct uses of those CPU- or at least most public, where they go, “Yes, it *is* this CPU,” and you don't just find that out after you've signed the NDA and gotten like some SDK where it's like, “Ah *that's* what this really is,” but I think the downside of it being sort of a more hidden or behind the scenes sort of CPU architecture is: it wasn't supported by LLVM, so like the sort of the basis Rust is built on, and that's a huge challenge because like you said, if- if you were just writing C, you couldn't use Clang to compile C code on to the ESP32 if LLVM doesn't know how to spit out code for that architecture. We've had this with like AVR and Xtensa and a couple of other like safety critical architectures where they're widely used in a niche but LLVM is sort of an open source project. If no one's needed that and added that support, then it just doesn't exist and that's sort of how things go where they've always had that gcc toolchain but also, Rust… well, now it's sort of supporting gcc, but at least at the time, when we're talking about two or three years ago, that was more conversation than than reality and…

*Scott Mabin*

Definitely…

*James Munns*

And that’s one of those hard things where you go, “It's so close… but I can't make them go together.” But that's one of those interesting things, where it felt like that was just… we got to the point where we go, “Yeah, it's just not going to happen…” like, maybe it could happen if someone does a whole lot of work, but I don't- I don't know who would *do* that work? Like… when would that actually happen? And then- and then Espressif did that, where they internally, and working with some other folks, added an LLVM backend for the Xtensa architecture. Then all of a sudden, Rust's just— well I say ‘just worked,’ I'm sure it was a ton of work from you and other folks— but from the outside appearance it went, “Oh no, you can just do that now.”

*Scott Mabin*

Yep. Yeah, I was extremely pleased when I saw the announcement that they were working on LLVM backend. I'd sort of- I mean you mentioned earlier there was a gap in talking about like the esp-rs stuff is basically because I was stuck. It was either use `mrustc` in that cursed setup or there's no other option. So I was really happy when they announced that, so I think that weekend I'd started trying to use this Xtensa-enabled LLVM with `rustc`. It was an experience. So I'd never touched any `rustc` internals before- before that point, let alone the code gen side of things, which starts interacting with like things like that which is um… interesting, but it actually wasn't that many changes. I fortunately found I think there was a patch set adding the RISC-V backend in upstream Rust, maybe like a year before, and I essentially looked at that and it was mostly the same. There was a few other things that I missed. But um… I got there eventually, so I was able to initialize the Xtensa LLVM backend within Rust, but the first version of the LLVM backend was tricky to use to say the least, so it didn't support any debug info. It also used an external assembler at this point so it was quite awkward to use. Firstly, trying to do bare metal programming with no debug symbols, no way to debug anything on an architecture that you don't know because nothing's public is a extremely challenging task. But after enough… I'll call it grunt work because it was just trial and error essentially, I did actually get it to do a simple blinky application— and I say it was in Rust, I mean it was literally just pure register rights, but the file extension was `.rs`, and it was compiled by `rustc`, so I'm claiming that. 

*James Munns*

I mean my first project was was figuring out how to take the Arduino libraries for I think the Teensy? And so, compiling that as sort of the hardware abstraction layer and just getting Rust to the point where it could make, like you said, those FFI calls— I guess for you is raw register rights, but for for me it was FFI calls— where I could call the set GPIO high or low functions and and get it to work and like you said it at that point it was, “Ah, we have implicated Rust in this project,” more than being a project *in* Rust, it was more a project that was implicated in that. But at the time, that was- there hadn't been that many people who had done that. This was maybe around the time where the Zinc.rs project was going on? This is like 2016, 2017 maybe, where it was like, some people had done it… I think Jorge was already- Jorge at the time was a compiler contributor, like he hadn't been working on embedded stuff specifically. He had just been working on the compiler while he was in university and I think his university degree was also in embedded systems so he was definitely the one of the first people that I saw that— like you said— wrote the whole thing in Rust, where I had the same reaction I think when I saw that same blog post that you were talking about, I go, “You *can* do it! Cool, I don't need- I don't even need the Arduino libraries anymore,” you know— 

*Scott Mabin*

Exactly.

*James Munns*

— and I think that required getting the whole compiler tool chain working, at least like LLVM at the time nominally supported Cortex-M, because I'm sure Apple or- or someone else had been using Clang to write their firmware for Cortex-M chips, so it was not surprising that LLVM worked for- for Cortex-M at the time, but just getting sort of like the top half of the compiler stack was already fun, and then like you said with doing it with an out of tree backend where probably it wasn't perfect. And then like you said, you were kind of blind to how the whole CPU was supposed to work and I empathize but I'm very, very impressed at at you being able to push through and getting that working. So— I don't have my timeline totally straight here of so they got the LLVM backend working prior to your involvement with them. So I'm guessing that's something they were doing because they wanted Clang to work with in C for their chips and things like that, or do you know what the motivation for them wanting to support LLVM was?

*Scott Mabin*

Yeah… so they definitely want to use Clang with ESP-IDF— their C-based SDK. Even a few years later we're still using gcc by default, just because the backend is just more mature like you get smaller code sizes, better optimization. But there is at least now the option to compile with Clang if you want to, and that actually helps on the Rust side in some cases, when— and I'll just explain a bit on the Rust- like ESP-Rust side, there's 2 approaches: you can use the `std`(standard) library using the ESP-IDF framework as essentially the OS, and you also have the bare metal programming which we've been talking about currently…

*James Munns*

That was an approach that I always thought was possible, and some people had talked about that, of using a real-time operating system to fulfil the standard library. So to to be able to spawn threads to have heap allocations and things like that, where in RTOS provides a lot of those things— at least potentially provides a lot of those things— and I know the ESP-IDF is based on FreeRTOS, which is very, very mature and has a lot of those features as either optional or- or very straightforward to do. So that was one of those conversations where I actually talked to proprietary customers about that possibility, people who are using either in-house or paid real-time operating systems. So not FreeRTOS but, you know, more commercial or application-specific operating systems and going, “Well, you could build on top of that and and treat it like you would anything else,” and a lot of those operating systems often even have like a POSIX compatibility layer, which means that porting it to the `std` library, it may not be the most performant way of doing it, but it'll probably work and it'd be interesting for a proof of concept and… It definitely I think lowers the barrier, because one of the first things you said is— you wouldn't necessarily recommend learning Rust and embedded Rust at the same time… 

*Scott Mabin*

Exactly. 

*James Munns*

I think there's actually 3 things there: for a lot of people, there's learning embedded if you haven't done low-level embedded things where you have to know how serial ports work and sort of what is a reasonable thing to try and build in embedded systems. And then there's learning Rust, which for for folks takes some time I mean it's- it's… a language that sort of forces you to make sure that you really understand it, otherwise it will kind of be an unpleasant experience for better or worse… I mean like, that's the reason we like it is because it doesn't let us mess up which means once you get used to that, it's very pleasant, but if you're new to it, it can be very easy to be ah… put off by that I suppose.

*Scott Mabin*

It holds us accountable.

*James Munns*

And then there's learning embedded Rust, which has its own set of paradigms, in how we design things and how we write drivers and how we write sort of things like that… and I've certainly always wanted to have something closer to like Arduino or Circuit Python where you go— look, you know something else. It will just work. Like it won't necessarily be the most efficient or perfect way of doing it, but if your goal is: I know Python and I want to learn how to talk to a serial port or talk to a sensor or something like that, I think there's a ton of room for learning on that without having to learn 2 or 3 things at the same time. So that was always really good to see, because for a lot of projects that's just good enough. Like very few projects that I've worked on really require you to push the limits of hard real time and limits of what RAM you have available. And every embedded developer will have a story where they had to do that, but so many projects are not that: especially for hobbyists and things like that, where the difference between the like, the chip with 32K of RAM and the chip with a megabyte of RAM is… a dollar? And when you're building one of them, that's worth your time. If you're making 10 million of them: yes, you want to optimize that dollar away, because that's $10 million. But if you're making one, then it does not matter and you should buy the fastest most- most full featured device out there, but… you need sort of all of those paths for getting in… But going back to when you were talking: we had none of that, so like… 

*Scott Mabin*

Definitely.

*James Munns*

You had mentioned that that was the approach was to sort of offer both of those options. But how did we get to that point where that was even feasible?

*Scott Mabin*

Yeah, so I don't remember any specific milestones in particular at this point… I essentially, I think I started a ESP32 HAL at that point so I don't think I touched the 8266 at all. I was just mostly interested in the ESP32 because it was newer, it was dual core, and I had one on my desk basically. So I think I started that and wrote a couple more blog posts: one about getting a debugging setup working. So I think at this point, the Espressif had released another iteration of the LLVM backend which supported debug info, which made things a whole bunch easier. I think I also… Oh yeah, I tried to mentally block this out, but I've just remembered: I wrote a horrible horrible tool to pass register definitions from C-headers and to create an SVD file and that was a crime against Rust for sure like I… I need to delete that repo. I think I archived it but I just need to wipe it off the face of the planet. But it did work, and it meant that I could debug using, funnily enough, Cortex-M debug the VS code extension, and I've supplied the ESP32 SVD that I just generated, I could see what all the peripherals were doing. That made it really easy to start writing drivers. At this point, there's also a bunch of community contributors, one of them was Arjan Mels, I believe. He's not around in the community anymore unfortunately, I think he… I'm not sure what he does now, but um… he was really helpful. He helped a lot with the runtime of just the extensive runtime. So you know you have the `cortex-m-rt` crate. I tried very hard to decipher how on earth these chips run and setting up caches and things like this, because this is also extra stuff that has to be done. With Cortex-M it's sort of out of the box, like you know, the RAM and flash will be mapped at a fixed address for the most part- I'm sure more complex chips do but with the ESPs, this sort has to be managed by- by the user or the runtime. But obviously, the only runtime that existed was C runtime, so writing one in Rust was interesting… but I learned a lot doing that. That was really good, and then I think at this point I did maybe one more blog post about Rust on Espressif chips, and then I think at that point Espressif reached out and um…  said, “We're looking to start a Rust team. Are you interested and do you know any other folks who are also interested?”

*James Munns*

That that is very cool. Do you know what prompted *them*? Was it them just following Rust like the rest of us were and saying, “Ah yeah, okay, I can see the value here. Yeah, that totally makes sense. Let's… let's start that going,” or was there like a customer that reached out to them, or or- yeah I know, you probably can't be too specific, but do you know like: what *started* the ball rolling there, or was it- was it just someone at Espressif following the news like the rest of us?

*Scott Mabin*

So, there was a like Rust channel in their internal Slack and they've been talking… basically there was a bunch of folks that were really interested in it and can see the power of it. But obviously it's quite a big task to, you know, just to do as like a side project at work in spare time or whatever. So I think there was definitely interest there. I also believe there were at least some customers curious about Rust. I don't know if any of my blog posts influenced that or not, but I imagine there was just some customers that heard about Rust and were wondering about using it. I think that was basically it. I can't speak to what they were thinking before they hired me, but in general they are quite a forward-thinking company, and they think about the future quite often and adopting future technologies and to be ready for when they are the present technology. So I think by starting the Rust team, maybe some people would say early? We now have, like, great support for Rust on our chips in various different ways. The tooling is great and in my opinion it's in a really good spot for you know, just if you want to build something, take a look at a library and either choose the `std` library approach or bare metal, depending on your experience level and just go for it. It mostly just works.

*James Munns*

Very cool. So you mentioned you were at university at the time and you were you were definitely working in a company that embedded was relevant, at least so that was on your mind even if they weren't using Rust. What did you go to university for, and what was- sort of before you talked to Espressif and went, “Okay, I'll go work for a chip manufacturer and help them build sort of infrastructure that a lot of people take for granted, or just use out of an SDK,” or- or things like that like… How did you get *into* embedded? You mentioned that your grandfather I think was an electrical engineer? Is that just something you'd always prototyped with stuff or- or build some electronics and you went, “Yup, definitely want to do that,” I mean, less about where you're working specifically, but more how did you get into embedded? Because it's always interesting to hear how people got into that, because it feels sort of niche but also I feel like there's a ton of different routes that people usually take to get into embedded.

*Scott Mabin*

So I ended up studying computer science at university, so I didn't have a embedded-specific focus or an electronic-specific focus. It was just something that I was always passionate about, in my spare time I was always, well, messing around with mainly Arduino stuff, sometimes ESP-IDF stuff, particularly towards the end of like my university career. Like, I’ve actually started to understand programming, so using the full ESP-IDF SDK was a lot more freeing than- than Arduino. And yeah, I mentioned that I- I did that placement year. I actually went back to that company for another year and introduced Rust at that company, which was nice. So I graduated at the beginning of the summer and I had the summer off and I knew I was going back to that place, and I was trying to figure out a way how I could convince them to start using Rust. So at the time they had just spun up like a- a new board revision for a- for a new product is using a Cortex-M F2 I believe. I looked around at the Rust ecosystem. So this was gonna be ethernet-based: so I needed a network stack, a ethernet driver and a few other crates available. So I looked around I saw a small TCP, I was like, “Check.” I looked at STM-RS and I saw STM32F, or ethernet, I was like, “Check.” And I was like, “Well, let's just see how far I can get playing around with it over the summer.” So I ended up being able to bring out the balls, get ethernet working, you know, a very simple… you know, I could just- I mean, I wouldn't call it HTTP server, I'll call it just sending, you know, fixed responses to make it look like HTTP server. So I rocked up back at the job and showed them that, and with enough persuasion I managed to convince them to- to use Rust in this project. And I mean, I've since left obviously but as far as I know the the Rust code has been deployed all over the world and basically just works. I don't- I don't hear many grumblings about it— 

*James Munns*

No one's reached out to be like, “I can't believe you- I can't believe you've done this to us,” like you show up, you do this and then you leave. At least no news is good news probably in that case. That's very cool. Yeah.

*Scott Mabin*

Yeah, exactly yeah.

*James Munns*

Huge props to that company, because that's one of those things that I've always thought is very helpful for bringing in both interns and just new hires straight out of university is that you get sort of this infusion of new ideas… where I've worked at some companies where the embedded team will be sort of this old guard that have been there for 20 years and they've always done it like this, and for some companies that works really well in, but it can also lead to, “… Well, we just keep stumbling over the same steps over and over,” or, you know, we've built a lot of defense mechanisms against that, but then as soon as we have to build something new, we start falling in the potholes again and things like that. But it's always been good to see— like, I find the companies that have the most sort of innovative approach are usually people who are bringing in new folks, either from other companies or fresh out of college, because sometimes it just takes that as an engineer you sort of learned, like, pattern matching. I don't have a better way of describing it of just going, “Okay, the answer to this question is this. When I see a problem shaped like this, you do this,” and when you put it in front of someone who doesn't have that experience, they go, “What if we do *this*?" and you go, “… what?” It's one of those really neat, surprising things where even though they'll have 10, 15 years less experience than you, they also have 10-15 years less *biases* than you, and it ends up being really interesting to go, “Oh. I- I guess we *can* do that,” where ten years ago they looked at it you go, “No, you can't do something like that,” like, that it's not reasonable or things like that but just… bringing in fresh faces or- or fresh ideas can help a ton of that. That's super good reflection on the company that you worked at, that an intern could come back after— I'm guessing you did one year there? 

*Scott Mabin*

Yeah.

*James Munns*

And then left and then come back and went, “Look what I have to show to *you*," and they went, “Okay, cool. Yeah, let's do that,” like… That's one of those things with working with interns like— you should assume that any interns you bring in will be sort of like a net zero to your team, like even though you have an extra set of hands, you're also helping them. And sometimes they're learning things and sometimes, you know, if it ends up positive at any point you go, “Great. That's wonderful,” and if it ends up a little negative, you go, “Still worth it…” like from a hiring perspective, or just sort of like new ideas or good-of-the-industry sort of things, it's good to do, but occasionally you will have like interns or things like that who come in and you go, “Yeah, you're killing it,” like and most companies are like, “Yes, please come back!” like, “We would like to hire you for that,” because… I've had a couple interns over the years and some of them were— like they were learning and they were doing their best. Some of them realized that that was not what they wanted to be doing, and that was a positive experience for everyone still; and then I've had some interns that, kind of in a very similar case: they came in, they build something, you go, “Wow! This makes my life just way easier, and I wish we had done this sooner,” and I'm glad- I'm glad they did that. So I'm glad you had that experience and they had that experience because that's not an always case and it seems like it was very positive for you and led to a lot of different things.

*Scott Mabin*

Yeah, definitely. Yeah, I mean— that year alone definitely cemented my love for embedded, even though I was writing C in that placement year. It cemented that this is what I want to do, so yeah, was all around a very positive experience.

*James Munns*

Very cool. So now you're mostly working on sort of infrastructure, and I'm guessing there's a lot of tooling that goes into that, there's a lot of development for SDKs and things like that or- or different vendors call it different things, whether it's like the BSP or the HAL or- or the SDK and things like that. But basically: the goal of most chip companies is we want to make it as easy as possible for you to use our stuff. Because for a lot of companies, especially smaller companies, they don't have sort of the teams to build a driver for everything. Or at least they have it in their mind that they can't do it and things like that. For a lot of things it makes a ton of sense: you you want the person who knows the most about the chip to write the driver, but also you can sort of get into a mindset where like they're trying to help everyone equally. And a lot of projects, you don't necessarily want that— you want a really specific thing. I'm always interested to hear what the experience is like from the *other* side, because I've never worked at a chip manufacturer, I've only ever been a customer of a chip manufacturer. And I've- I've written a lot of drivers myself, and I've grumbled about vendor tooling and drivers and documentation a lot before… but what is it like from the *other* side, because I think even if there are so many embedded engineers out there, there are very very few people who work at one of the 15 or 20 public-facing chip manufacturer companies, working on drivers and things like that. So what is- going from someone who built an application or a firmware or something like that to someone who's providing tools for other people: what does that mindset shift like, when you hear us complain in the Matrix room as people who consume those libraries— maybe not about ESP so much, but about other vendors we certainly have complained— what is that mindset shift like, or what's sort of like that cognitive dissonance that you've seen?

*Scott Mabin*

Yeah, I think this is actually kind of a different answer to maybe what someone working on the C-SDK would give, because I think the Rust team works very closely— like *very* closely with the community. Obviously, the ESP-IDF is very community driven as well. But they don't typically hang out in chat channels and talk to, you know, to the community like face-to-face. It's more like more, you know, someone files an issue, they're talked to a more- we have the forums which is a little less formal, but not as informal as like you know the Matrix channels that we have. 

*James Munns*

Yeah for a lot of silicon vendors, there's sort of 2 ways in: there's either we have a community forum somewhere that usually is well- well maintained. But you see a lot of the same questions over and over, or some of them will only have ‘Call your field rep’— like if you are a large enough company that we care about the number of orders that you make, you call someone on the phone and they will write the code or the proof of concept support for you. But for especially a lot bigger companies, that's the only interface they have with their customers. So if you're a hobbyist, the answer is ‘Have fun’ like, “Oh, we don't support that.” Okay, like… but it's been really refreshing to see y'all hang out in the main rooms and host your own main room where we can say, “Oh, if you have a question about that, these are the best people to go talk to, and they will actually make things work.”

*Scott Mabin*

Yeah, and I think you have a really good point about the hobbyists. And if you as a silicon vendor are trying to make it as easy as possible to use your chips, maybe getting feedback from experience and better developers isn't- I mean, it's always a good place to get feedback from but you know, if a hobbyist can use it with minimal experience, then you've essentially achieved your goal of creating easy-to-use drivers for your chips. So I really think that feedback from from them is really helpful.

*James Munns*

Yeah, it's one of those things where there's a surprising amount of habit and pipeline that not everyone values, but it's one of those: if you are in university and you're learning a chip and you have a really good experience with one of them, when you go to your next work project and they go, “Well, what chip should we use for the next product?” and you go, “I've used this one and it's pretty good,” *that's* going to get weighted really really heavily, versus if you went, “No, we should not use that chip— I tried to use it and it is miserable.” Even if your company is large enough that you would get this kind of custom support, it doesn't take much to rule out someone like… I’ve been in those decisions where you go, “Well, we make a Powerpoint slide or like an Excel table, where you go: these are our 5 options. Pros and cons for each of them,” and like 3 of them are going to get ruled out immediately because of price or features or- or whatever, and then usually there's this conversation where if 2 or 3 of them meet the goals and price and features and stuff like that, it's going to come down to: what have you done before, either at the company or someone goes, “Yeah, I know how this works,” or just someone goes, “I had a good experience,” like… I've absolutely worked somewhere where we ended up using I think Nordic and Zephyr at the time because I could drop into their IRC room, and one of their devs was hanging out in the IRC room and I had a weird niche problem and they're like, “Oh, it's probably this, oh we'll file a bug… Yeah, you tripped over that weird thing. It shouldn't be like that…” it was- it was Bluetooth and I was using some Android phone that handled Bluetooth weird and so they went, “Well, the phone shouldn't be doing that but we *also* shouldn't be freaking out about it,” and that was just such a positive… it only takes one of those positive interactions to go, “Okay, yeah, well we'll base our entire product stack on that chip.” So it's really good to have those positive interactions. And if you're not like Broadcom where you're like, “Well, we won't talk to you if you're not buying a million chips,” or something like that, then those can make a huge amount of difference because… the world is relatively small and we- embedded engineers talk to each other and people will tell stories where… I've been in forums either on like Slack or like, or Matrix or things like that where someone's like, “I'm thinking about *this* chip,” and me or someone else has gone, “Noooo, do not,” like… unless you have this really specific need, which yeah— then you probably will put up with it because that chip is *that* good at that, like you go, “Just pick this one. It's maybe a little more expensive or you'll have to work around this,” but like… Yeah, people talk. Especially with the internet. And it's been interesting to see some companies *get* that and some companies really *not* get that.

*Scott Mabin*

Yeah, definitely.

*James Munns*

It seems more common with sort of what I think of like, the open source Rust ecosystem. Someone like Dario or dirbaio from Embassy or some of the other folks that contribute to open source hardware abstraction libraries or drivers libraries and things like that, where you're aiming to put out a library that works for people, but there's nothing really special, like...
You have the same audience of: you want this to be good for people because you want them to use it, or it works for you and you're happy to take things that work for other people and… versus sort of a more… Yeah I- I guess that's also the goal of silicon vendors I suppose… but that feedback loop is much shorter because you're operating in the same way and that's one of those things that has been really positive is that I have seen the Rust team at Espressif pick up a lot of the mannerisms from the embedded Rust ecosystem, where there's not like anything hugely special about what we do, but there's you know like— Okay, we'll work on Github in this way, and we structure things like this, and we put priority and focus on these kind of things and… it's always interesting to see ‘reflected values’— I don't have a better or less buzzword-y term than that— but like maybe that's just me because I come from that Rust background. It's always interesting to see someone match so closely, where I saw that in the esp-rs repo, when it was just independent contributors and when Espressif hired a lot of those teams I was in some of those conversations where they go, “Well, how do we present our official Rust face to that?” and the answer was, “Well, we'll just move the esp-rs repo into the Espressif namespace,” and then you just keep working the way you were working, because obviously that's how you interface with that community, and sort of understanding your customers— or at least the subset of customers, or the specific community that you're addressing— is really big because it just lowers that like impedance mismatch of, “Oh, I have to go file tickets,” or like, by email or by forum and we go, “Well, in embedded Rust, we don't use forums a lot. We use, like, Github issues or chat,” and things like that. It's been interesting to see someone match the community so directly.

*Scott Mabin*

Yeah— I think a lot of that is because we come from that community. So the core contributors in the Rust team at Espressif— me, Jesse, Björn— were hired from the community. So we essentially already have those values, and now we're just I guess presenting them, but from Espressif’s perspective.

*James Munns*

Very cool. Well, I definitely didn't mean to make this all about Espressif. Are there any like, particular projects that you're working on right now that *you're* really interested in— whether it's on Espressif chips or not, I won't tell your boss, but— are there any like specific projects, or things that you're looking at— whether it's embedded focused or not— that's particularly interesting for you right now, or is it just focusing sort of solely on the- on the problem of, “How do I make Espressif chips easy to use for folks?”

*Scott Mabin*

So I do have one project in mind. So, I do enjoy like, developing libraries and drivers and things. But there is just something different about, you know, building an application or you know… building *something* that I miss. So I'm currently looking at building my own mechanical keyboard based on a ESP32-S3, and I kind of just want to essentially soup it up a little bit, get a nice display on there, get like a nice um… volume control knob. I've done a few PCBs in my time, but I would not be confident in any PCB that I create, so this is a learning experience for me at the moment. But yeah, I'm enjoying that and working on that on the side.

*James Munns*

Is there a specific form factor you're going for? Because I know there's… there's a million choices you could make in keyboards. I'm interested in what… I've built a keyboard, both like: I bought a kit and then put software on it, and then I've designed some like smaller keyboards and things like that, more like keypads, which has been really fun. But I know just getting into that realm: there's some people who are *very*- like, it's like people who are enthusiastic about cars or cooking or coffee or something like that. There are *opinions on the internet*. So… what design decisions, or what like choices have you made for *your* keyboard that makes it yours specifically?

*Scott Mabin*

So it's a variant of a ten keyless, so I'm essentially modifying it to fit my needs. But I currently have a 60% mechanical keyboard which I like but I miss the arrow keys and I also miss the `ISO enter` you know, like the big chunky enter key. 

*James Munns*

You are UK-based.

*Scott Mabin*

Yes, exactly. So those are my original goals and then I started doing the schematic and seeing how many free pins I had on the- on the S3. I was like, “Oh, I could maybe get a display on there…” I could maybe do some other things, which led me to start looking for displays… And I think already ranted you about this, about no displays have the tear effect pin exposed on modules, so… I hate screen tearing, like with a passion, so that's been a fun adventure. Yeah, that's the main thing I'm working on, on the side at the minute… other than just um, just cracking on with esp-rs basically.

*James Munns*

So, you chose the S3 which I think *does* have Bluetooth?

*Scott Mabin*

Yes.

*James Munns*

So is the intent to be USB *and* Bluetooth, or just a Bluetooth?

*Scott Mabin*

Yeah, both: so it also has a USB interface as well, so it be USB and um… Bluetooth.

*James Munns*

Very cool. Yeah, I- the keyboard I bought the kit for and that I designed I used an nRF52, specifically because it has USB and Bluetooth. There's a really cool library called Keyberon. 

*Scott Mabin*

Yeah, I heard about that.

*James Munns*

It's been a while since I used it, so I don't know if it's the current best effort. But it works really well for USB, but I've never gotten it working with Bluetooth… Now that Embassy has a ton of Bluetooth support, I think I have seen people do like the keyboard Bluetooth profile and things like that. So I think that's accessible these days? I haven't looked. But it's one of the things where: I built it and I went, “Well… I don't like…” I use my laptop a lot. I sit at a desk sometimes, but most of the time I'm sitting on a couch or in a chair or something like that and I just have my laptop with just the screen on the laptop. So I don't usually carry a keyboard anywhere. And I get really in the habit of using either like the Thinkpad or the Mac keyboards that I'm using. So I built this keyboard, I went, “Great.” And it was also a 60% keyboard where I went, “Okay, well I guess I'll figure it out,” I had some like meta keys for turning them into a- a directional pad and stuff like that and I did that and I went, “I'll just… I’ll just use my laptop…” like, so that's one of those things, like do you normally use a mechanical keyboard, or is that a?… because I did the project because— I went, “That's cool.” I could do that, and I did it, I went, “Cool.” and it was like building like an ash tray when you don't smoke, you know what I mean? Like, it was a thing where you go, “That's neat… but I don't use that.”

*Scott Mabin*

Yes, I do actually use it. So the monitor I have is is really cool. It's got a KVM switch built in, so I can switch between my desktop and my work laptop and still use the same mouse and keyboard. And I actually wrote a tool in Rust like two years ago, so the the interface to switch, you can only use the buttons but there's also a USB interface- like there was a Windows tool that could control it via software. So I just sniffed the USB packets and then wrote a quick tool and to essentially switch it to the inputs I want in Linux or Mac which is really cool. I've got it working in like a day with a like, tray icon that worked on each platform, like on MacOS or Linux or Windows all thanks to I think it was called tray-item-rs or something?

*James Munns*

Oh, there was a Rus- there’s actually a Rust project for it already.

*Scott Mabin*

Yeah, yeah… Which was pretty sweet, it’s essentially just gluing things together and writing a couple of USB packets, which was- that was a fun project.

*James Munns*

Very cool. All right.

*Scott Mabin*

But yeah, I do plan on using this keyboard if I ever make it and if the PCB works. 

*James Munns*

And which switches did you choose?

*Scott Mabin*

I've gone for calli milky yellows. They sound pretty nice that they're quite cheap. 

*James Munns*

Okay, I think I went like linear red because I had no idea what I was doing. I've used a lot of the smaller like Kyle or Kylie like the ah the Choc switches like the `CHOC` which are like the low profile ones because I was making a lot of numb pads and stuff like that. So those were lower profile, but I had a whole pack of like the white ones, which are the *really* clicky ones and then the brown ones which are the tactile ones, which are more thumpy but they're still very clicky… like even the red ones are kind of clicky to me I guess, but… I've never tried to use it in an office with someone else, and maybe if you're working from home maybe that's good if you like a clicky keyboard?

*Scott Mabin*

Yeah… before, I was working from home I did bring my current keyboard which is browned and I did get a fair number of complaints. So I left it at home after that.

*James Munns*

Nice. Are you doing that keyboard in public or is that a “just to for you” ah, sort of project?

*Scott Mabin*

It'll be in public once there is something to make public, essentially. Well, once I have a board, I'll just post that on Github I imagine, then start writing the firmware… I think is- is the plan.

*James Munns*

Yeah… I did some hardware design in university, and then I didn't touch it for like 8 years. And I think when I did it in university, I used like whatever the free version of EAGLE was at the time; but I started following a lot of people on Twitter who do electronics design, and I was really surprised at how good Keycad or KiCad has gotten in recent years. And I started designing my own hardware for the last like 2 years, and it's surprisingly accessible now especially because there's all of these fabrication houses that will even assemble a lot of the small components for you, and you only have to buy 2 or 5 of them or something at a time. And it might be a little more expensive than assembling it yourself, but knowing that I'm not going to fry like half the board, or have to debug it for a week because I didn't solder it right, or one of the chips backwards or something like that has been really neat as an embedded engineer to go, “Oh! I can- I can build my own glue!” Because that's one of the things that, like earlier in my embedded career I- I felt very limited by: you either have to buy a module from Adafruit or AliExpress or wherever, or find someone who's designing cool hardware who doesn't like writing software and, you know, find a way to partner with them for those kind of things, of just going— no, I can throw a microcontroller or a module on a board with some- some passive components and very quickly build something that's directly useful to me which was… I don't know. It's a very neat thing, and I feel like it was way harder which is why I avoided it. But now it seems much much more accessible.

*Scott Mabin*

Yeah, definitely. So the first PCB I did was that quote-unquote “smartwatch.” I actually did that in the web browser— I forget the name of it, but it was JLC… 

*James Munns*

Is it like EasyEDA or something.

*Scott Mabin*

That's it, that's the one. Yep and that, honestly— it's probably not the best editor, but it did the job and the PCB works, so I was happy with that. This time I'm using KiCad or K-I-Cad, however you actually say it. And yeah, I'm liking it so far. I'm a complete novice when it comes to this stuff. But so far it's relatively easy to use, and there's also a lot of good resources online. So yeah, fingers crossed: if I ever get this thing done, it'll work.

*James Munns*

Very, very cool. Well, I appreciate you coming to chat with me today: is there anything else you want to plug, or anywhere where you want folks to come find you, or where's the best place to follow you and keep up with- I know you're doing the quarterly blog posts on the state of the whole ecosystem. Anywhere specific you want folks to go look or go see after they listen to this?

*Scott Mabin*

Yeah, I guess the- the blog posts: if you know nothing about esp-rs, they're a good sort of time capsule as to how we've progressed over the years. Other than that I guess follow me on Twitter, or X, whatever it’s called these days. Where you’ll get the the latest of what I'm up to.

*James Munns*

Very cool. Yeah, we have show notes so I will put all the links to that in the show notes, but…

*Scott Mabin*

Awesome.

*James Munns*

Thank you so much for being here, it was excellent talking to you. 

*Scott Mabin*

Yeah thanks having me, I really enjoyed it! 

*James Munns*

Yeah! Right, talk to you later.

*Scott Mabin*

Alright? See you later. 

</details>

## Credits

This podcast is brought to you by OneVariable UG — a consultancy focused on advising and development services in the areas of systems engineering, embedded systems, and software development in the Rust programming language, based in Berlin, Germany. Check out our website at [onevariable.com](https://onevariable.com/) or send an email to [contact@onevariable.com](mailto:contact@onevariable.com).

Audio recording done by James Munns, edited and produced by Amanda Majorowicz. Special thanks to [Louie Zong](https://louiezong.bandcamp.com/) for the music.

Thanks for listening!
