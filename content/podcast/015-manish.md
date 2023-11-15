+++
title = "015 - Manish Goregaokar"
date = 2023-11-15T11:00:00+02:00
draft = false
in_search_index = true
template = "podcast_post.html"
+++

Another episode is coming from the archives, originally recorded in May 2022 with Manish Goregaokar as the guest- James and Manish touch on many topics, including: internationalization of languages, zero-copy deserialization in Rust, speedrunning video games and Vaccinate CA.

**Originally recorded on 2022-05-09**

<!-- more -->

## Audio

### FLAC

<audio
    controls
    src="https://delivery.jamescdn.com/2023-11-15-manish-goregaokar.flac">
        Your browser does not support embedding FLAC.
</audio>

[Download as FLAC](https://delivery.jamescdn.com/2023-11-15-manish-goregaokar.flac)

### M4A

<audio
    controls
    src="https://delivery.jamescdn.com/2023-11-15-manish-goregaokar.m4a">
        Your browser does not support embedding M4A.
</audio>

[Download as M4A](https://delivery.jamescdn.com/2023-11-15-manish-goregaokar.m4a)

### MP3

<audio
    controls
    src="https://delivery.jamescdn.com/2023-11-15-manish-goregaokar.mp3">
        Your browser does not support embedding MP3.
</audio>

[Download as MP3](https://delivery.jamescdn.com/2023-11-15-manish-goregaokar.mp3)

## Show Notes


- Intro [Manish Goregaokar](https://github.com/Manishearth), [Rust Dev tools Team](https://www.rust-lang.org/governance/teams/dev-tools), [ICU4X](https://github.com/unicode-org/icu4x) and [here](http://blog.unicode.org/2022/09/announcing-icu4x-10.html)
    - [Manish on Twitter](https://twitter.com/ManishEarth)
    - [Mojibake](https://en.wikipedia.org/wiki/Mojibake)
    - [Unicode](https://home.unicode.org/)
    - Mozilla + [Google internationalization](https://developers.google.com/international)
        - Mozilla [Servo](https://servo.org/) also [here](https://en.wikipedia.org/wiki/Servo_(software))
- How does ICU4X helps with internationalization, and programming for embedded devices 
    - [ICU (Internationalization Components for Unicode)](https://icu.unicode.org/) libraries
    - [Postcard](https://github.com/jamesmunns/postcard)
    - [zero-copy](https://en.wikipedia.org/wiki/Zero-copy)
    - [Serde](https://serde.rs/)
    - [yoke](https://crates.io/crates/yoke)
    - [Copy-on-write (cow)](https://en.wikipedia.org/wiki/Copy-on-write)
    - [type erasure](https://en.wikipedia.org/wiki/Type_erasure)
    - [`'static`](https://doc.rust-lang.org/rust-by-example/scope/lifetime/static_lifetime.html)
    - `for<'a>` or “For tick-a”: [Higher-Rank Trait Bounds (HRTBs)](https://doc.rust-lang.org/nomicon/hrtb.html)
    - [GATs](https://rust-lang.github.io/generic-associated-types-initiative/index.html)
    - Eduard-Mihai Burtescu : [eddyb](https://github.com/eddyb) and Jack Huey : [jackh](https://github.com/jackh726/) and [Oli Scherer](https://github.com/oli-obk)
- Galaxy brain blog posts from [In Pursuit of Laziness](https://manishearth.github.io/)
    - Not a Yoking Matter [Zero-Copy #1](https://manishearth.github.io/blog/2022/08/03/zero-copy-1-not-a-yoking-matter/) 
    - Zero-Copy All the Things [Zero-Copy #2](https://manishearth.github.io/blog/2022/08/03/zero-copy-2-zero-copy-all-the-things/)
    - So Zero It’s … Negative? [Zero-Copy #3](https://manishearth.github.io/blog/2022/08/03/zero-copy-3-so-zero-its-dot-dot-dot-negative/)
    - [zerovec](https://crates.io/crates/zerovec)
    - [rkyv](https://crates.io/crates/rkyv)
    - [Abomonation](https://docs.rs/abomonation/latest/abomonation/)
    - [byte-slab](https://crates.io/crates/byte-slab)
- Formatting huge amounts of Rust code, making GitHub crash
    - [crabbake](https://crates.io/crates/crabbake/0.4.0)
    - [proc macro (procedural macros)](https://doc.rust-lang.org/beta/reference/procedural-macros.html) or [here](https://doc.rust-lang.org/proc_macro/)
    - Microcontroller [i.MX RT family from NXP](https://www.nxp.com/products/processors-and-microcontrollers/arm-microcontrollers/i-mx-rt-crossover-mcus:IMX-RT-SERIES)
    - [form](https://crates.io/crates/form)
    - [rust-analyzer](https://rust-analyzer.github.io/)
    - [web-platform-tests](https://web-platform-tests.org/)
    - mergebot [Bors](https://bors.tech/) or [here](https://github.com/bors-ng/bors-ng)
    - [Docs.rs](https://docs.rs/)
- Video games, speedrunning and Excel integrations 
    - [Fuzzing](https://en.wikipedia.org/wiki/Fuzzing) or [Fuzzer-Generated Code](https://github.com/dwrensha/fuzz-rustc/#bugs-found)
    - [Elden Ring](https://en.bandainamcoent.eu/elden-ring/elden-ring), [Tetris99](https://tetris.com/topic/tetris-99), [Elden Ring ‘fake’ walls](https://www.gamesradar.com/oh-no-elden-ring-has-fake-walls-you-need-to-hit-up-to-50-times/)
    - Breath of the Wild [Blood Moon](https://www.ign.com/wikis/the-legend-of-zelda-breath-of-the-wild/Blood_Moon), Zelda speedrun : [Item Sliding](https://www.zeldaspeedruns.com/twwhd/tech/item-sliding) (grappling hook)
    - Super Mario 64 [“Watch for Falling Rocks” commentated](https://www.youtube.com/watch?v=kpk2tdsPh0A) and [parallel universes](https://pannenkoek2012.fandom.com/wiki/Parallel_Universe)
    - [Celeste](https://en.wikipedia.org/wiki/Celeste_(video_game)), [EVE Online](https://www.eveonline.com/) and [Excel integration](https://www.eveonline.com/eve-academy/excel-add-in)
    - [Factorio](https://www.factorio.com/), [Prometheus](https://prometheus.io/), [Grafana](https://grafana.com/)
    - [MIT Mystery Hunt](https://puzzles.mit.edu/)
- [Vaccinate CA](https://en.wikipedia.org/wiki/VaccinateCA) 
    - [Story of Vaccinate CA](https://worksinprogress.co/issue/the-story-of-vaccinateca) by [Patrick McKenzie](https://twitter.com/patio11)
    - Tweet from [@Patio11](https://twitter.com/patio11/status/1349577791537250310)
    - [Airtable](https://www.airtable.com/)
    - [MySQL](https://www.mysql.com/) / [PostgreSQL](https://www.postgresql.org/)
 
## Transcript

<details>

   *James Munns*
 
 Well do you want to give yourself a quick introduction?

*Manish Goregaokar*

Yeah, so hi, I'm Manish. I've been doing Rust stuff for ages now: I'm part of the Dev tools team, used to be on the core team. These days most of my Rust work is on ICU4X, which is a unicode project for making an internationalization library in Rust that's modular and fast and, well, in Rust. 

*James Munns*

So, I've known you mostly through the Rust project, like I feel like I've interacted with you online a couple times, then I know with the Rust all hands, we've chatted a couple times, probably played Mario Kart once or twice. 

*Manish Goregaokar*

Yeah, probably.

*James Munns*

But yeah, I know following you on Twitter is always an experience because I know you're on the Unicode bodies and things like that. Which means you have… you are the abyss gazer for things like mojibake and things like that like… whenever when someone's like, “Why isn't this encoding right? Why did this ridiculous edge case happen?” Or even just for spoken human languages, people start talking about like, a weird mashup of puns or roots of words— I feel like you're always at the root of that conversation, or get roped into that conversation fairly quickly.

*Manish Goregaokar*

Pretty much, yeah I'm the abyss gazer for multiple abysses I guess? I've always been interested in human languages and that got me into Unicode, that got me into many other things, and I guess it's a similar kind of interest that got me into programming languages as well. I spent a lot of time doing Unicode stuff, I have a lot of interests in human languages in general, though most of that doesn't overlap with my primary work in Unicode.

*James Munns*

So I know you were at Mozilla for a number of years… Was you working on Unicode a result of working at Mozilla, or did those things happen completely independently or…?

*Manish Goregaokar*

Ah, kind of both? So as someone interested in languages and especially writing systems, at some point I got roped into the Unicode script ad hoc where they work on encoding new writing systems or new characters in existing writing systems. So basically, the part of Unicode that's not emoji and not other weird stuff, it's for the actual text, and that was just an interesting thing for me to attend every now and then and help out in and enjoyed that. That's kind of how we got into Unicode, but my primary stuff right now is on ICU4X, which was started as a collaboration between Mozilla and Google. And when it started, I was at Mozilla. I was not working on internationalization at Mozilla, I was working on Servo, but the person who was working on this knew me well, and also I helped him with a lot of Rust stuff and also he knew that I had a decent amount of internationalization background. So I got kind of roped in when this started, and it was just like this little side project I had of helping out ICU4X, and then later when Servo shut down, the folks at Google were kind of like, “Hey you want to work on ICU4X full time?” and I was like, “Yeah, sure!” This is something that I cared about enough that I actually spent extra time on at my previous job. So, I don't mind working on this. So yeah. So it's kind of both.

*James Munns*

So, I know internationalization covers a really broad set of concepts and and things that are needed… What aspects of internationalization does ICU4X specifically aim to help with, or what kind of problems does it solve?

*Manish Goregaokar*

I kind of want to say all of it. 

*James Munns*

Okay.

*Manish Goregaokar*

But that's also kind of broad depending on what you mean by internationalization. Basically, ICU4X doesn't do translations or anything. It doesn't do things like providing you a framework to translate things. What it does do is kind of all of the hard algorithmics or data-driven bits of internationalization. So, how do people format dates? Oh well, it turns out that even in the US you have 50 ways of formatting dates, whether you want to use numbers or words or short words or whatever and now you need to do that for everyone. How do different languages have plurals? How do people format numbers? Because some people use periods and commas and vice versa, and then some people put the commas in different places. So it's a lot of stuff like that, segmenting words, whatever… There's already a library, really 2 libraries called ICU —which is Internationalization Components for Unicode — and they've been around for at least a decade, probably 2. They're kind of old: they're in C and Java and they're maintained by Unicode as well. They're kind of what everyone uses to do all of this, and they're fine. The main problem is that they're not modular and they don't give you much control over the data. So you're kind of stuck pulling in this giant dependency, and it takes up a lot of space and you can't do a lot of dynamic stuff that people would want to with data loading and with other stuff. Also the end result of this is many platforms have like multiple copies of it in the end, just because you can't really slice it up nicely. Android has at least 2 and I think it's more than two. I mean Chrome has its own, Android has at least 1 and 1 more. There's there's a bunch. Everyone has this problem: Firefox has this problem, Android has this problem. Because it's so large you can't even like think about targeting an embedded platform, because this giant Java or C++ library is just not going to fit. ICU4X was kind of: with the goal of we want a library that's modular so you only pull in what you need. If you only need to format dates, you're not going to pull in the formatting for currencies or plurals or whatever. And much more control over the data loading, so you don't have to bake in the data from the beginning. It doesn't have to mean like, “Oh, well because we can only have our app be 50 MB, we're only going to support these 5 languages because we can't support more without bloating up data,” and we want to give you control over data loading so you can kind of load it off the network or whatever, or kind of design your own way of loading data, cache it, whatever tradeoffs you have about data, we can support it because we kind of let you handle that part. That just makes it applicable to so many more things and so much more flexible so that's kind of the goal. And also it's in Rust: so modern programming language, safe but still fast. It's fast but still has a small footprint and yeah, so that's kind of like our goal.

*James Munns*

I've spent most of my career on tiny embedded devices, and for a lot of them, they either tend to be headless so they're mostly sending raw data and things like that. So, user presenting messages are not— I haven't worked on a lot of systems with a user interface, I should say. So, this has been rare in my career but I've definitely worked with some folks who have either worked in the video game industry, or web and front-end industry where internationalization and localization was a huge pipeline project where: from the tools that you use for doing the translations to keeping track of those translations in the application and things like that I know there's this huge amount of- I don't want to say unseen effort, but it's something that when a lot of people are thinking about software and development, that's not the part that they're thinking about unless they've worked on a team that's worked like that and and to go back to what you said about size the few projects that I have worked on that have had an LCD or something like that— we've typically had to recompile the entire firmware for all the different languages because, like you said, there's only so much room for non-volatile storage on those devices. So I definitely remember having macros in there and you'd have to build with different, you know, environment variables or compiler flags in there, and rerun 16 build jobs and then update the firmware specifically for devices that are going to that region… which might make sense for a device that never gets updates, but definitely as things become more connected and expect to have updates and either gain functionality or details change and things like that, that becomes less and less optional even for the really tiny stuff.

*Manish Goregaokar*

Yeah… tiny stuff… most embedded devices probably have fewer internationalization needs than like Twitter or Firefox because, you know, there's- there's only so much UI you can have. But even just thinking about, like, for example, a smartwatch— or this isn't actually a smartwatch, this is a GPS watch, which is even a better example because this- I don't think this chip on this is, like, a proper chip with a full OS and everything, this is probably an embedded device. It does a lot, but also it's got to have a battery life of like at least a week or so when I'm not in exercise mode, and it's got to show stuff. And this one isn't internationalized, but if it were to be internationalized, you'd want to fit all of that on this tiny chip. Most of the actual, like, smartwatches, like the actually smart-smart watches, where you can install apps and stuff, those run Android or IOS or something and they have a full-fledged ARM chip… but again, for battery life reasons, you're not going to have that ARM chip running most of the time, you're going to have it running, like, only when I'm pressing stuff on it and otherwise you've got this like tiny little embedded device- embedded chip that's usually just kind of chilling there and showing numbers on the screen.

*James Munns*

Yeah, the race to sleep is pretty much everything in battery powered devices is: how little can I do and how quickly can I go back to sleeping and *look*  like I'm doing something, but really using micro amps of power because there's no other way I'm going to make it through the week.

*Manish Goregaokar*

Yeah, but they still have plenty UI and nothing I've ever used of this kind is internationalized but there's still enough to internationalize, not enough as Twitter or Firefox like I said, but still quite a bit.

*James Munns*

Yeah, definitely, so this is something that not necessarily is what's holding, you know, I have this template my welcome message and I don't have the 25 different languages there, but this is something that's a toolkit almost for making that, where you have the details of the numbers or, like you said, even just calendar dates of making it not look strange to people who aren't in the region where the developers are basically — because I think we've seen that on, you know, US developed devices, or devices that are from a more international audience and you look at it and you go, “I know what it means…” but just every time I look at it looks weird, like… I know living in Germany, just looking at currency and things like that and seeing the period and the comma switched for numbers and will throw you off the first couple times you see it because you go, “Wait — is that — why does that… $1,000, and why are there 3 decimal places on that? Oh no, it's a million Euros, okay we're talking about something completely different here, or €100,000 instead…” So, I know that you're using Postcard as one of your formats there. I know that you and I have had some particularly interesting battles with zero-copy things. So: for folks who aren't super familiar with zero-copy, the idea is that sometimes these messages you receive, either from storage or off a network or something like that, make up a pretty huge amount of the data that you receive. I mean, if you think about JSON, which is probably a bad example which we'll come around to later, but… I mean that's a bunch of keys that are strings usually and a bunch of values that are either strings or objects that are then consisting of strings most of the way down, and that tends to be a pretty big amount of the data that comes in, and if you are streaming hundreds of megabytes of this data per second — if you have a cloud service or something like that — if you had to sit down and copy every one of those into a Rust string or something like that… It's not a lot, like `clone` is not that expensive an operation, but anything done millions or billions of times adds up, and zero-copy is sort of an interesting way of saying — well, don't duplicate it, just hold on to the original packet and whenever you have a string slice or whatever the equivalent is in your language, you just say — go look at the original payload, and it's there. And in the past, this has always been done for efficiency reasons but in a lot of other languages, it tends to be kind of a huge threat vector to say nonetheless, because if you accidentally keep pointing back to that message buffer and then get rid of the original message, but you're still holding on to some reference of that — you're in trouble. And this ends up being either, like, a use-after-free or buffer corruption kind of thing. And Rust has been particularly interesting, because lifetimes are more or less exactly what that's for — is the ability to safely say, “Do I still have that packet? Is that packet still good, and is it still around and can I reasonably borrow from it?” I know when I was making my the first iteration of my little computer, my little OS, I was like — I want to copy none of the times, I want a DMA memory directly into a buffer, and then I want to borrow that and process the entire packet stack and then send it out with only 1 copy basically from the input DMA buffer to the output DMA buffer. So I could get end to end routing… and I drove myself crazy, because you can do that and Rust will not let you make a mistake, but everything will work and then you go — oh let me just move this message over- Oh nope - Doesn't- you're not holding onto that buffer for long enough anymore, or you have to copy it and then you have this one path where you have to copy things and it ends up being really painful… and Serde does let you do zero-copy things out of the box, but I think both you and I have run into cases where we've wanted a little bit more than what comes available out of the box, or we're trying to do something a little bit more clever? And I know you've ended up writing a library called yoke which is for exactly that kind of problem.

*Manish Goregaokar*

Yeah— in the world of zero-copy, I've actually at this point designed 3 libraries um, that do various things in this space and they're all kind of- there are limitations of the space that I want to get around. They're not necessarily all crates that solve a problem that can't be solved another way. But they all- like for for our specific set of constraints, they work well. To touch on yoke a bit: the name ‘yoke’ comes from the fact that in zero-copy deserialization, mostly when people talk about strings and bite slices, they'll use the cow type because as you mentioned earlier: you can't zero-copy deserialized formats like JSON because they have escapes. So a string in JSON might not actually be the same exact representation as it is in memory because it'll have some backslashes in some places that you don't want. So if you're deserializing that, you can't always take a reference you might need to create an own type. In the zero-copy world, it's basically good practice to always use copy and write types everywhere so that your type can be deserialized from self-describing and from binary formats. The idea of yoke is basically that it does… It does what I call lifetime erasure, which is kind of a throwback to type erasure from din and the idea is— It can turn a compile time lifetime into a runtime one. When you mentioned earlier that when you're doing zero-copy deserialization in many languages, it's just a massive threat vector. In Rust it no longer is, but it is a massive lifetime headache because suddenly the data you deserialize from- the compiler will keep track of it for you, but you still need to handle it and like keep it around and you've got to do that all at compile time and you can't always do that. Sometimes you want some kind of caching strategy. Lifetimes don't understand caching, lifetimes just want to be statically known to always work. The idea of yoke is basically: you can construct some borrowed data out of a data source which I call a cart. And you can kind of yoke that data to that cart, and you get this yoke type which contains both the data and the backing source. And it doesn't have any lifetimes that are externally necessary. It's got a `'``static` lifetime that you can see but basically this means that from the point from the point of view of the outside. This is just a normal type. You can kind of bop around and move and you can hold onto it for as long as you want you can destroy it immediately. And it's got a runtime kind of lifetime and it's a fully owned type basically. The way you access the data is this .git method, which gives you the internal object with a much shorter lifetime. So it's still safe. So it's kind of gate keeping your type at runtime without incurring any runtime checks, .git is just a free kind of pointer. It's- it's giving you the lifetimes at runtime and so you can put something like an RC as the cart. And now you suddenly have dynamic lifetimes. You have the benefits that RC gets you when it comes to data management, but you still have zero-copy deserialization so you don't ever have to do those allocations when deserialising, you just use yoke and things are fixed. I will caveat that it uses the `for<`a>` syntax a whole bunch, which is basically- it is trying to use higher kind of types before higher kind of types are ready.

*James Munns*

Is it something that will be better with GATs when GATs come down or is this like really all the way in the higher kind of type?

*Manish Goregaokar*

Yes, it- it will be better with GATs when GATs are down. But also, mostly any compiler bugs we hit are compiler bugs that are probably also present with GATs. So it's not like a huge difference, we're just using the stable thing for now, and when GATs are like fully baked, we will do a breaking change and release a better version. It uses, like, stable GATs and there are plenty of bugs and shoutout to eddyb and jackh who have fixed a lot of them. I keep showing up with like, “Oh hey, here's an ICE,” and then my example code says like ‘yokable’ in 20 places because um… I have joked that we should just like check yoke into tree as, ah, as a test case. Yeah, we- we- we hit a bunch of ICEs.

*James Munns*

What was the threat I saw you make against Oli?… ”The- the longer something isn't const, the more transmutes I will make.”

*Manish Goregaokar*

Oh, so that is not galaxy brain zero-copy crate 1, or galaxy brain zero-copy crate 2. It's galaxy brain zero-copy crate 3. 

*James Munns*

Okay… oh, so there's something that's superseded yoke now. Is- is that galaxy brain crate 2, or 3? Okay.

*Manish Goregaokar*

No- no, no… 

*James Munns*

Okay

*Manish Goregaokar*

No, these are all things that kind of work together… and a bit of background on all of these, like every last crate here, I was kind of like— let's just eat the performance cost or the like memory cost and like see what happens. But then like, firstly folks had measured it, or already kind of had experience from ICU, what the costs would be, and also folks were kind of like, let's get the last bit of performance out of this. So in every case, I was like okay— so there's the simple solution that most Rustacians would do, and it's got a cost, and I've got this idea… I really don't think we should do it, because it's kind of weird and a bunch of work and everyone's like, “Yeah, you should just do it!” And so I have spent a lot of my time just doing these things. I've- I've been doing feature work as well. But a lot of my time has been spent building like, weird Rust crates— which I enjoy! Like that is actually very fun for me. It's a lot of unsafe code. 

*James Munns*

When someone pays you to shave a yak... You shave a yak, I guess.

*Manish Goregaokar*

Yeah, when someone pays you to shave a yak, you do shave a yak. Exactly. You can even like yoke it to a cart, like a pack yak. So- so, the second to crate is this thing called zero-vec which essentially… serde only lets you do zero-copy with byte buffers and string buffers- and strings. So- so byte slices and strings because everything else has constraints. For zero-copy deserilization, you need to guarantee that the in-memory representation is the same everywhere, and you can only do that for those 2 types- the only 2 unsized types that you can do that for are those 2 types. And for types that are sized, you just copy them typically. You're not going to actually try to do a zero-copy deserialization, because those just get copied on the stack. You only want to do zero-copy zero to deserialization when you've got something that's like a string that's a hundred characters long, or a byte slice that's one hundred bytes long. And that's all fine, but we want to do more. We want to actually have zero-copies completely— or well, we want to have zero buffer copies. Which means we need zero-copy collections. And that's kind of what zerovec gives you. Zerovec basically gives you versions of vec and map that can hold most types. You might need to auto-derive a trait on them but they can hold like all the integer types they can hold an enum or a struct that contains the integer types. They can hold like a slice of strings, so you can do- you can do things like vec of vec of string, or vec of vec of vec of vec of whatever in zero-copy. And also they are internally copy-on-write, because in the zero-copy world like I said you almost always want copy-on-write, so they just do that for you… and yeah, they internally kind of work by defining a wire format for everything and storing everything in memory that way and doing that conversion at runtime instead. So there's a bit of a runtime cost on reads and a larger runtime cost on writes, but the idea is at least in our case, we're never going to be writing to this data in user code. We produce data and then the users get it, so it doesn't matter if producing data is a bit slow. So yeah, that's the second one and it basically just gives you this entire world of types that you can use to do  zero-copy. And we've been using that, and it's been working pretty well. There's also a map type in there and the map type kind of. It's basically a binary search map. 

*James Munns*

It is it like a linear map. Yeah, okay, binary search. Okay.

*Manish Goregaokar*

Yeah, nothing fancy. And worth mentioning that there's already a crate that does a lot of this called rkyv, which was talked about a while ago and it's got pretty popular and- and it's quite good. Ah, we didn't want to use rkyv because it kind of mandates everything about the format. We wanted to use Serde with its pluggable formats, so… and rkyv kind of needs you to be in that universe, but rkyv is also very very good and… everything that zerovec does, rkyv does better. 

*James Munns*

Nice. Yeah I mostly I'm not really met the rkyv folks, but I ran into them because when they were building rkyv, they actually went out and built one of the most comprehensive benchmark suites for different serialization formats where they they have a lot of the Serde formats. So my format Postcard got pulled in there, and rkyv was in there and then there were some non-Serde ones, like more Protobuf-style ones as well… And it was interesting to see that, and they even included like Abomonation which is one of my favorite crates which is just basically like— well, you `memcpy` to a buffer, and hope you never send it to another computer that has a different representation… but it was written by ah, a guy who was working on high performance computing and things like that where they knew that every node in their cluster was using that exact same CPU. So for them, why pay portability costs when you know that portability is not a thing and they gave it the name ‘Abomonation’ intentionally spelled wrong. So I mean you know sort of the danger that you're getting into but it was interesting going back and forth on that and and seeing the different tradeoffs, because Serde has been tremendously popular in that it covers like, 95% of the serialization and deserialization use-case landscape, and because of that it's gotten huge. And you want to stay in that ecosystem because everything works with that, almost any crate that you have that has data types will just have some sort of Serde pluggable format, or like you said — the model is implemented, which means you can plug it into Postcard or JSON or TOML or whatever you'd like… But there are a couple of these edge cases where there's just… either the format- it was impossible to do that when the format was first stabilized, so these kind of things are not possible without breaking backwards compatibility. Or they're just outside of the design, but like the primary design space of these things like that where yeah, zero cost to serialization is one of those things that I've run into, where I've had a lot of these copy-on-write problems. But I'll go one further and usually I am working on a `no_std` system which means that I don't have easy access to do that copy when a write is necessary because there's no allocator, which means you really don't have much to work with so… My first version of that was doing totally deserialized but you just couldn't touch anything and you had to be really careful about what you touched. The second one I ended up making my own sort of like user space, reference counting allocator, where you just would have slabs so you would just say okay I know all of my messages are going to be less than 512 bytes on the wire. So I have a little mini allocator that can hand out 512 byte pages and didn't matter if you got a 10 byte message or a 499 byte message. You always got the big buffer. But: it was reference counted so you knew as long as someone was holding onto some piece of that slab, that memory would stay intact, which was exactly what I ended up needing. But even doing that, it was difficult, because I've forgotten… but I know you and I had a lot of conversations because you were working on yoke around the same time I was working on byte-slab and I was trying to figure out how to make serde do the thing that I wanted, and there just really wasn't… like there's a really deep set of APIs that you have accessible as either a format implementer, or as a data model implementer, someone who's serializing the data types. But I realized what I really needed, needed to be on both sides of that, and in Rust's traits, there's not really a great way to enforce that you have someone on both sides of that. So what I my hack ended up being: you deserialized to borrowed types, and then I would come in afterwards, look at all the references, look at the pointers and then try and reassociate them with the original buffer, which means I'm scanning through all the references and I think I called it ah… ‘rerooting’ or something like that where it's just like, “Is this a reference? Is this a reference to the slab that we have? Okay, cool!” where I'm literally just doing pointer math to see if it's in between the memory range of that buffer, and made me very nervous… Although Genkra eventually did calm my fears on whether doing that pointer math because: in my mind doing math on pointers is always undefined behavior, like if you're comparing pointers from different allocations, it's always undefined behavior. And I was worried if you're comparing a pointer of a reference, that's not from that buffer; with one that *is* from that buffer, then you have problems but she pointed out… I think the most succinct thing was… there's some limitation there where it's basically like— yes, I think that's theoretically allowed to be undefined behavior, but… literally no compiler defines that as undefined behavior, because it would break literally everything, and there's basically a switch that no one turns on LVM for specifically that optimization and it breaks everything. So I was a little worried about it, but it ended up being okay… But I know you and I have sort of felt around the edges of what is possible with serde, where on some hands, it's ridiculously powerful but then there's always that one 5% of things that you want to do where it's just like there's just no way to express that unfortunately.

*Manish Goregaokar*

Yeah, and like zerovec is kind of an attempt to like add another percent to that, or subtract another percent from the 5 %… but yeah exactly, it does a lot, but it also it has limitations and we have been trying to work around a bunch of those… Overall, doing pretty well. It's a great crate and it does almost everything we need and the things we don't, it's good enough that we've been able to design these crates that extend it. Also, yoke is not even working around a serde limitation. It's working around a problem that any zero-copy deserialization crate in Rust will have unless it decides to manage the data for you, which I think some might. Yoke is something that you can use with Archive as well, or with anything else. Oh, and the third one is the most galaxy brain yet because it is… It's the one where we go, “What if you never had to do *any* deserialization, what if it was 0 deserialization deserialization like forget zero-copy It's like negative copy There's no deserialization cost.” The background of this was in some cases you actually do have trusted data. And we- again we want to support data loading patterns and whatever, sometimes your data is baked into your binary, you already trust it and what you could do is like include bytes and then deserialize. But you're paying that cost at some point, and if you're a browser like Firefox: Firefox is- as mentioned before, Mozilla is working on ICU4X quite heavily… So if you're a browser like Firefox, you care about process cold start times very very much, especially now that browsers are many processes, so you don't want to pay that cost at the beginning… and you also really just don't want to pay that cost as much as possible. So, even if it's zero-copy, zero-copy deserialization is pretty fast. But it's still- especially if you're doing a lot of data at once, it's still somewhat slow, so the idea… the last crate was kind of like— what if we could solve this problem? What if we could- we could support a way to kind of bake data into the binary without paying serialization costs? And the answer in that space is `const` and the- the easy doesn't-actually-work answer is: what if all our serialization framework was `const`. It doesn't actually work, because Rust doesn't have support for all the things that need to be done such that something as complicated as serde can be maybe `const`. It does have designs for all of this though. So I think yeah, 

*James Munns*

Oh really?

*Manish Goregaokar*

The Rust `const` infrastructure will actually kind of live in a space that's kind of perpendicular to traits, so that a trait doesn't have to be inherently `const` you can kind of parameterize yourself on a trait, that you say that this is the `const` version of this trait. So you kind of have traits- normal traits, and then you can- for any normal trait, you can say, “this trait but make it `const`". And that's a different bound. So I think it will be theoretically possible with the designs people have, but that's like a couple years away, so we can't rely on that. So instead, the thing we're doing— and this is where some galaxy brain stuff happens, and this is also where I threaten Oli with writing more `mem::transmute`s— instead, what we're doing is we're still using `const` to create one static, but we are serializing to Rust code. So there's this crate called crabbake. 

*James Munns*

Go on…

*Manish Goregaokar*

This one is not actually published yet, or- well it's on it's on crates.io as a placeholder and it- the first version of it should be published this week or so, but it's still much more experimental. We're still kind of playing around with it but folks can try it out. Crabbake gives you a custom derive that… basically it gives you a custom derive that gives you a function on the type that generates a token stream that can `const` construct a value of that type. 

*James Munns*

Ohhh, ok…

*Manish Goregaokar*

So now you can use that in a proc macro or build script, or- or just in a tool before- run before everything, and generate an absolutely massive Rust file for all of your data. 

*James Munns*

So you serialize a proc macro basically and then the proc macro executes the serialized proc macro to create the values?

*Manish Goregaokar*

Yeah, you serialize- well, you serialize to Rust code. It’s just normal Rust code and then whenever you want- well, it can be weird because it's trying to be `const`. So yeah, you serialize to Rust code, so basically the bakeable or crabbake trait gives you a .bake function on any value and that'll output a token stream. Which in this case it's just normal Rust code, it's just a constructor that calls constructs all the children and whatever, you just stick that in your Rust file. 

*James Munns*

So- so, it actually serializes 2 as token stream you said? 

*Manish Goregaokar*

This 2 as token stream. Yeah.

*James Munns*

Wow.

*Manish Goregaokar*

ICU4X is a ton of data that we kind of test with we have like a whole bunch of locales and a whole bunch of different things. There's a pull request open right now which is making everything work with this. It's like… multiple megabytes of Rust code like like 10s or something of megabytes of Rust code I think. I believe it actually takes a while for Rust format to format. 

*James Munns*

Wow, I don't think I've ever seen Rust format hiccup before.

*Manish Goregaokar*

Yeah I- I forgot the numbers…

*James Munns*

Yeah, the biggest crate that I've seen is, in embedded we tend to do code generation for register definitions and things like that. So you know, when you've got these registers that configure your serial port or your memory interface or whatever, we'll generate a bunch of code for that, that gives you sort of safe APIs for that. But these microcontrollers have a big range of how complex they are, and for some of the really like… really really high-end microcontroller— so getting out of the realm of what a microcontroller actually is anymore, I'm thinking of ones that are like the i.MX RT family from NXP which is a 1 GHz microcontroller with a ridiculous amount of RAM. I think it generated a million lines of Rust source, which probably isn't 10 MB even, and I think we we already had to break that up using a tool called form because the codegen all happens to one file, so you get this librs that is just 1 single line of 10 million lines worth of code— or a 1 million lines worth of code— then you run it through Rust format, which chunks that into many, you know, a million lines of pretty formatted code, and then you run it through a tool called ‘form’ which takes modules and breaks them out into files automatically. And then you run Rust format on that again, but the problem is whenever you do a clean build on that it takes like, 6 minutes or something like that just for that one crate to power through that million lines because it's a single codegen unit, which means parallelism means nothing to it and yeah, it's it's sort of the, “Oops, we have found the logical end of our tool’s usefulness,” where like, okay, O(n^2) is fine up to some point but then at some point it just becomes not okay anymore.

*Manish Goregaokar*

So yeah, the GitHub diff stat says 350,000 lines, and apparently it crashes rust-analyzer. So now we need to tell Rust we're figuring- well, I think we've already figured out how to tell rust-analyzer just- just don't look there. I'm also kind of advocating that we don't check in all of it because if we check it in for one locale- that's kind of in a- and we can generate all of it during testing. But yeah, it's a lot. Actually this just reminded me of a somewhat unrelated anecdote of when I was working on Servo… There's a test suite that all browsers share called web-platform-tests and it's kind of maintained collaboratively by all browsers. Browsers also have their own tests but this is kind of like most of the web compat tests go here and it's massive, and we used to submodule it. But basically all browsers moved over to checking it into tree and having like a sync tool that tends to work better for stuff like this, and the commit where we did that… It didn't just break GitHub on Servo— it took down a GitHub, like, node or cluster or whatever they've got. We know this because, well, our mergebot Bors stopped working because it could no longer tell if things were mergeable because the GitHub API was just not telling you if things were mergeable across the the big merge we'd done. And then we kind of emailed GitHub to be like, “Oh hey, this happened, and also we made this merge. So maybe that's why…” And then they're like, “Yeah, there was the whole thing that happened,” on like— I don't know exactly what the term was but apparently it took something down. Not too much, but it was like, not just our repo.

*James Munns*

Yeah, I think the worst we've had with that in like embedded Rust is occasionally we’ll codegen a normal microcontroller will be like 100,000 lines of code, but sometimes some of the way that these organizations work is they'll have all of the chip families in 1 repository, just because there's like common tooling and things like that. So when you update the tooling, it will regenerate all of these, and then we'll publish all of them and you'll get something, like you know, 150 of these crates checked in at the same time that take about 4 minutes on a clean build each, and they're also relatively large. And I think this was before there was like a dedicated paid docs team, or like a dedicated docs.rs team when it was much more of a volunteer project. And you just go— we'll send someone an email like, “We need to publish these, like how can we make this not… like we're doing this as volunteer work, and we realize you're doing this as volunteer work, and we don't want to cause problems, but we also want all 150 of our crates on crates.io like… what- what can we do here-” I think now there's a much better system for priority leveling and things like that, where there's a couple ecosystems that tend to do that a lot. It's not just the embedded folks anymore, but usually it tends to be generated code projects that are doing… like I'm thinking of like Google or Amazon's API definition generators or things like that, that generate JSON or Protobuf or gRPC or whatever for all those interfaces and they tend to be huge and you'll see just like 200 crates in the queue for a day or two…

*Manish Goregaokar*

Yeah, they all get deprioritized I believe which is kind of how it's handled. Docs.rs has like a list of known ecosystems like that and it will deprioritize them. It still wants to build them, but it will like try to you know, not let other crates suffer a sort of. I don't know exactly how the prioritization works, but yeah, it does something like that. Which I think people in those ecosystems are kind of fine with because you know, they just want their stuff to work and it's fine if it takes some time. 

*James Munns*

Yeah, we would also get into problems where because it's like 1 crate… We kept blowing the memory limits of the Docs.rs builder and stuff like that too. So then you just have these like backed up failed jobs and things like that and… yeah it- it was bad… but I think… Yeah, I think we ended up submitting some of those as like stress test examples for the compiler project as well, because when you're generating that much code, it's pretty pathological to what a normal Rust project looks like, but there's also not a great way of breaking… we've- we've tried breaking it up a couple times but it ends up- you end up with circular dependencies that are really hard to programmatically generate if that makes sense.

*Manish Goregaokar*

Yeah. Generated code is always kind of, like well… the worst. I mean also— and you've almost certainly have— but if you've looked at fuzz code… It is… it is written by aliens. It's like the same thing, a lot of compiler bugs are just, you know, hit by code written by aliens I guess…

*James Munns*

Oh oh, you're talking about like… the generated like minified cases that get generated by fuzzer… okay.

*Manish Goregaokar*

Yes! Yes, when a Fuzzer… It's always wild stuff. It's like— Why? Why? Who- who would do this, why? Why is this? 

*James Munns*

Who wrote `break` 117 times in a row inside of an `if` statement and you're like, “Well, you're right, I didn't think to test that, but that sure does crash the compiler…” 

*Manish Goregaokar*

Yeah, and the answer to who would write that is Elden Ring players. 

*James Munns*

Yeah, okay. I admit I am totally out of the loop. I've been playing like Tetris99 for the last 3 years and I am a… I am a terrible gamer.

*Manish Goregaokar*

Oh I'm also out of the loop. One thing that was- it caused even a little bit of a controversy- was apparently they had this wall that you had to punch like 100 times and there was no feedback that like punching was doing anything; you know in in a normal game, if you kind of attack a wall, just do nothing, and if it's a special wall, you'll hear a little sound. And there was no feedback: you just had to like stand in one spot and punch a wall a hundred times, and then it opened a secret door… Which later I think it transpired that actually that was a mistake? It wasn't intentional, but because Elden Ring is so well known for being a hard game, everyone was kind of like, “Yeah. Yeah, that's- that's what this game's like. This- this is normal.”

*James Munns*

It's like old video games would have that in their, like when they would ship the games and then they would write the manuals after they ship the games and they're like, “Look out for this- this person will come in. Ah it'll end your game!” but it was really like, a buffer overflow or something like that. Like they would just write it in like it was some intended behavior but it wasn't. I've seen people on Twitter talk about like as soon as speed runners realize that they're basically doing reverse engineering, but like hard mode, because you have no tools or anything like that… sometimes now you have tool-assisted speed running and stuff like that, but like figuring out things… I can't remember which one of the Zelda games it was, but one of the Zelda games, if you exhaust the heap, you get like this red moon condition, and it kills everything on the map and then respawns things. It basically is like- it's like a forced culling heap.

*Manish Goregaokar*

Oh that's a different one… Oh oh oh oh! That's oh, you're talking about Breath of the Wild. Yes.

*James Munns*

I think it's Breath of the Wild, yeah. It's funny because they programmed it in the game so it doesn't look weird, but people have looked at it and gone — Oh okay, you just exhausted the heap or fragmented the heap so bad that it needed to basically give up despawn all the entities and then respawn the ones that needed to be there in like a clean, nicely compact format or something like that. It is funny to see all of those speed runs are basically executing arbitrary code or figuring out how to get the allocator into like a really niche terrible fragmented state just so you can force some behavior.

*Manish Goregaokar*

So yeah, there's- there's an old Zelda speed run where someone just like- apparently when you throw a grappling hook something of it gets leaked and so they were just like leaking grappling hooks into the heap until this barrier would not load. And like, it was this barrier that would take a lot of time to go around so you kind of- you first fill up the heap until the barrier refuses to load and then you can just go straight to the boss fight which was nice.

*James Munns*

Nice. Yeah I’ve seen a bunch of those where it's- when you watch the speed run and the first like 8 minutes is: they're doing one thing, like they're doing backflips or shooting a grappling hook or picking up and throwing bombs and picking up and throwing bombs, and it's- it's all that just to like get the stack pretuned or to get the heap pretuned to have certain values and it's like aaand rob sled- like, and you just do ridiculous things from there.

*Manish Goregaokar*

I yeah, yeah, this isn't arbitrary code execution. But like if we're talking about speed running I would be remiss if I didn't mention the quadruple parallel universes one, if you've— Oh, have you not seen quadruple parallel universes? 

*James Munns*

That rings a bell. But ah, I have no idea what game that is for, yeah.

*Manish Goregaokar*

So. It's for the Super Mario 64 “Watch for Rolling Rocks” level. And there is this one Youtuber who… This is not a speed run in the like speed sense. It's a speed run in the ‘we're playing the game with some arbitrary constraints because you know, why not’ and the constraint that they're trying to do is minimize A-presses. You know, the- the very useful button in the game. Let's- let's just not use that as much as possible. And what the game is about, is about beating that level in half an A-press. It explains what it means by half an A-press, but the general idea is sometimes in some cases, you can go through a lot of the game with just A held down. So if you've already pressed A for a different reason and you don't let go, then you can do a bunch of stuff but it's one of the most galaxy brain speed run videos I've watched, and it's- it's commentated and they kind of explain what's going on in a very matter-of-fact way. It doesn't sound like they're describing something galaxy brain but like, every 5 minutes, it just gets worse. They start out with like simple stuff and then it just gets worse and worse and worse, and eventually they get to what is known as quadruple parallel universes. That's the like end state so you can kind of see how much it's going to take to get there. It's a very good video and it has- I feel like it has kind of captured minds much wider than the speed running community. Someone made this animation of like Mario versus… some other Nintendo character where they fight, and then the fight heavily references this video. Quadruple parallel universes is just this amazing video and it's like- it's like 20 minutes, it's not that long. 

*James Munns*

I'll have to go look at it… Especially if you've caught it after it's been known for a while, people have gone back, and a lot of times when they figure out the trigger case or the reproduction case they'll go in through an emulator and like step through all of the states and figure out exactly why it does that. Or like trying to figure out other ways that you can reproduce it even faster, or like you said like— maybe throwing the bomb triggers it in a hundred throws but the hook shot does it in 20. So that now everyone switched over to the hookshot meta, and starting to use that but… I have to go look at that one like… I've seen some really crazy Skyrim ones and like, Super Mario 64 has got to be the one that I see the most. I think that's also one of those games where… they shipped it in… I can't remember exactly what it was, but it was something like: they shipped it with some optimizations on but nearly all of the optimizations in the game turned off, because they just… like, they were working up to the last minute to ship it and I'm sure they were running to some like compiler limitation or undefined behavior that they were tripping over or something like that, and like… I want to say something like the engine is at like 01 or 02 but all of the entity logic for all of the the characters and stuff like that are at like no optimizations, because like— someone's told the story afterwards, they're like, “It was just hitting some compiler bug and we couldn't hunt the compiler bug down, so haha no optimizations! And turns out it's still fit on the system.” But I'm sure there's like a ton of the exploits that take advantage of that, either just because like it's less optimized so it's easier to get it to fill up the stack or the heap or something like that, or just something else terrible, or more predictable to exploit because it's not optimized in some really weird way.

*Manish Goregaokar*

Yeah. Speed running is not something I pay that much attention to, but whenever I do, I always have a good time.

*James Munns*

Yeah, it's a look at something that's like peripheral to your industry, but not exactly what you do and it doesn't cause you a headache because you're not working in the game industry. So it's not like immediately nausea-inducing.

*Manish Goregaokar*

Yeah, though there are like also some really good relationships with speed runners in the game industry like Celeste was- I think it was designed by someone who is a speed runner? But it was designed with speed running in mind as well, and like there- there are a whole- whole bunch of little things that are in the game that kind of help you notice that. Recently someone… someone made a version of Celeste with- it was the wildest thing I saw and someone was speed running this on Twitch- and Celeste is a very hard game and someone made a version of Celeste where instead you're playing Mario and you have Mario's move set mostly so you are playing a game that is very hard with not even the right move set? And there's the whole bunch of like- it's not just that, there's like a lot of things are changed to make it actually playable. And I was watching a speed run of that and I was just kind of like— people are amazing.

*James Munns*

I love when you get the crossover of games and developers, especially games like that, that either have like a really specific workflow or something like that… like, EVE the online, like, space faring game—

*Manish Goregaokar*

I know what you're talking about. I know what you're about to get to. Go for it.

*James Munns*

Introduced yeah, an integration with Excel, so like because people were already like tracking the meta of- because like the whole thing is like shipping and getting arbitrage of like ‘buy it here for this cost and sell it over there.’ They're like, “We just built an integration!” And I know you were playing… what is it called, the… Factorio with a bunch of Rust folks and someone's like, “Okay, how do we get like, Prometheus logging into our instance so that we could use, like all these- like logging and tracing and visibility tools, so we can watch the amount of science we are doing per second, or the number of trains we have going or…” And watching those come together where people are like, “Ha Ha! I have the tool! I have observability tools for this, like I know how to automate this!” and that becomes like a weird meta-game.

*Manish Goregaokar*

I'm pretty sure that was Eliza, and I'm also pretty sure that's like, the second or third Factorio game I've played with Eliza over the years, where at some point Grafana or Prometheus gets brought up. And I'll point out: there is a mod for Factorio that lets you do this. This is already possible! I've never used it. Ive never played a game with it, but it has been fun to talk about. Yeah, definitely, that overlap is also always fun. The e-online thing made me chuckle a lot. 

*James Munns*

Yeah I'm sure they did it mostly for a laugh but like, I saw a huge amount of press just on that, where it's like, “Eve <3 Excel” kind of thing.

*Manish Goregaokar*

Yeah, I mean I suspect it's like actually really useful. Yeah, Google Sheets can do, it can do network requests, so you actually can do a lot of weird stuff in Google Sheets if you really want to…

*James Munns*

It's got this- like instead of like the visual basic environment you'd have on your desktop- I know my wife does a bunch of data analysis and things like that and there's a couple of like… Google Sheets Javascript platform because they basically have like a little sandbox Javascript environment you can use for- you would use like, not just a VLOOKUP but the more like, advanced scripting type stuff, if you wanted to pull in currency definitions. I'm sure you can go… deep with it, if you really want to.

*Manish Goregaokar*

So, this year for the first time I participated in an MIT Mystery Hunt team. And for those who are unfamiliar, it's kind of like this treasure hunt that usually occurs on MIT grounds every year, this year it was remote but it occurs on Martin Luther King weekend. Basically you solve a bunch of puzzles, and the answers to the puzzles feed into more puzzles and it's just like you know… puzzles. I was- I was participating in a chill team, I'd- a friend introduced me to it, and she was like, “You, you're gonna enjoy this.” Initially, I was doing a bunch of like language related stuff, because there were some things that I knew that like many of the people on the team didn't, so I was like focusing on those. But a thing that I noticed was firstly: my team did everything in Sheets. Like, everything. And the sheets were magic. You could add rows to a sheet and it would… every- every time we unlocked a new puzzle, you could add a row to a sheet, and it would add like a Slack channel and create all of the new sheets that you need, because everything was done in Sheets. And also: that was not unique to my team, and I know this not just because people told me, but because the puzzle website had a, like for every puzzle, there was a ‘Copy to Google Sheets’ button or ‘Copy to Excel’ button that would kind of copy it in a format that could be pasted into Sheets without any problems. So like, if there's a bunch of stuff on it, it might be a puzzle that actually- even if it's a puzzle that really doesn't need sheets, it still had one, but… It was just, you know, everything happened there and it was- especially since people were solving puzzles remotely, that actually worked out really well, and I had a good time. Folks had like some serious Google Sheets chops. It was, like… there were times, especially since I was in Pacific, there were times when it was late at night and I was one of the few people playing, and I got to like use- or only person who is free who was able to do the thing, so like I was also able to do a bunch of complicated Google Sheet stuff. But like some things people designed were just amazing. I always love when people do weird stuff in Excel. And Sheets. 

*James Munns*

Yeah… I feel like the downside to that is usually at least as a software developer is those things scale up to some point, and then the maintainability drops off a cliff because you are like- it makes it very easy to do certain things but not maintain them, but for something where it's like a three day weekend where you're like— I need observability now and I need something that's basically automatable and usable as a frontend to my entire team, it's got to be probably one of the most flexible things for that without building your own crazy toolkit for it out of the, you know, from scratch.

*Manish Goregaokar*

That gives me flashbacks to Vaccinate CA. Vaccinate CA was a speed run startup.

*James Munns*

Yeah, I remember following that along and seeing especially like, what's his name Patrick— Patio 11— talking a lot about that and… do you want to give like a brief history of what that was and how you got involved? Because I saw you were involved with it, but I never really heard the story behind it.

*Manish Goregaokar*

Yeah, so Vaccinate CA was basically the idea that finding vaccines is hard. This was in February 2021. You've got to call up like 10 places to find out if any of them— forget if they have stock or not— if they are even doing vaccines. At the time in California, mostly… mostly people above 65 were eligible, so it was also like, this is quite a bit of a burden… and we also knew that this is going to just get worse as more people get eligible. I think the government did have plans, but they were not moving along. So basically- and it started with a tweet from Patrick McKenzie which was kind of like— a thing that tech people could do without that much effort is just build a, like… and not just tech people, like volunteers… could do without that much effort is just call up all the places that might do vaccines, find out who are doing vaccines and publish this list. Yeah, so I got involved because ironically, they were doing some um… Excel / Google sheet stuff and some scraping and someone was like, “Hey, Manish, you know a bunch about that: do you want to get involved?” and I was like, “Yeah, sure!” So I got involved in that. We started out- and this is where like the speed run startup comes in, because we… I mean it was a speed run startup whose only goal was throwing away all the money. Which is, you know, we're not trying to make money, we got donations at best and then we spent it on stuff. It was a speed run because we kind of went through, like, the stages I think startups kind of go through with a bunch of their product and stuff, but in ridiculous time spans. And we start out with like an Excel sheet of just a bunch of places folks had kind of copied from various websites and phone numbers, and I did like some Google Maps API calls to populate them with phone numbers and everything else and folks were calling there and just like ticking something in the sheet… and at some point people who had used Airtable or worked on Airtable got involved and they were like, “You know what… This is not going to scale. Let's go to Airtable.” so we went to Airtable. And we set up kind of a bunch of tables and that was great because it was very easy to kind of filter stuff and redirect stuff in Airtable. We also had this little script. In Airtable, you can write JS to make like a little UI, and we had this little script someone had written that would kind of just give you a random number and a place, and you call it and you just had like a phone tree to kind of click through, and that meant the programmers and like the people- the organizers kind of direct calls and stuff like that very quickly. This got very useful when we realized on like day 6 or something that most people don't have vaccines but safeways do have vaccines because turns out - you know who's good at getting cold stuff around? 

*James Munns*

Grocers?

*Manish Goregaokar*

Grocers. And if the grocer happens to have a pharmacy, they're also- yeah, they also have vaccines, so then we kind of focused everyone onto Safeways. At this point we still kind of just had this Airtable embed on the website, so people would open the website and kind of- you could filter it there but it was still very hacky and then Valerie Lansey designed a little map that would show you and you could just zoom in and kind of click on the area. So basically, we grew from like, a small group of people to quite a lot of people, a lot of people calling, new volunteers every day. In like a week or so, maybe two weeks, we had coverage of all of the healthcare places in California that we thought would have vaccines. And we were like able to get information from them at a scale of like, a couple days on recalling and people were already using it quite a bit… And we kept doing this, and at one point we actually- we grew past the Airtable data limit. Like— bear in mind, we had people who worked at Airtable. We had enough money to pay the problems away. We hit fundamental limits in- there's like a 50 thousand row limit in Airtable-

*James Munns*

Mhm, I know Excel has something similar.

*Manish Goregaokar*

Airtable made it 100 thousand for us, I think their actual limit is something else. But they were like— this is a fundamental limit, so we ended up having to rearchitect again to use like SQL. But this this took a while, and at this point there were actually like full-time employees. When I got involved, it was fully volunteer, and I did a whole bunch of the technical scaffolding at the time. So another thing I speed ran then was, I speed ran Burnout over ah- over a long weekend. It was actually- I think it was good that I did that, because it was an interesting experience, and I handled it well because there was the Martin Luther King long weekend. I was already pretty involved, and I was doing a lot of stuff: I was like doing a lot of the technical infrastructure, but also doing kind of a lot of the managing of who we call in all of our ontologies, because every county did things differently. A large problem we had was just the ontology of things: how to categorize this information in a uniform way, how to get all the information that's necessary, and how to surface it to the user and so that was a lot of work that we were doing. So I was just constantly involved and because I was behind a load of technical stuff, I was like necessary for a bunch of stuff. On Saturday and Sunday basically… and most of Friday… on Saturday I go to the hills and do habitat restoration, so I did do that. But aside from eating and sleeping, like Vaccinate CA was all I did. And I enjoyed it. And then like late Sunday I was kind of like— this is not sustainable, I cannot keep doing this. And so I started writing docs, which I'd already been doing but I was like— more docs. And on Monday I kind of made sure more people are involved, handed off a bunch of things and stayed pretty involved, but was no longer like—

*James Munns*

Load bearing.

*Manish Goregaokar*

— load bearing on a lot of things that needed a constant effort. There are more people involved and… Also we kept growing. 

*James Munns*

Yeah, startups are interesting in that like from what I've seen, the- the ones that do the best tend to design for the next order of magnitude or 2 and no further and no nearer or anything like that where like. You know that if you're starting with the Excel you're like— okay, this is going to get me to N-thousand rows or X-number of simultaneous users, and it'll be fine. I don't need to overengineer it until that, and then you go to Airtable because you're like— okay, well I can do my next 2 orders of magnitude of growth here. And then at some point you're like, you know, SQL is unavoidable at this point like— why not drop it into MySQL or or Postgres or whatever managed service. You were using or something like that and… It's interesting to hear that go so quickly, because I've- I've seen startups die because the market takes off faster than they can respond, and I've also seen startups die because they respond faster than the market takes *them* up, you know what I mean, like… they're designing multiple orders of magnitude forward when that's not their problem right now. But it's interesting to see like… you don't get that a lot in startups where your market is so excited and like people are like, “Yeah, cool, I get what you're doing. Yeah, let's do it. Let's help,” like… Where- where getting vaccines in hands of people… and another a huge part of that startup process is like learning the on-the-ground information where, especially if you have a startup that is not made up of people from that industry or things like that— there's just certain lessons you only learn by being involved, and I saw a bunch of reports from that, of just learning that— oh, you can *ask* the pharmacists at this place because they have other friends that are pharmacists and will tell you what all the other nine pharmacies are in that region, and like you said like: no one thought to check a Safeway, but someone's like, “Have you tried call in Safeway yet?” and I'm sure that was the point where you're just like, “Oh, this has changed…” like—

*Manish Goregaokar*

Oh, we- we already had Safeways on our list. But what we didn't realize was- I mean we were just calling everyone on our list, and then we were like calling Kaiser hospitals where we'd have like a 1 hour wait because everyone was calling them. Half the big places were places everyone was calling, and we were like— let's get that information put on the website so that, you know, instead of people having to call… Yeah, we knew Safeways were there. We just weren't focusing on them, where we're just calling everyone and then we were like— Wait, the big hospitals don't have their stuff together yet, but Safeway does. And soon after CVS did and like… We could see the trends, we we had a very good bird's eye view of distribution. Yeah, so we knew about Safeway, we just didn't- it never occurred to us to be like— oh, of course. Safeway is who we should focus on.

*James Munns*

Yeah, and I'm sure that changed like you said changed every week. Because you were trying to capitalize in the folks who didn't have their stuff together last week, but did have their stuff together this week, but the market- or like the people who were looking for vaccines hadn't caught up with that. So it was like trying to quench- or basically maximize the amount of effectiveness you could have of your callers for what the availability was.

*Manish Goregaokar*

Also to give an idea just of the like speed of the thing: Vaccinate CA lasted like five months. Not a long time, and it went through like 3 or 4 stages of startup land in that process. The Excel thing was like a day, and the Excel-to-Airtable took like three days, and then Airtable was around for like a month or 2 or maybe 3.. and then after that for the rest it was… yeah. And we were adding a lot more stuff in that time, there was like more than- that kind of went through that ratcheted scaling thing just very quickly. Yeah.

*James Munns*

That's very, very cool. Yeah, and I know just like a couple months ago I saw Patrick posted like, “Hey, we've actually closed down the Vaccinate CA company because I guess there was a company that got spun up to to handle those donations and things like that and—” 

*Manish Goregaokar*

For donations. Yeah.

*James Munns*

— it was like you know… You don't always get to be really successful *and* close the startup up, but like literally there was nowhere else for this to go and I'm happy where it ended up where it's just such a antithesis of how a lot of startup stories go and it was fun to watch from the outside and to hear people talk about like everything that was learned and the stuff that you might- like make sense in retrospect, but until you're there, like you wouldn't have thought to ask that or something like that. 

*Manish Goregaokar*

Yeah, I learned a lot in that, and when it closed down, it was a very fun moment. It was a very interesting moment for me, not fun, but it was interesting because it was like I was extremely happy that everything… We had gotten to the point where we didn't need to exist anymore. It was also kind of sad that like, oh, all these people I've been working with I'm not going to get to work with them that much but it was… It was an interesting moment, like kind of bittersweet. 

*James Munns*

Yeah, it's it's weird to categorically say ‘it's a success *and* it's done and gone’ like it's not something that lives on just outside of you. It's just something that that was a successful effort, and like you said: you were so successful, it no longer needed to exist, or you know the rest of the world caught up with the speed at which you were working.

*Manish Goregaokar*

Yeah I think I saw- I think it was a Tumblr post, but someone recently was talking about how in our society we tend to mark view success as permanence and it doesn't have to be like… You ran a restaurant for like 10 years: that's success even if it closed or whatever. Success doesn't have to be permanent. If- if you did a thing and you enjoyed it, that’s success. If it did good, that’s success. Yeah, that's kind of how I think I see Vaccinate CA. It was never intended to last more than like—

*James Munns*

It’s filling a need that you knew was ephemeral, but like you wanted it to be *as* ephemeral as possible, like you didn't want the mismatch of supply and demand to be large forever. The goal was always to bring that- or constrain that as much as you could so…

*Manish Goregaokar*

Yeah, exactly. Yeah… I think it succeeded pretty well in that. 

*James Munns*

Very cool. Well, thanks so much for chatting with me today. 

*Manish Goregaokar*

Yeah, it was great talking to you! 

*James Munns*

Where can people find you on Twitter and things like that?

*Manish Goregaokar*

Well, I'm- I'm ManishEarth like, everywhere on the internet. So yeah, you can find me on mostly Twitter or GitHub I guess, yeah.

*James Munns*

Very cool. Well thanks so much for chatting. 

*Manish Goregaokar*

You're welcome! 

*James Munns*

Alright, bye. 

*Manish Goregaokar*

Bye!

</details>

## Credits

This podcast is brought to you by OneVariable UG — a consultancy focused on advising and development services in the areas of systems engineering, embedded systems, and software development in the Rust programming language, based in Berlin, Germany. Check out our website at [onevariable.com](https://onevariable.com/) or send an email to [contact@onevariable.com](mailto:contact@onevariable.com).

Audio recording done by James Munns, edited and produced by Amanda Majorowicz. Special thanks to [Louie Zong](https://louiezong.bandcamp.com/) for the music.

Thanks for listening!

