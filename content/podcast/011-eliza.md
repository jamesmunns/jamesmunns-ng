+++
title = "011 - Eliza Weisman"
date = 2022-04-12T20:00:00+02:00
draft = false
in_search_index = true
template = "podcast_post.html"
+++

James chats with Eliza about systems, systems of systems, operating
systems, java, java cards, what posix did wrong, and a ton of other
rust adjacent things.

**Originally Recorded on 2022-04-08.**

<!-- more -->

## Audio

**FLAC**

<audio
    controls
    src="https://delivery.jamescdn.com/2022-04-12-eliza-weisman.flac">
        Your browser does not support embedding FLAC
</audio>

[Download as FLAC](https://delivery.jamescdn.com/2022-04-12-eliza-weisman.flac)

### MP3

<audio
    controls
    src="https://delivery.jamescdn.com/2022-04-12-eliza-weisman.mp3">
        Your browser does not support embedding MP3.
</audio>

[Download as MP3](https://delivery.jamescdn.com/2022-04-12-eliza-weisman.mp3)


## Show Notes

Coming soon!

## Transcript

<details>
James Munns
Yeah I spend way too much time listening to podcasts and like especially like D&D podcasts are like the thing that I found a while ago just because they produce so much content and I just like having people speaking in the background because it helps my brain shut off.

Eliza Weisman
Umm, same Oh yeah, same. Yeah I listen to a lot of podcasts when I'm like cooking or doing chores around the house. I Listen to a lot of well. There's your problem which I think ah oh you would love it. It's a podcast about engineering disasters with slides.

James Munns
What?

Eliza Weisman
Oh you should You should check this out. Um, well,, there's your problem is like my favorite podcast. They talk about Historical engineering disasters and like how what happened and why and then they just like make a lot of jokes and it's like very irreverent and this show has like extremely like leftist politics. So like what else could you ask for. And I Love those sort of like engineering failure stories. Um, because there's so much to learn from them. Yeah.

James Munns
Yeah, there's ah, there's some yeah I've seen like the air disasters like there there used to be like the air disasters website and I know someone's making a podcast I think Rooster teeth is making a podcast about it now where they just go through the details but they're like especially the aviation ones are so interesting because they go deep in the investigation. So like they figure out exactly what happened.

Eliza Weisman
Yeah, yeah, a lot ah like well there's your problem 1 of the hosts is like ah a structural engineer so he sort of focus ah like they do a lot of episodes about like buildings and dams and bridges and stuff. Um, but they do other things as well.

Eliza Weisman
Um, and it's It's just a really really fun show despite though like extremely dark sort of content because like like the hosts are just like very very entertaining and it's kind of silly and they all have good politics So that's one of my favorite podcasts. Anyway.

James Munns
Very cool.

Eliza Weisman
We're we're on the podcast talking about other podcasts that we like. So yeah.

James Munns
I mean that's meta I mean I haven't released an episode in like a year so I mean whatever meta we get into is going to be totally fine, but before we get too far. Do you want to give yourself a quick introduction.

Eliza Weisman
Yeah, ah for sure. So my name is Eliza Wiseman um I am a system software engineer at um, a company called buoyant um, formerly based in California now we're sort of a globally distributed remote organization. Um, and the main thing that I do for my day job is I work on um, a piece of software called Linkerd. Um, and linkerd is what is called a service mesh so you have these like um. Like really big web backends for like for big web applications that have all of these like microservices right? these like different components that all talk to each other over like some Rpc protocol. Um, and what linkerd is is. It's sort of ah a proxy layer that you put. In front of all of these different microservices and all of the like intraservice communication. So like within the data center all of the different services talking to each other sort of goes through this like this application layer proxy.

Um and it has two components. It has sort of a control plane that. You know pushes configuration and management collects metrics stuff like that and then you have these proxies and the proxies sit in front of each each application service and traffic is routed through them. Ah we use ip tables for that. Actually so it's like kind of transparent. Um, and in the proxy layer you can do all of these like really cool things like you do routing obviously in load balancing but you can also do stuff like um, the proxy layer actually is where we can implement like mutual tls.

So you get these like security benefits for free. And all of this is kind of like stuff that people would have to like re-implement over and over again in each of these like microservices and maybe they're like written in different programming languages or like running different software stacks and you don't really want to have to like copy a bunch of code or you also don't really have this like, single management plane for all of those configurations if like the load balancer settings are just sort of embedded in like each service. Maybe they're different and it's really maybe an ops responsibility more than like an application developer responsibility. So Maybe they want to configure those things globally but they they can't because like every. Application and you know they use like different libraries and different languages and so on so the idea of of putting all of this stuff into the proxy layer and making things like Tls load balancing networking metrics and application routing is sort of a. Ah, concern of the network layer instead of a concern of each application service and so we have this out. Yeah,, go ahead exactly right? exactly.

James Munns
Um, it's sort of oh sorry, yeah, it's the sort of like roads and bridges. It's the stuff that really everyone sort of needs and rather than having everyone having to invent their own standard and invent their own things that it's it's letting everyone kind of share that and it's funny when you said linkerd my brain was primed and ready to think.

Eliza Weisman
And.

James Munns
I work on this little project called Tokio but I I suppose Tokio I suppose Tokio is more the means rather than the ends whereas like Tokio is widely used in a ton of different ways. But Tokio isn't the product Tokio is sort of like yeah like the means to the end of of linkerd.

Eliza Weisman
Um I do also work on that. Yeah, yeah, yeah, so this is sort of the story is that that's um. Actually this is kind of an interesting story. Um, it wasn't really where I was planning to go but I you know I'm happy to tell this story because I think it's really interesting. Um, the first version of linkerd was actually written in Scala. Um, and the reason for that is that a lot of ah the founders of buoyant my employer. Um, our former Twitter engineers and Twitter at the time was like very all in on the Scala programming language. Um, and at Twitter they had written this really quite wonderful library called finagle um, and finagle is this. Like functional programming inspiredd rpc library so you model like clients and servers for network services using this sort of functional. Um service. Abstraction. You can layer in all of this different middleware that does things like routing load balancing so on and this is just like this big Scala library that honestly. Is a little bit hard to use and it doesn't really have right and it doesn't really have this sort of like global configuration plane. So the original thing that my company did is we just took all of the cool like load balancing and reliability features and metrics and all of this stuff. Finagle does.

James Munns
I've never heard that about Scala before.

Eliza Weisman
We just take that and turn it into a standalone proxy. Um, but sort of the problem was that this sort of space of um like the service mesh space. A lot of the people in it. Um, ended up using Kubernetes and. The original linkerd ran in so you have these like cluster orchestrators right? that like big cloud thing where you have like um application containers and you want to schedule a bunch of them so you have some some system that like. Schedules the different containers across multiple machines in the distributed system and handles like um, you know who can talk to who and like what ports are exposed and all of this stuff. Um, and the first version of linkerd was very agnostic in like what environment it might run in. But most of the industry sort of centralized on Kubernetes and 1 of the things that people wanted to do in Kubernetes is that they wanted to deploy these pod or these these proxies in sort of a per service model. Um I mean. Kubernetes calls them pods. It's like 1 or 2 containers that are deployed together and so people wanted to use this sort of sidecar model. Um, where each yeah sorry this is kind of right.

James Munns
So to zoom out real quick. So so like for both listeners mean and everyone else like I am very much an embedded engineer where we like my world is like measured in kilobytes. But I know that we're right now we're talking in the domain of like large scale infrastructure providers like a Google or as an Amazon where who are.

Eliza Weisman
Big servers. Yeah or on-prem people who like Run big data centers. Yeah yeah, absolutely.

James Munns
Yeah, we're managing like yeah, they're managing systems of systems where they're where they're deploying hundreds or thousands or tens of thousands of items and they need some way of wrangling all of these and getting them to talk to each other and configuring all of them and launching them together. So when we're talking at like the scale that we're talking here. We're talking sort of.

Eliza Weisman
Yeah, and well this is where it gets interesting. This is why where you ask to Bo Tokio this is how we get to Tokio um is that ah so like in these these systems are running on like insane servers. You know like you have these like rack-mounted machines that have like.

James Munns
Huge scale 5

Eliza Weisman
Hundred and twenty Eight cores and like Terabytes of Ram and like these really big beefy machines but sort of the whole idea is that those machines are not really executing a single server the way that like in previous models in like 90 s you would have like a server this is the mail server. You know. Now you have like each of those big like rapmounted like servers from hpe or whatever those are running like a million different app. They become essentially each server is treated sort of like a cpu core in the sort of distributed operating system. So you have like you used to have maybe each server is doing 1 thing now you have each of these like application processes that are sort of being treated as though they are being scheduled across all of the nodes in the system and. That's sort of the deployment model of a lot of these applications and this is where um so we're talking about containers mostly? um and we're I mean in a lot of these systems if you are you if like somebody is using like Google cloud or Aws what they actually probably have.

James Munns
So are we talking like virtual machines or containers at this point or a little bit of both. Okay.

Eliza Weisman
Is the hardware belongs to Aws or Google cloud and then on that hardware they are running vms right? that are running Kubernetes and those vms are running your containers. You know like they probably have vms for each customer and but the vms become something.

James Munns
And.

Eliza Weisman
Push down into like that's the service providers way of like segmenting their infrastructure and then at the user level you have containers. Um, anyway, the place that I was trying to get to is so we have written this like Scala proxy that does all of this wonderful stuff.

James Munns
That makes sense.

Eliza Weisman
And you know that people like complain a lot about the jvm yeah jvm um is actually quite fast right? like Java virtual machine performance. It used to be bad people like really used to like trash Java for this. But. Like Oracle and son did a bunch of engineering work on like hotspot the jit and like the jvm um performance in terms of how fast it is. It is it often as fast as native code because everything gets jitted down and it basically is native code. So the jvm actually in many ways is quite good. There's 1 thing that it is extremely bad at doing though. It's good at scaling up right? if you have like a fast cpu Jeff Applications and therefore scala applications pretty good at taking advantage of that. The thing that is absolutely terrible at is scaling down so you cannot take a jvm.

James Munns
Ok.

Eliza Weisman
Like every jvm yeah is using I don't know like sixty megabytes of Ram just for the jvm yeah, you know like because you're running in this in this virtual machine that has like a bunch of code associated with it and then you have to load all of the classes into the Vm and. Jvm programs are just like massive and in in terms of their memory footprint. Um, primarily and there's also this problem of of Gc pauses. Um, and this is where we got to rest and the way that we got to rest is sort of 2 things. 1 of the things is that in these like big distributed systems that we're talking about the absolute most important thing is latency. Um, we care we care a lot less about some of the stuff that you probably care a lot about and embedded. Right? like that. It's very very important for your binaries to be as small as possible to use as little memory as possible but we care massively about latency and where it gets really interesting is that the latency we care about isn't really the average case latency. We care about like. Basically the latencies you care about in a distributed system start at the ninety ninth percentile maybe the ninety fifth percentile like Ninety Fifth percentile is the latency that you care about Ninety Ninth ninety nine point ninth percentile you care about these extreme tail latencies.

James Munns
Mm.

Eliza Weisman
Because of the scale of the system if like millions of people are using like Gmail and you say that like gmail runs like all of these. You know, rendering a webpage for the gmail web ui normally takes like three milliseconds but in an extreme tail case. It maybe takes 5 minutes right you have these like and that that's like very statistically improbable. But if you have millions of people using that application. The thing that statistically never happens is happening like every 5 minutes um

James Munns
Yeah, that's one of those like someone someone definitely I think I'm yeah, that's one of those things that I've heard is is you talk about like 1 in a million or one in a billion events and if you're talking about handling billions of requests per second that means you're going to have one of those one in a billion events every second and.

Eliza Weisman
Yeah. Yeah, yeah, yeah.

James Munns
It's really funny that you mentioned embedded systems because especially for safety-crit embedded systems. This is a huge thing because when you make hard real-time guarantees That's a big thing is that the answer is this should never happen. We actually even have like terms for describing that for like responding to certain events. You'll have what's called the worst case execution time.

Eliza Weisman
Yeah.

Eliza Weisman
Right.

Eliza Weisman
And.

James Munns
You actually have to figure out like literally if everything goes wrong. How bad does it get which is a lot like I guess you know the the fifth ninth of of response time and things like that. So.

Eliza Weisman
Um, yeah, yeah, exactly people in the distributed systems world talk about it statistically instead of deterministically but it's It's very much.. It's basically the same thing. Um. It's that you know at massive scale things that never happen happen every day. Um and they are yeah they absolutely are somebody gets mad. Yeah.

James Munns
I Think that makes sense I mean I would call those systems soft real-time systems like in the same way that video games or audio processing is like no one's going to die if anything goes wrong, but you're going to know when it goes wrong right.

Eliza Weisman
The system is not designed to ensure that everything absolutely happens by a certain deadline. It's designed to ensure that things always happen as responsively as possible. The other thing is that these tail latencies are the latencies that cause outages you know, like if stuff if something is slower than it normally is. And the rest of the system can't cope with that. That's when things start to back up and when things start to back up is when you start to run out of memory because you're waiting for whoever you're talking to to process the the things you want them to process. And oh you have to buffer them for longer because you're waiting you start to run out of memory. Maybe the operating system kills you because you're using too much memory and then oh now that thing is dead and whoever depends on that is like well I'm having a problem because I can't talk to it and that's when these sort of cascading failures that take down distributed systems. Can start to happen so you carbo tailil latency for 2 reasons. 1 of them is that's the latency that makes users mad and you don't want to do that you know, ah 2 it is also the latency that sometimes like anything unexpected is what causes the operational problems.

James Munns
I.

James Munns
Yeah I mean that's yeah, that's one of those that's one of those things especially in embedded systems where like if it's hard to reproduce certain bugs those tend to be the worst understood where if you have something that happens a million times a day you're going to understand exactly like the failure mode and all of those kind of things. But.

Eliza Weisman
The things that don't happen every day cause averages.

Eliza Weisman
Ah, okay, okay.

James Munns
As soon as something only happens one in a million or one in a billion or only under certain loads and in certain problems you get those kind of failures that like you said, if you if you start exploring all of the corners of all of your interconnected systems stuff starts going really poorly really quickly. So.

Eliza Weisman
Yeah, for sure and and okay so this is back to the question. But why rust? um, way way. Did we mention like I don't know 15 minutes ago. Ah, um, the reason so we have this scal of proxy right. And it's actually quite fast. It has pretty good performance. Um, but these these scala proxies when they're actually running they take up a huge amount of memory they're running on the jvm The other thing is that they the jvm is garbage collect so you have these garbage collector pauses. And like the jvm um gc is probably the the best lowest latency gc of all of the gcs in garbage collected programming languages. It's still garbage collected and what that means is that you have latency spikes when the garbage collector is running and you really really don't want that. Um and people. Like big fat proxy that uses a lot of memory and uses a lot of cpu cores. It is designed for this sort of per host deployment model where each of your servers you have one of those proxies running on it every application program on that server. Is talking to that big fat proxy and then that big fat proxy is talking to the same big fat proxy on the server that's like 1 rack unit up from you you know and then it's. All of the traffic is going between those 2 proxies and then they're distributing it to all of the other processes on their node and so that's like one deployment model. Sorry um, but the alternative deployment model and the one that people really started to want in this space is one where. Each of those instead of having this this sort of centralized big per host proxy. You have in smaller individual sidecar proxies and these are running next to each of those application containers and the reason.

James Munns
Okay, so you said sidecar twice and this is a phrase that I've seen before but I have no idea what a sidecar is so.

Eliza Weisman
Yeah, in this case that is sort of a that's a Kubernetes term. Um I think that it it may be used in other systems. But basically what that means is you're telling the scheduler every time you start one of these containers. You also start this other container and they.

James Munns
Okay.

Eliza Weisman
Our buddies. You know this container runs right next to that other container and they're part of a single Kubernetes calls this a pod which is sort of like a deployable unit of a thing and that's sort of like the abstraction of like what it schedules and it schedules them together. All the time so you're saying like I want this demon to run next to the application server. Um, and the reason that you want that. The big reason you want that model is for security reasons or security and and this sort of concept of 0 trust networking.

James Munns
Gotcha.

Eliza Weisman
Which I don't know this is I This honestly my plan was not to come on the show and talk about anything I do for my day job and yet here we are. Um, yeah yeah.

James Munns
I'm excited to to hear the things that people are excited about so when you say 0 Trust that's that's a phrase I've heard in a lot of different contexts and here in 0 trust ah networking does that mean. These live next to each other so their conversation can be secret between the two of them and the whole world doesn't need to hear it or is there another meaning for zero trust and.

Eliza Weisman
So the main thing it means is that this is also sort of a way that the world of of like networked server applications has changed since I don't know the 90 s or early two thousand s which is where. In in that sort of earlier era you have this idea of like perimeter-based security and that's where you have everything that comes into your data center comes in through this firewall you know and that firewall knows who's good and who's evil and it maybe terminates tls. Right? So it has a certificate that's like here's the the tls certificate that was issued for like migrate website dot com and it sits right at the front of the data center everything that comes in is like you have these encrypted connections coming in and that big. Ingress proxy. That's also a proxy there. This stuff is all proxies distributed systems proxies all the way down. Um and you know and they all do different things and so this yeah you have a right.

James Munns
So this is like this is like the medieval town these are like City gates where you say the stuff inside the City gates totally say if I can trust it but we check everyone at the border who comes in and out and we make sure everything's good at the border. So.

Eliza Weisman
Right? And the other sort of critical thing is identity um is that like tls right? You don't you have encryption but you also have identity you have some like when you get the little lock in the in Firefox or whatever the little lock icon. That means not only does it mean this connection is encrypted but it also means when I did a handshake with the server they sent me a proof that they have a certificate and that certificate has some key material in it that shows that it was signed by a certificate authority that I trust. Um, and that means that this server that I'm talking to not only can no one else sniffing the network read the the messages that we're exchanging but it also means that I I have reason to believe that I'm talking to a server that actually represents http://google.com or whatever. And of course like that's a human abstraction and the way that you trust it is that these these cas are just like there's like 7 companies that issue root certificates and you trust them just because there's not a lot of them. Um, but still sorry I that is a spam call.

James Munns
Noise.

Eliza Weisman
Um, so so you have this notion of identity too and the reason that that sort of matters is that um well I mean did there's 2 2 functions of encryption here to ensure no one else is reading their messages but also to ensure you're talking to who you think you're talking to.

James Munns
I mean.

James Munns
Yeah I run into this with embedded systems too because especially when you have embedded systems like think of your like home router if you want to have an Ssl connection to your home router. That's actually really problematic because there is no like you said the human abstraction of the url like I am proving that I'm talking to this url.

Eliza Weisman
Ever have. Right.

Eliza Weisman
Um, yeah, right.

James Munns
But on your local network. There's no http://google.com because Dns is outside of your network and so like getting something like a secure connection over wi-fi to your ah your wireless router is actually really challenging from an embedded systems perspective because you can't ask a c a to be like is this one nine two 1 6 eight zero one

Eliza Weisman
Ever And then.

Eliza Weisman
This is they have exactly the same problem inside the data center literally exactly the thing you have described and this is what this idea of 0 trust networking is about.

James Munns
Because everyone else has one of those in their home network and so how do you prove that This is the one that I'm expecting to be talking to and I I imagine that's got to be the same when you have these.

Eliza Weisman
It's saying all of the workloads within the perimeter. They all have cryptographic identities and there's a cluster ca that issues cryptographic identities and says this workload actually is who who they claim to be. And all of the connections inside the cluster are encrypted so if like 1 of those microservices is compromised somebody finds like some security hole in it and sends it like some. And somebody gets rude on that machine. They can't read everything else that's going on around them because the whole cluster treats. Everyone else in the cluster as though it's mutually untrusted and that's yes.

James Munns
So you're running like a miniature Ca inside of the data center that says when you spin up this container. Okay you I now authenticate for some limited amount of time that you are Identity X and I am introducing Identity X into the neighborhood and until this time out in a day or whatever.

Eliza Weisman
Yes, precisely. Yeah yeah, yes.

James Munns
You're allowed to trust this cryptographic public key as whoever it says it is and.

Eliza Weisman
Right instead of everything inside. The data center is plaintext and everything coming in from the outside world is encrypted So that's this notion of 0 ero-trust and in this like 0 trust world. You have these proxies if the proxies are responsible for the Tls. Right? for responsible for maintaining or establishing and maintaining the encrypted connections which you want because all of this security stuff is kind of a pain and like application developers don't really understand it all of the time and they want to focus on like doing web backend stuff that I personally don't give a shit about.

James Munns
I.

Eliza Weisman
Like I don't know like they know how to write sql queries that are good or whatever I e have never written a sql query in anger in my entire life I don't know about web app stuff. Um, but I do like I know some things about tls and like how to do it correctly and also we want to have. Like this ca that pushes key material to these like different application processes and we want to do that in a consistent single like plane of of control way so we want to have the proxies do the the tls and the reason. That we want to move away then from this like per host model to a sidecar model is that you want um you want the the trust boundary for that key material to be like the individual application workload and not the the machine in the data center. Because sort of the whole idea of the cloud is that the machine in the data center is an implementation detail that you don't actually care about you. Don't say there's a ah cryptographic certificate for like the machine on rack 56 row 7 or whatever you say there's a. Cryptographic identity for the user's service or the profile service or the widget service or whatever and if you're doing that you need the key material to stay within the thing that actually has that identity and that thing might be.

James Munns
And.

Eliza Weisman
On any number of servers on any number of rows in different data centers. Um, so you really yeah.

James Munns
Yeah, you want to scope it as small as possible. So that basically the damage control. So like if if that gets damaged. You know that they've only um, exploited like you said the the user identity server but not the credit card server or or those kind of things that you're keeping sort of the.

Eliza Weisman
Right.

Eliza Weisman
Yeah, that is a big part of it. The other thing is that you also want these identities to be like semantically meaningful. You want it to mean something in the like in what the application is doing and not. It's the key for this particular piece of hardware.

James Munns
Blast Radius for for these kind of things as low as possible.

James Munns
And.

Eliza Weisman
Because that particular piece of hardware might be doing 1 of 50 things. It might have like all of these containers might be running on the same box and then like some of them might get rescheduled somewhere else and now that box is doing something completely different. That specific you know and then that piece of hardware probably dies. That's the other thing that happens at scale is hardware fails like on a daily basis because these once in a million events happen a lot when you have a million servers. So like that that machine might get deraced and replaced with something else and that identity is meaningless.

James Munns
So you're gotcha So you're you're identifying the person doing you know in my very metaphor you're identifying the person who's doing the work rather than the address that the person is residing at but whereas that's sort of the more traditional. Yeah, so that's like the traditional model you say as long as the address is within this bubble.

Eliza Weisman
You want the identity to refer to the workload. Not the hardware. Yes, right? because I might move.

Eliza Weisman
Yeah.

James Munns
We're good whereas now because you can have people shuffling around to working in different places that's sort of a meaningless assignment nowadays so you have to have this sort of proof of who you are and what you're doing tied to the individual rather than the location I.

Eliza Weisman
Yeah, yeah. Right? So the scallet proxy that uses like 90 to a hundred megabytes you know in a low traffic scenario. It's not really under load. It's just sitting there. It's just loaded all of these like java class files and oh suddenly it's like a hundred megs that sucks.

James Munns
Yeah, so.

Eliza Weisman
When you want to have one of those for every single container in the system. It's fine if you have one that runs on each machine like one hundred megs isn't a big deal when you have a machine with like five twelve gigabytes of Ram that doesn't matter. But if that machine. Yeah.

James Munns
So I was going to say a silly number and it was lower that I was going to say like a silly number like 64 gigs of Ram and then I realized that you're talking about rackmount servers fair I'm still running 16 gigs on my laptop and feeling.

Eliza Weisman
Um, my desktop pc my desktop pc is sixty four gigs of Ram and I barely use all of them. Um, yeah, yeah, yeah, and nobody nobody needs that much ram unless you're running hundreds of containers.

James Munns
Luxurious and.

Eliza Weisman
Which every single rackmount server is running hundreds of containers and every single rackmount server if each of those containers has like a hundred to two hundred I don't know maybe even like under a lot of load maybe five twelve megs of of Ram for each of those proxies. That suddenly sucks a lot. So the 2 things you really want to get rid of are like that high cost of running Jvms and you want to get rid of the the gc pauses that you get because you're running in a garbage collected environment. Um, and you see.

James Munns
Yeah I imagine those pauses like you were saying like I was the the mental model I had when you talk about this cascading failure is is when people like pump their brakes and traffic is that 1 person pumps their brake. The person behind them does and then you get this five mile pile up of cars behind them because one person pumped their brakes.

Eliza Weisman
Um, yeah exist.

Eliza Weisman
Yeah, and somehow it takes down like a root dns server and now like your whole thing is just fucked and like that Facebook outage where they had to because they put their like door control system was like also hosted on the same infrastructure as the web app for some reason.

James Munns
Once Like. I.

Eliza Weisman
They had like a guy with an angle grimder come in so they could even get into the data center they had to like cut the lock off the door and when you do that. That's that's not fun. So the gc pause and the Rss the resident set size. Um, and these proxies have to be really small now they have to be really low latency. More importantly, they have to be predictably low latency. We would actually happily take another three you know like another like 3 Ah milliseconds in the in the average like 50% case in exchange for bringing the ninety ninth percentile closer to the 50 percentile we would rather make it a little slower nobody notices a millisecond. You know we'd rather bring it down. We'd rather actually trade that like. Common case performance for making the worst case closer to the common case but you know it also needs to be fast. Yeah yes.

James Munns
Yeah, that's one of those things that broke my brain when I started working in hard real-time systems is is like you will use different algorithms that have more predictable more predictable behavior because like you said you'd you'd rather it always take five milliseconds

Eliza Weisman
Yeah.

James Munns
Then it takes half a millisecond 99% of the time and then takes a second that other time because if you're if that's on like your critical path if you're if you're talking about it like on the critical path of like you stick your arm in something and a sensor is supposed to detect that so it turns the blades off like.

Eliza Weisman
I Have screwed this up sometimes.

Eliza Weisman
Right? Yeah, yeah, yeah, absolutely.

James Munns
You don't want one out of 100 times that to take a second because your hands already in the blades at that point so you'd much rather like like I said it in like aviation and stuff like that you'll throw twice as powerful of a cpu at it to just go. Okay, it's always going to take five milliseconds but we need it to take 4 Okay well you know put a bigger cpu in it and it'll.

Eliza Weisman
Bright.

James Munns
Cost a buck extra but we now know that this will never take more than four milliseconds or something like that. So.

Eliza Weisman
This is this is a very very similar problem domain. You don't care about that as much for the actual application services but you care about it immensely in this proxy layer that all the traffic is going through the other things that.

James Munns
Yeah, it's like when it's like when people talk about high performance High performance is one of those like words that means something I say nothing but it really means a lot of things to a lot of different people whether you talked about throughput or Latency or um, resource usage or or all of those things can mean like you said.

Eliza Weisman
Yeah, what does that mean? Yes, absolutely.

Eliza Weisman
Um, yeah, um.

James Munns
Jvm's great for things like throughput because your average case is lovely. But like you said, if you're if you're really worried about Latency then that becomes sometimes an entirely different area of research and.

Eliza Weisman
Right? Well latency sort of is like the inverse of throughput or throughput is sort of the inverse of latency but they they tell you very different things when you're looking at latencies statistically you know that's something that's something very different. And it's easy to lose these like extreme tail cases in throughput right? where you say oh you know this does like a bunch of requests per second that's fucking great but like 1 of those requests takes like 50 times as long that's not as great.

James Munns
You are you are you saying we should ah eliminate Spider's georg from the from the statistical analysis.

Eliza Weisman
Yes, Spiders gayorg is in fact, like if if well here's the thing if you actually think about this this statistics spiders gayorg and like how many people in the world. There are how many spiders gay orgs are there. Actually you know.

James Munns
So well if they're one in a billion then there's going to be at least 7 of them out there.

Eliza Weisman
Yeah, right, there's 7 guys. So so we care a lot about spiders gayorg and his spider consumption because you know in in this world. You're actually going to meet that guy like every day. Um, this is sort of a strained metaphor. Anyway, that's how we got into rust. Because we needed to we needed to make these proxies smaller and we needed to eliminate garbage collection. Ah because there's there's really no way to get around the gc pause whether you write it in go or Ruby or whatever and we're not going to write in ruby for obvious reasons. Um, you absolutely have to eliminate that. And our options were well. We could all learn c plus plus or we could learn rust and we want to make a lot of promises about security because that's one of the big value adds of this software is that it's managing encryption and that it's managing like auth policy and who can talk to who. Is absolutely critical that this thing be like extremely secure. We're not going to learn c plus plus we're going to learn rust and at the time at the time when my company first started like looking at rewriting this scholar thing in rust and making like this whole new.

James Munns
So for reverence when was this so.

Eliza Weisman
Whole new proxy. This was like um this was around when I started and actually one of the big reasons that I got the job that I have now was that I had learned both Scala and rust um and like could read what I was at least like passingly fluent in both of these languages out of college because I was sort of. Programming languages nerd and I just like learned a bunch of weird programming languages that they don't actually teach you in college. Um, this is this is the company where I work was founded I believe in ether 2015 or 2016 I started around 2017 so about a year in

James Munns
So is this is this after 2015 or

Eliza Weisman
And that's when we're starting to invest in Rust and at the time the Rust Async networking world was just sort of starting to become usable. Um yeah I believe I think.

James Munns
Yeah, because 28 ish is when async landed right? Fox it was for the 2018 addition right.

Eliza Weisman
Maybe 29 yeah um I I think that the async keyword was reserved in Rust twenty eighteen I don't think that it was stabilized in rust 2018 if if memory serves I'd have to check.

James Munns
Um, okay, it's been a while I mean.

Eliza Weisman
It has been a while. It's been a couple years now but this was before asyncowaite this was way before Asyncwaite I definitely worked at buoyant for like 1 or 2 years before asyncwait um, and at that time this ecosystem is like rapidly growing but it's really not there. Um, and. So like I worked actually like I used to work with Karlerka from Tokio um I still work with him but he no longer works for my employer. Um, and so we invested very very heavily in all of the libraries that we needed to use to write this thing and continue to do so and that's kind of a big percentage of. My time goes into Tokio and tracing which is the diagnostics library that I kind of wrote. Honestly um I don't like to to tip my own hat for writing the whole logging library. But yeah, it's that in particular is kind of my um.

James Munns
Um, tracing is cool beans I mean definitely like it's.

Eliza Weisman
Is a bunch of stuff. It's one of those things for me every time somebody says oh it's great. All I can think of are all of the things that I wish I had done better or that I wish I could fix or that I want to add but it it is always very gratifying to hear that from everyone else.

James Munns
So.

James Munns
I Yeah honestly anytime you put up a new release or like a new demo of like I remember a while back I I think it was you and someone else were working on basically like ah, a top equivalent but for Async task So in the same way that you'd you'd monitor.

Eliza Weisman
Anyway.

Eliza Weisman
Yeah, yeah, yeah.

James Munns
Operating system tasks you could look at all of these ephemeral Async tasks that were going on and seeing what your system is doing because this is one of those like at a certain scale. Ah, whether you're talking about virtual machines or containers or things like that at some point you just need to statistically wrangle all the stuff that you're doing and when you when you're getting to the point where you're.

Eliza Weisman
Enough.

Eliza Weisman
Right.

James Munns
Single piece of software can be spinning up thousands of individual working tasks at the same time you've got to figure out which one's causing problems.

Eliza Weisman
Um, well I think even if you're yeah, you're talking the thing you're talking about is Tokio console. Um, which is sort of 1 of the projects of the the Tokio team um that we would really like to um. Make it a general purpose tool that you can plug into even like some of the um embedded focused async runtimes someday because you're definitely right that this matters a lot when you have like these very large numbers of tasks. But I think that it just matters in general because in this async world. Scheduling is something that's happening inside of your program instead of at like the os level and so and it's cooperative scheduling. So the tasks are are saying hey I want to yield now instead of the operating system going. It's time for you to stop. Um, and because of that there are like a bunch of bugs that you can introduce by writing bugs in your code. You can introduce like scheduling behaviors that are maybe not what you want and in a way that you can't really when you're programming with threads and this applies in the world of like the big. Giant network applications where you can't use threads because every thread has a stack and those stacks take up too much memory and you can't handle like 10000 connections that way or in the embedded world where you really don't have any notion of concurrency because you have a single core microcontroller that has like 8 megs of Ram. But you need some way of having different things happening because you spend most of your time waiting because this is one way that these worlds are very similar is that when you're talking to anything on the network whether it's ethernet or I two c or whatever you spend a lot of time waiting for stuff to happen. And you don't spend that much time doing math. Um, yeah.

James Munns
That's one of those things that I had to teach like when I was teaching rust that was one of those things that like people always wanted to learn about Async and it was funny because I almost always spent very little time on Async and a lot of the time that I spent teaching was more about how to think about async.

Eliza Weisman
O.

James Munns
And like 1 of the first things that I was led with was it's important to understand the difference between concurrency and parallelism and my my like my short explanation for that was ah parallelism is about working on many things at the same time and concurrency is about waiting on multiple things at the same time where.

Eliza Weisman
Yes.

Eliza Weisman
Um, ah was it you that said that because I have always okay well I got it I got it from someone else too.

James Munns
For a microcontroller. Oh I got it from someone else I got it from someone else. Okay I certainly propagated. Yeah, it's one of those things where like unembedded That's one of those really important things because when you talk about it a single core microcontroller. You can't.

Eliza Weisman
And I've always said something I heard someone say was this and I thought that was really insightful. Yeah.

James Munns
Work on multiple things at the same time but you're going to be waiting for a button press and a network packet and an ledb to be done drawing or a screen to be done rendering and that's one of those things where I find rust is interesting because it helps sort of that weird wraparound of high-performance computing to embedded systems where.

Eliza Weisman
Exactly.

James Munns
I was talking to someone on Twitter about this today where it was in embedded systems. You have to be really careful about what you do because you have nothing you you just don't have the resources to do a lot but on high-per performance computing or high-per performanceance servers and things like that.

Eliza Weisman
Bright.

James Munns
You have to be really careful with the resources you use because like you said there could be thousands of instances on exactly the same machine and you end up running them to the same problems.

Eliza Weisman
Um, yeah, you're just yeah, you have a disgusting amount of resources to use. The problem is the amount of stuff you need to do is even more colossal.

James Munns
But you just have a tiny shard of it though. Yeah.

Eliza Weisman
So you really you end up having exactly the same problem. It's just that one of them involves a lot more statistics like.

James Munns
Yeah, yeah, because instead of like 1 How bad can he get you go? Okay I got a thousand of these little gremlins that I need to take care of any 1 of them can cause a problem for me if they decide to get unruly whether they just won my my 1 gremlin can get rowdy. But it's funny to listen to you describe.

Eliza Weisman
Um, right? yeah.

James Munns
Systems like this because like operating systems are wonderful because they give you a standard middle of the road. Wonderful way of handling things where as a developer you don't have to think about I don't have to write my own file system I don't have to write my own network driver just give me a packet or give me a file or give me a a thread time and things like that and.

Eliza Weisman
Better. Ah.

James Munns
Embedded systems especially Bare metal embedded systems are they're really just programs that are operating systems because when you have to do multiple things you schedule them yourself because you don't have an operating system or you can't afford an operating system so you end up building just the bits of an operating system you need whereas when I hear you talk about servers.

Eliza Weisman
Exactly.

Eliza Weisman
I have ever.

James Munns
You're talking about user land scheduling and you're talking about user land drivers and even I've seen like what is it high- frequencyquency trading folks who will write their own user space networking stacks because they need to squeeze that last point zero one percent of of latency out because that means they make an extra million dollars this month or something like that. So it's.

Eliza Weisman
Yeah. Um, Boom. Yeah.

Eliza Weisman
Yes.

James Munns
It's so funny that we've wrapped around to the same. Don't worry operating system I'll run the world for you world. But it's just on completely different ends of the the spectrum.

Eliza Weisman
Ah. So I have 2 things to say in response to that observation which I think is extremely insightful. 1 of them is that well you're absolutely right? and like 1 of the things that the people working on things like systems like Kubernetes these distributed schedulers is that. People like to say that something like Kubernetes is an operating system for the whole datacent right? that it's really doing exactly the same things an operating system does. It's managing access to limited resources. Its scheduling processes. And it's sort of ensuring that no one can do things that they're not supposed to be able to do right? Those are like the operating system's 3 jobs except that it's an operating system that's not for 1 computer but for a whole massive building filled with computers. So that that observation is absolutely correct. Um. The other sort of question when you you were saying like oh people writing user space network stack. Do you ever heard of dpdk dpdk is a very cool library from from Intel that I'm kind of sad that I didn't actually get to use.

James Munns
It doesn't ring a bell.

Eliza Weisman
Um, we sort of looked at using it for for linkerd and then it turned out that it it wasn't really friendly with the containerized world. But it's a ah kernel bypass networking library. Um, and what it basically does is if you have like specific intel nics you can like expose all of this like very low-level nic operations to user space software so you can do like I'm going to write out a tcp packet and I'm actually not going to do any context switch to do that. Um, you can do like dma of like nic buffers directly into user memory.

James Munns
M.

Eliza Weisman
And maybe you do like 1 syscall to say hey I want to be able to do this right? And once you've done that syscall you never have to talk to the os again and we look yeah exactly right? We we sort of looked into using dpdk and trying to.

James Munns
Um.

James Munns
It's like a mutex lock you you lock the mutech Once you get exclusive access and then it's your shenanigans until you're done with your shenanigans. So.

Eliza Weisman
Bind it to rust actually quite early on I think back in like 2 17 it turns out that it was not really easy to do this in the like heavily containerized cloud world because it really relies on like direct access to like you got to actually have one of the like 3 like enterprise Intel Nics and like you maybe do have that and in your server but you're like running in a Vm on that server and maybe that Vm has another vm in it and in that Vm, you're in a container and by that point you have no idea which like Nick you have. And also maybe the application gets scheduled on a machine that has like a different k neck from a like a broadcomni or something that's also like a big enterprise nickck but it doesn't work with dpdk. But I think that like the hft folks are using like this kernel bypass stuff. Ah very heavily.

James Munns
So yeah.

James Munns
M.

Eliza Weisman
Um, and I think I've always thought it was very cool and this actually gets into um one of my sort of spare time interests which is like my my first love My first love has always been operating systems. Um, actually ever since I was like just a little kid I've been interested in operating systems wait like probably like.

James Munns
And.

James Munns
Um, yeah I feel you.

Eliza Weisman
Younger than most people are aware of operating systems. Um I was a nerdy kid. Um, yeah I played a lot of like um I remember being a kid and I loved like simcity and like railroad tycoon and those kinds of like infrastructure games. I've always loved infrastructure. Um, and I Yeah got you? Oh we We We could have been friends as kids. Um, yeah I mean same.

James Munns
Um, I So was em so lemings and Duke nur for me I probably would have known my computer I.

Eliza Weisman
Right? That's that's where I'm going with this and so I love these games I remember I had a friend who was also like a very nerdy kid who loved trains and and we were like hanging out we were playing um railroad tycoon we were having a great time and he was like oh I'll burn you a Cd right of railroad tycoon. Um. And so like you can play it at home and then like we can hang out and talk about okay so he burns me a Cd and I'm I'm maybe like nine or ten years old um and I go home and it turns out um my family all of the computers in the house are max. Um. My dad in a sort of past career was ah a graphic designer so he like was first introduced to computers on like the early Macintosh and so my my family's always been a macintosh household I have the Cd and then I have like some of my other like Matt games that I like to play you know and I take this cd and I put in my computer and. Um I don't get railroad techcoon. What I get instead is like a whole bunch of files that I've never seen before and I don't understand right because it's a windows version of railroad tacoon. Um, and that was when I learned I was like a lot of kids would have just been like frustrated and then given up you know. For me this was like the most fascinating thing I had seen in my entire life. This blew my mind. Yeah, but also it just like it revealed to me that there's this whole world of stuff that's going on all of this infrastructure.

James Munns
That someone has put a challenge in front of me.

Eliza Weisman
Right? And I'm fascinated by machines and how things work and complex systems and I'm like oh this is like a very fascinating system that happens to have gotten in the way of me playing the game but then I like just spend all of this time like looking at all of these weird Files and I think I open some like windows executables on my mac and they open in like. A text editor and they just look like garbage and this is like magic to me this cracked my brain open and ever since then I have been like really fascinated with by operating systems and like I remember being a college student that was like my favorite class in college and I just like um I've always wanted to do like Os stuff. And so I Love my job working on a bunch of cool things that in many ways gets kind of close to this space. But my my like first love has always been I Want to write an operating system and I actually specifically want to write an operating system for the desktop computing use case.

James Munns
Ok.

Eliza Weisman
Which is the one that like no one is ever going to write a new operating system for right because like the hardware is pretty standardized but there's so much of it and so the like the cost of getting started is like very very high and there are now like some of these experimental Os projects or like. Even not just experimental but like new operating systems are being written for like for embedded platforms. Um, for like some of the sort of in between embedded and and real computer platforms like phones right? like you have Android Ios or sort of like these. And but even even those systems sort of have like like the ios Kernel is like mock right? which is the same kernel as as Mac Os and Mock was like a ah research project from some University from many many years ago that just sort of has had more and more stuff glued onto it.

James Munns
Um, yeah.

Eliza Weisman
And I think that kind of sucks. Um I think somebody should just like write a totally new experimental operating system that like all of this stuff dates back like like kernel technology has has changed a bit since the 90 s but it's it's kind of the same. Um, and you just kind of keep piling more and more abstractions on top. But the like fundamental thing has not really ever been just like radically reevaluated and that's kind of always been my like my my first love and I have this hobby project. Like obviously none of us are ever going to be running on our pcs because it's like my hobby project and I work on it about like one weekend every month I have the time to like actually hack on it. Um, but that's sort of it in in mycelium. Yeah.

James Munns
So that's Mycelium Mycelium Mycelium Mycelium. Yeah.

Eliza Weisman
I've heard it pronounced both ways. Um, so I think I think you can I've actually heard like a mycologist pronounce it mycelium. But I've also heard a mycologist pronounce it Mycelium So like um, yeah, right? but.

James Munns
Oh nice, That's one of those things that breaks your brain with the internet is everyone's like oh no, it's pronounced like this and then you're like well it's a Latin word. It's pronounced like this and then you get someone else who says oh, but.

Eliza Weisman
Also we don't actually know what real Latin sounds like because we only know what church Latin sounds like in Church Latin is like different from Latin as the Romans spoke it so who knows it doesn't Um, but yeah in in the in this sort of glorious ideal Post-revolution I Actually like I love my job a lot. Um, if we live in this world where like.

James Munns
Yeah.

Eliza Weisman
We have universal, basic income in this like hypothetical post-carcity future I would work on Mycelium full-time but I actually really do enjoy what I do for my day job. With that said, this is what I would love to spend all of my time on.

James Munns
So.

Eliza Weisman
And I think that that would be the only way that it would get to a point where people would actually run it on their pcs.

James Munns
So you mentioned you really like the idea of radical reimagining. What does it? What is your like I can tell you so I'm working on a little os problem too and I can tell you what like my radical reevaluation was but I'd love to hear like what was your.

Eliza Weisman
Um, well I know you are.

James Munns
No damn it. We're going to do it this way in myos like what was your that.

Eliza Weisman
Yeah, well we came I thinking about some of the stuff I know you're working on I think we have come at it from very different directions that I think are both really interesting. Um, like I'm building mycelium I'm targeting primarily. Um. X 8 6 64 bit um so I'm just saying I'm not going to think at all about the hardware I'm going to assume we're going to all use the same Intel hardware that I already have in my house. Um, and someday I'd like to target um like arm desktop cpus as well as um, risk 5 someday. But I haven't really written like the hardware abstraction layer for those systems and I have an x 8 6 machine and I would like to be able to run my operating system on it. Um, but the thing that is like ah there are a couple things and 1 of them is I remember being a college student taking operating systems course. And the professor sort of is telling us about monolithic kernels and he's telling us about micro kernels and he's talking about all of these different ways that micro kernels are just better in every possible way like from an engineering standpoint this is like just a much smarter and much more elegant way to design the system. And so I'm like okay professor like I raise my hand I'm like what alpert. What? like commonly used operating systems today are micro kernels and professor goes. Oh none of them are like absolutely none of them. They are all yes.

James Munns
Micro Kernels Microernels are the graphene of the computer science world. They can do anything except for leave the lab.

Eliza Weisman
Right? Um, So so Micro Knels like true Micro Kernels have never been tried right? Is it. It's like like true socialism has never been Tried. You know there is no I Guess maybe the closest thing like G and you heard never went anywhere. Um. Mock sort of started out as a research Micro kernel. But then like when it became the Macos Kernel like most of the stuff was moved back into Kernel space to make it a monolithic kernel. Yeah right? so.

James Munns
Um.

James Munns
So so for the folks who aren't familiar the the difference between a macro kernel and a micro kernel. How would you like delineate those to at least from a purity standpoint.

Eliza Weisman
The idea is that the the fundamental ideas that you have all of these drivers right? and a kernel a kernel is doing a few things. It's process Scheduler. It's providing some abstractions like for interprocess communication. Um, it's providing a system call layer stuff like that. It's also managing. User Programs accessing hardware right? and those are sort of the jobs of the operating system and one of the problems with hardware is that it turns out there's like a shitload of it right? like the world is full of hardware and like ah it turns out and it turns out that like a bunch of people make hardware and all of those people that make hardware make a bunch of.

James Munns
It turns out.

Eliza Weisman
Different devices and you know we have all of these nice standards that make like every hard drive sort of seems like every other hard drive every graphics card I don't know you plug a cord in the back and plug it into your monitor just sort of fucking works. Um, but drivers are the software that actually makes that happen and. The way that you write a driver is you get like a big 3 ring binder from a hardware manufacturer and it says like here's how you talk to the hardware and then you sit down and you like drink a bunch of coffee and you write all of this like code that just does like these weird incantations that make the hardware work. Um, and then it turns out that right.

James Munns
I.

James Munns
Just describe my job first.

Eliza Weisman
And then it turns out the it's the 3 ring binder from the hardware guys that actually lies um and so then you have like um one of my favorite I think my favorite comment in all of linux. Um I don't know if you've seen this. It's for um, like the driver for a specific real-time clock.

James Munns
Yeah, yeah.

Eliza Weisman
Um, and it turns out that like this is like ah like a multi-paragraph comment. That's just like in some c file in the linux kernel and the comment is essentially that like um, something about how like you know there's the gregorian calendar and then there's the Julian Calendar and then there's the like whatever the name of the hardware manufacturer calendar is which is like different from the gregorian calendar because they got like so I think that they like got the order of the months wrong or something or like 1 of the months has too many days.

James Munns
Um. I.

Eliza Weisman
And it's just like impossible to fix that because this is all like implemented in silicon that you can never change and so a bunch of Pc Motherboards just have this real-time quark that like the manufacturer documentation says that it just gives you the correct date but it turns out that if it's a certain month that just actually doesn't give you the correct date because they fucked it up.

James Munns
And now they can't change it because it would break someone's code that has the driver That's yeah.

Eliza Weisman
And there's like no way for them to fix it. Um, because like right break every other operating system that does this and like they already made like the the masks for doing like lithography to make this thing and it's just like well you it's impossible to change now so now linux has to handle the like Gregorian Calendar and also though like whichever hardware manufacturer calendar and you're just stuck with this.

James Munns
I had I had this so like like the hardware that I'm working on is is Nordic it's the n of 52 love their chips but like anyone else they have these hardware errata that you're talking about where like.

Eliza Weisman
You right.

James Munns
Supposed to do something and and it does not but they've already made a million of these chips and it's not like you firmware update the silicon because like you said it's lithography. It's been etched into the silicon like what are you gonna do um and they have 1 Ah so they have this q spy which is like the way you can have an external memory chip and.

Eliza Weisman
Yeah, yeah.

Eliza Weisman
Right.

James Munns
There's this functionality called X I which is execute in place which says like hey you can read from this external flash chip as if it was the built-in flash chip and yeah, occasionally you'll have to some latency from when you're pulling from it but like other than that we'll map it to your address space. You can treat it like it's local storage. It's wonderful.

Eliza Weisman
Other.

Eliza Weisman
And of earth.

James Munns
But they have this arata like I was loading a program and I was doing something like I was reading I was I was doing like a Crc on it or I think I was doing like a cryptographic signature on it to make sure that it loaded correctly and I was reading from it and the.

Eliza Weisman
Even right.

James Munns
The signature was loading correctly, but the signature that I calculated in the memory was wrong and I was like that's weird like did I corrupt my memory or something and then I went in like in a different way I dumped the memory recalculated on my desktop checked out totally fine and I go that's weird was troubleshooting that for like two days and then I went and found and they say.

Eliza Weisman
Oh boy. Ah.

Eliza Weisman
Um, yeah.

James Munns
Oh if you do a branch operation right? after you read from x I p the the cache will be wrong for 3 cycles. There's there's like a delay slot that the hardware doesn't handle so it read like it just basically while it was reading this.

Eliza Weisman
Oh God Oh there's a delay slot right.

James Munns
16 or thirty two kilobytes of programage. It just hiccuped and cryptographic signatures do not like hiccups they they go? Well no, that was not the correct value but this is one of those things where I like beat my head I was like did I do the unsafe code wrong did I do this wrong did I configure the hardware. No just don't hold it that way.

Eliza Weisman
Yep, right? and. Yeah, yeah, it turns out that there's just a hardware bug and the hardware bug is impossible to fix. So the way we fixed it is we put in the documentation. So say you know don't do the thing that trickers the hardware Book. Um.

James Munns
Is very much like yeah yeah.

James Munns
Yeah, which is really annoying when the thing that you bought the chip for is the thing that they say not to do a lot of the times and.

Eliza Weisman
Right? Yeah, this is like 1 of the classic like um, like just dead stupid x Eight six things x x Eight six is filled with like just dumb shit I think largely because it's been around for a very long time was like. 8086 was like the first like Vlsi like microprocessor on 1 chip. Um, it's been around since the dawn of time and all of the like dumb shit has like just accumulated um and that's why it's like by far the worst instruction set architecture that people still use.

James Munns
Hold on I could go on and on about x Eight six but I still want to hear what your what your claim to differentiation before we get too deep. You mentioned you have I want to? yeah I want to know about your operating system because I know how cursed deck p six is but.

Eliza Weisman
They're yeah oh you want to go back to mycelium. Yeah, okay, right? Yeah so so there are a couple of things that I want to do with mycelium. Um that I think are kind of fun. And 1 of them is okay so I'm this college kid and I'm hearing about microvernals and how they are like virtuous right? And how in the like ideal like. Someday after the revolution when we're all like beautiful and wealthy. We're going to have these microcurernel operating systems that are going to be so stable. They're like your computer is never going to crash and like ah a driver bug cannot corrupt operating system memory and like all of these like wonderful things and it just seems like ideologically pure. And I think that it is and meantime we have gotten operating systems that are now like much more stable like I have never in the last like 105 years I've very very rarely seen a kernel panic. They've all happened on Mac Os as a side note um. Specifically the like Apple I O h the I kernel extension ah has like a weird bug in it that sometimes when you bring your macbook up from from sleep if you have the wrong Macbook the whole kernel just crashes. Um, but that so that has afflicted me.

James Munns
Oh cool. Oh.

Eliza Weisman
But besides that like you don't see these like blue screen of Death Kernel Panics happen nearly as much as you used to um and I think that they have fixed these or like reduced the frequency that these things occur right through just like getting better at engineering computer scientists hate. That you can solve problems by getting better at engineering. It's sort of like um, you know, computer scientists hate that like well there are some advantages to using a link list right? Um, and there are like advantages to using like an array based list. Um, and if you use the link list. There are like things that you might get.

James Munns
Um.

Eliza Weisman
And that it might actually be better in some ways and like oh I wrote the like um, there's ah, a fun paper that I found like just browsing through like archive which is called like um, resizeable arrays in optimal time and space and it's like implementing like a vac type. Um. Where you have this resizeable array and they have this like proof that their design which you do like a bunch of math every time you like resize the Ray and you the array and you allocate new chunks by doing all of this math. Um and they have this proof that's like this. This very cool algorithm that we came up with like minimizes the number of reallocations to grow the array right? So you spend less time allocating and you spend less time like mem copying and it's so much better and um I wrote this I like implemented this paper like exactly the way that it says to in the paper. Um I wrote a bunch of benchmarks that compare my thing with like the rust standard library vc vc is always faster. Um, and then I like took all of the moonmath out right? I commented it all out and I replaced it with like um, some some well I replaced it with like some bit twiddling tricks. You know.

James Munns
If double or something like that. Okay.

Eliza Weisman
Um, because I realized they're like okay they're doing all of this stuff but actually you can just do like binary log two and it's almost the same. Um I replaced it with that. My thing is now like only like 10 percent worse than standard library vac. It turns out that it's just impossible to ever beat vck because um, even even if you were pushing a bunch and it has to grow a lot because like putting in an extra pointer. Do you reference that you have to do to push like actually just kills you every time.

James Munns
Is it just cache like is that just one of those like order of magnitude between L three and main mem.

Eliza Weisman
There's no way to beat it. Yeah yes, no met yeah well also like the allocator is just like faster than you want it to be like it would be very cool if like JEMalloc was like bad.

James Munns
Um.

Eliza Weisman
You know because then I could do like all of these very cool hacks to avoid having to Malloc ever. Um, and that would be like great because then all of this stuff would be worth doing ah but it turns out that it's basically not worth doing Anyway. So This is sort of what happened to the Micro Kernel I think that they made the the. Like modern operating systems crash a lot less and they don't have these like a driver bug takes the whole thing down and I think that's largely just because people got better at programming. Ah you know like I think the solution for this was just like stop writing Shitty C code and stop having like one out of bound write that just like Clobber's Kernel memory.

James Munns
M.

Eliza Weisman
Like maybe don't do that anymore. Yes.

James Munns
There's also been a lot of like hardware advancement where like a hardware has certain like protection and stuff like that where you you stop imagining that you're all in a certain linear address space and like you can't just trounce out from driver memory to that and you have.

Eliza Weisman
Yeah, absolutely yeah yeah I think that the thing that maybe stopped us from actually going down this like Gn you heard like.

James Munns
And mmu protection and even like I Ammu for things like Pcie and things like that where.

Eliza Weisman
Beautiful micro kernel future where everything is in user space and you just do all of this Ipc I think the thing that really fixed that is like Rwx I think that just like when the like x Eight six cpus grew like a read write and execute bit. You know like this basically all just went away.

James Munns
Oh got? Yeah yeah, yeah.

Eliza Weisman
Um, and if you do like ah a read on a write-only page or you do like a write on a read-only page you try to execute code from a read and write page that doesn't have to execute bit you try to do that and you get like a cpu exception that you can trap and if you can trap it You can just kill that driver and keep going.

James Munns
Be up.

Eliza Weisman
You know and that this kind of defeated the like beautiful dream of like the the micro kernel where everything is like totally isolated and independent. Ah, which sucks because it's like ideologically pure and it just seems like very nice and cool. So. 1 of the things that I wanted to do is I was like I'm going to write a micro kernel operating system because if I'm going to do this as a hobby project. You know if I'm just going to do this thing for fun I'm going to do it the right way the way that my computer science professor told me was the right way. And not the way that people do it in the real world where they actually have to like make shit that works and like they actually just have one kernel that's been copied around a million times and like x and u is just mock which is like someone's research project from 9095? Um, what if instead of doing that we just did it right? from the ground up. Because it doesn't actually matter if there are like problems with that approach because I'm just doing this for fun because I'm insane. Okay, so that's like thing one. The other thing is you know I had done like a operating system project in college. In my spare time that actually like kind of caused me to flunk out of linear algebra because I don't give a shit about linear algebra. But I love operating systems and so I spent all of my time when I was supposed to be doing linear algebra homework writing my operating system. Um, and I got like really far and I was doing like all of this neat stuff.

James Munns
I.

Eliza Weisman
And I got to the point where it's like okay I want to actually like load and run a user binary and if I want to do that I need to have system calls. Um, and so I kind of am faced with this choice right? which is do I want to just take all of the system calls that are in possex. The portable operating system standard that specifies like um like the unix system calls that all unix operating systems have and then of course there's like extra non-standard ones piled on top of that they're like linux and Mac Os are actually different. They can't just run any unix binary because. Mac os is sort of a Bsd and linux is not sort of a Bsd because it's linux and you like and there's like eppole and like now io ring and like all of these different like cool linux features that are not standardized but there's like this possix thing where hypothetically you can just take like a normal c compiler and tell it hey please. Compile this binary and like only use the possi Sys calls don't use any of the like weird linux ones and you can do that and then you can run this thing on like your troyo operating system in theory. Um, but the downside of that is that you have to use possix. Right? And possi is this thing that was invented in like 1970 like this interface was specified like a billion years ago and I am this like angry hotheaded kid. You know, um I have a problem with authority I still do I think that I've chilled down chilled out a little bit like whatever I'm an anarchist. Um, but like here's me in college I have like an extreme problem with authority and I'm kind of arrogant and I'm like drinking a lot of coffee and I've learned about all of the things that are broken in the world and like in computing that like all of this old stuff from the 70 s like Linux is like. Or like Unix is from the 70 s and linux is just Unix and macos is just unix this unix thing like this is from a totally different time where everyone did everything wrong and they're all stupid and I'm smarter than them and I can do it better and so that's sort of the attitude that I have in college but the sort of downside of that is okay if I don't. Do possi I have to invent my own system call interface and if I invent my own system call interface I have to like make my own libsy if I want to compile programs or if I don't like libsy.

James Munns
And.

Eliza Weisman
And I don't write because I'm this kid who hates like everything from 1970 you know like we can do it right now. Well I don't want to write my own liby. Well if you don't want to write your own Libsy. You basically have to not only do you have to make the whole operating system which is like a pretty big, pretty tall order. Okay, you know like now draw out the rest of the Owl kind of thing. Not only do you have to draw the rest of the Owl but you also have to like make the entire like programming language and Compiler tool chain to run any kind of user space binary or you're going to handwrite in an assembly right? So if you make your own system call layer. Like now you have just like quadrupled the amount of work you have to do and that like appeals to my sense of honor that I would really really like to have this like computer that is like running a program that I wrote on an operating system that I wrote and that program was written in a language that I designed in a compiler that I implemented.

James Munns
Um, yeah.

Eliza Weisman
But it's also sort of like if I work on this operating system every weekend. Um, it's probably I'm going to be like 95 yeah I'm going to be like 95 and it's still like sort of going to work and not really be useful. Um.

James Munns
So will be done by 2070

Eliza Weisman
Even if we set aside the whole you also have to make the programming language in the compiler and the compiler cue chain the system call abstraction. All this other stuff. Ah so that was kind of a bummer for me when I figured this out. Um, but the thing that changed a few years ago is wasm wasm became like this very cool new thing and wasm is like webassembly I think a lot of the podcast listeners are like rust folks who've probably at least heard of this. Um and it's like very cool. And oh it's like something you can compile your programs to instead of Javascript and they can run the browser. That's great. Um, but then it turns out that people want to compile programs and like run them in places other than just the web browser. Um, and so now they need some kind of interface. For like what do I do if I want to open files or talk to the network or all of these things that like web browsers maybe don't let you do or they have their own apis for doing. But if you're just like a normal program you have to do all of this stuff. Um, and so a bunch of people from like the a bunch of wasm people come up with this thing wasy. Which is like the webassembly system interface and it is sort of like a system call interface for webassembly programs that specifies like here are the syscalls that you might do and it's it's a bit nicer than possix at least it's newer.

James Munns
Um.

Eliza Weisman
Um, and it it sort of has this idea of like capability based security. Um, so in Theory it's like maybe more secure and it's sort of like pos. Actually if you look at it like a lot of the names were sort of directly inherited. Um, but you know what? yeah.

James Munns
We come with biases as as people who have learned things over the last years yeah yeah Yeah,

Eliza Weisman
It's also like what else do you call the read syscall. You know you're not going to call it like um I don't know maybe you work for Microsoft and you're working on windows and you're going to call it like read bytes from or like some bullshit like that. But like what are you going to call it. It's read.

James Munns
I Obtain Bytes E x.

Eliza Weisman
You know so in some ways they're kind of similar but at least it's like this newer thing that's like being actively developed and it's not so stable because every computer in the world has it. Um, you know so it's like at least it's a little newer and more exciting. Um, and the other sort of interesting thing. Is that you have this webassembly thing and you have this like binary format that is not machine code right? like no actual computer runs webassembly no hardware does and it's probably. Impossible to make hardware that runs it because some things that webassembly does are like not really, they're easily representable in silicon but it's this like kind of cool format and that's interesting and then the other sort of very cool thing is um, a project that I think that started out at at fastly. A company where you know it just so happens that several of my friends work not like plugging fastly on the podcast but they're working on this kind of cool thing and I'm talking to somebody who's working on it I I believe I'm talking to Adam Fulzer um who is a great guy. You should have him on the show sometime. He's very smart. Um, and I'm talking to Pat Hinkeey who also works at Adam's boss and they work it fastly and this is like before everyone knows about this thing but they start telling me about this thing they're working on which is um, it's an ahead of time compiler for webassembly. Um. And this is now what ends up being called Luci and it's like they use it in. They're like serverless offering and everyone knows about this but this is a couple years ago and it is like I think that it was sort of an open secret. It hasn't been like officially announced yet and they're telling me about this thing and about how cool it is because what it's doing is it's giving you.

James Munns
Okay, ah, okay.

Eliza Weisman
Like native performance essentially for what are the for um, it's it's giving you native performance but it also has the sort of advantage of it has like all of these nice isolation advantages that webassembly gives you. You know like this capability-based system call interface wasi um, and it has like webassembly has this idea of linear memory. Um, and it just like has nice ways for sort of managing the address base of the program. Um, and it also has this sort of feature that. You can take a lot of languages compile them to webassembly and like those different compile tooler chains can all make webassembly and so it it has some of the advantages of the Vm or interpreter that you you know some the different nice things about that. But. You can also just go and make native code and the native code can run with like native code performance. Um, and so they're telling me about this thing and I'm thinking about oh I want to write another operating system and I was sort of thinking that because I I missed working on my operating system. Um.

James Munns
And.

Eliza Weisman
But I didn't want to figure out the syscall problem and so all of these things create sort of a perfect storm in my head where I realize well I don't have to write you know I don't have to specify this whole syscall interface if I use this thing that the was people are working on and I can do this kind of okay. Oh this is where it starts to get interesting. 1 of the problems with with micro kernels one of the reasons that we're not all living in this like Gloria's microernel future micro kernels have a lot of context switch overhead right.

James Munns
You because you're always swapping between the user space. The kernel basically you go from 2 entities you have to jump in between to 3 entities you have to jump in between and.

Eliza Weisman
You're always swapping between the user space and the kernel right? and like all of these drivers are talking to each other by Ipc. It's really really hard to do any kind of Ipc where you don't jump from like process a into the kernel. Into process b back to the kernel back to process a you know like that's a lot of context switches you have to do and like I had just written an operating system I'm smart I know about but like pushing registers on the stack I know about all of these stuff. That's a lot of registers. You have to push on the fucking stack and you're just doing this all the time and there's no way to not do it.

James Munns
It's like when you look at your perf graphs and you're like oh wonder why? everything is Mem copy in my perf graph. Yeah.

Eliza Weisman
you know yeah right and actually around the same time this is when um some of the you know this is like this is a couple years ago I'm like still kind of a young dumb kid. Um I'm unlike like 24 um and some of the smarter people than me at my job like karra Leka Sean Macarthur who are sort of like big names and Russ They are reading about this dpdk thing around the same time and talking about how like cool and exciting. It is to be able to do this kernel bypass networking. Um and then oh it's sad that we can't actually use this because of Kubernetes. Um, but it like just sounded so awesome to me as like this kid who just like loves making things go fast. Um, all of this gives me the like really dumb idea of you know we could actually make a micro kernel. Um, where all of these these drivers are like these totally self-contained demons that just talk to each other over like principled Ipc primitives if we didn't actually make a micro kernel if we actually ran all of this like the the ideas that you have. Like in hardware you have these protection rings you have like internal mode and user mode and switching between them is really expensive and you have these different stacks and you have all of the stuff going on and it's like quite expensive to to switch between these rings. What if we actually like didn't do some of that. What if we took some of these protection these sort of isolation features that the ah the hardware is offering us and we just like did that in in software instead. Um, and so the sort of right and so the idea that I sort of had is you can have like user mode drivers.

James Munns
So more compile time rather than runtime sort of things.

Eliza Weisman
And I did big air quotes for the the people listening from home James saw the air quotes but nobody nobody else saw my air quotes so that's maybe I shouldn't have done that um you can take you can have all of these nice modular restartable hot reloadable user mode drivers.

James Munns
I Like this is an audio podcast. Yeah, ah.

Eliza Weisman
Um, and then you can just sort of bin pack them all into kernel space and put them at like different offsets in kernel space. Um, and you get the isolation benefits by taking the only kind of thing that the system can run. It doesn't run like elf's it runs. Webassembly modules and you submit them to the kernel as webassembly and the kernel compiles the webassembly to real code with something like Luci. Um, and that the reason that that that has to happen in kernel space is because one it. It's a trust boundary right? Like you have to actually trust the compiler to not have taken this like code in the high-level language and compiled something evil right? You have to trust that so it has to be within that trust perimeter of the kernel. Um, also the kernel is the only one that knows its own address space. So like you can you can have your compiler take the webassembly linear memory and then just figure out. Oh I want this at this offset and I'm just going to add that constant or like add these pages to like every. Every time I like when I compile that binary I'm just going to go. Okay I'm like 0 is actually like 7 five f or whatever and I can just pack all of that stuff into one address space I can do ipc ipc my Ipc abstraction. Yeah I did air quotes again.

James Munns
So.

James Munns
First air quotes.

Eliza Weisman
My Ipc abstraction can actually just be shared memory. Um and the kernel can you know and then you can inject these syscalls as like all of these things are doing system calls but the system calls are really just jumping to a different part of the kernel. Um, and.

James Munns
So you so you move the interpreter. Well both a compiler like an ahead of time compiler and the interpreter or the runtime into the kernel so that essentially people presubmit their Kernel Modules The kernel I Guess at that point ah decides whether it likes it or not and either rejects it or accepts it.

Eliza Weisman
Um, yeah, right? yeah.

James Munns
But then once it sort of gets past that layer then it's just an interpreted ah piece of so so earth it.

Eliza Weisman
Yeah, but it's not interpreted. It's running. It's running as as as real code and it kind of has to be because you have these like um like the idea is that this is for drivers but the idea is also what if that was just the whole execution model.

James Munns
Um.

Eliza Weisman
And maybe you have a few different modes depending on like how much you trust that binary. You might want to like everything is being submitted to the kernel that you want to run as a webassembly module. That's just the only way stuff goes in. But. Depending on how you want to spawn that module you might spawn it in like 1 of several ways you might run it in a wasm interpreter right? Like a Vm that's just like executing the webassembly directly. Um, you might run that wasm interpreter inside the kernel in ring 0 you might run it in user space in like in ring three because we don't care about the other 2 rings because nobody uses them because they don't really do anything because they're kind of one of those stupid vestigial things in x Eight six that nobody cares about Um, so you have 2 rings. Ah so you might you might be running them in an interpreter. You might be doing a head of time compilation right? And maybe if you're doing a head of time compilation in the kernel you might have some kind of caching mechanism so you don't do that every time maybe you have like a cryptographic signature or a hash that you use to determine like is this actually the. Thing that I compiled already and I can just reuse that compiled artifact. But that's sort of an engineering problem to figure out later but the like sort of really cool thing that you can do is that you can you have this sort of flexibility in how you're running this stuff if you want maximum performance you put it in kernel space and then it's very fast. Because it never has to do a context switch. Um, obviously like wasm gives you some isolation guarantees doesn't give you the same ones as hardware stuff like specter and meltdown can still happen because these things are running in 1 address space. So you, you.

James Munns
So.

Eliza Weisman
You Maybe don't want to run every binary that way. But the ones that you are giving a higher level of trust to like your device drivers. Yeah, you can just put them all in kernel space make them basically free to jump between um and then maybe if you want to run less trusted Applications. You could run them in a Vm in the kernel. So that they can't really do anything evil but they're still like running in Kernel Space. There's some performance penalty for that or maybe you could run them in user space and maybe in user space What you could do is you can bin pack different binaries together into one process.

James Munns
You You're back to your buddy system.

Eliza Weisman
Because you can do this, You can do this sort of virtual memory magic or linear memory like Wasm linear Memory. You can do this like oh a cool thing about webassembly every wasm Module actually says hey here's how much Ram I'm going to use. Like it says ahead of time when it starts like some of its metadata is I want this much linear memory. Okay, well you can map that to a fixed offset and you can make an address space that bin packs a bunch of different modules together and now Ipc between those programs is also free.

James Munns
Um.

James Munns
Be up.

Eliza Weisman
Right? Because you're jumping from one program into another one. You don't have to go to Kernel space and back you only have to go to kernel space when you want to talk to a driver. Okay, that's kind of cool. This is something interesting and this is sort of the idea of Mycelium and someday it's going to do that stuff. You want to know what it does right now.

James Munns
Yeah, it's a smaller. It's a smaller context jump.

James Munns
What does it do right now. Okay.

Eliza Weisman
Well, it has a webassembly module and that webassembly module prints the string Hello world. Um, and right now the Hello world Webassembly Module is sort of hard codeded into the kernel. Um, and so I have yeah.

James Munns
We're in a remarkably similar state like I don't have an interpreter like mine runs in user space but all it does the only application I have right now is hard loaded into the kernel and it prints loop back from virtual Port zero to virtual port one.

Eliza Weisman
Right? Yep, Yeah yeah, so I actually have a unit test. Um, and my oh I This is a cool thing. This is something I'm kind of very pleased with myself with that I had some help from a friend on. Um.

James Munns
Oh nice.

Eliza Weisman
That we we sort of this was a cool project. Um, but so what I have is I have a unit test and when my unit test runs it runs this hello world binary and the syscall for for like writing to like a file descriptor is sort of hardcoded so that if the file descriptor is standard out.

James Munns
Um, that's like extreme mocking. Okay, okay so I've been sitting here so doing on.

Eliza Weisman
And if it's called with the string Hello world. It makes the unit test pass right? and then and and then and then the program exits and that's what Mycelium does. Yeah.

James Munns
On Well actually I don't know well actually but I'm gonna hit you with a lightning round of note of of statements that I want your gut response to either like no, that's that's wrong or or things like that. Okay.

Eliza Weisman
Yeah.

Eliza Weisman
Oh yeah, well some of these might also be like things that in my head I filed away is I'm gonna solve that problem once I actually get to it. But yeah, just fuck me up. Let's go.

James Munns
Sure. okay okay okay I love that we started the conversation talking about the problems of Java and in my brain wasi and wasm are like next gen java in that you have.

Eliza Weisman
Over.

James Munns
A language that has a portability interface Java calls it bit code Wozi calls it ah that they both have a pre-compiled and ah, an interpreted mode and we started the conversation talking about the unacceptable overhead of Java and we ended the conversation talking about how wasi helps you achieve the future of.

Eliza Weisman
Brighter.

Eliza Weisman
Yeah.

James Munns
Ah, micro kernel operating systems even though they're using the same techniques just but I mean to be fair, there's a lot of learned learned answers in 30 years of engineering you know what? I mean.

Eliza Weisman
Yeah, well yeah, this is a great question. Actually 1 of the big differences between like okay so there's 2 things that I'm going to I'm going to say right now I did say like that the jvm yeah is actually very fast. That it is not. You don't have this like interpreter overhead of like every single instruction is actually executed by a bunch of compiled code that's running in real life because it has like a jet and the jit is very very good actually like the hotspot jit is like 1 of the most. Incredible pieces of engineering that has ever been done by a corporation with more than like 4 employees right? like Oracle? Yeah, yeah, yeah, ah, yeah, jvm um, hotspot is actually often faster than native code. Um, did.

James Munns
It's like v 8 throw enough engineering power at something and you will make despite all odds you will make something that is astounding and.

Eliza Weisman
Because you know it maybe is a smarter because it's doing like jit compilation. It's like profiling things as they run and it might actually be able to compile things better than like Gcc in some cases the problem with the jvm is that it's loading all of this bytecode into memory. Right? Like 1 of its problems is actually its usage of memory. Um, well, it's loading all of this byte code into memory and then as that bytecode executes in an interpreter. It's doing this jit compilation and the way that you do jit compilation is you say hey to the kernel I need like a page that is executable.

James Munns
Is that not the case for webassembly.

Eliza Weisman
Give me an executable page and then you start writing machine code to the executable page and then you start executing that machine code. You know you jump to that address you run that code. Um, and so what this sort of means is that you are doing like you're loading the Java class files which are Java bytecode that you can execute on your Vm. And then as you jet them. You are also allocating more memory and putting machine code in it. That's 1 thing. Another thing is just that having all of this jit machinery like this is also a program. This is also part of the process. And like the actual vm is also in memory. So you're using a bunch of memory for that. You're using a bunch of memory for the classes and then you're using even more memory for like the actual jitted versions of those classes. Um the goal with my it.

James Munns
It but doesn't Java have a pre-compiled version too like it's been a long time since I haven't done Java since like first year of university so like I haven't touched in forever. Okay.

Eliza Weisman
I don't think that it like really does like you you compile things to Java bytecode. Um, actually Scala has a compiler pipeline that gives you that goes straight to native code which I think is kind of cool. It's called Scala -native um

James Munns
Um.

Eliza Weisman
I don't I would not personally use it because rust gives me all of the things that I like about Scala and scala nativeative doesn't give me all of the things I like about rust um like scala native is an unsafe language. It does not have like compile time safety but it also has like.

James Munns
It goes into llvm right? or is it emitting like C code that gets okay.

Eliza Weisman
It It does go to allvm I believe I believe that it goes straight to lvm I don't remember though I haven't looked um and then it also has all of the language features about scallet that I think are bad like implicit conversions I don't think that one's bad that one's fine.

James Munns
He like every ah everyone divining their own operators for everything. Okay.

Eliza Weisman
It's the implicit conversions that are evil the way that they work is evil and they're actually more principled than any other language with implicit conversions. But they're still kind of fucked up. It doesn't matter. Um, yeah so Scala Native is very very interesting. It also sort of seems like a version of rust that's kind of worse.

James Munns
3

Eliza Weisman
Ah, like it. It gives me some of the same things but it also gives me like less of them. But anyway that doesn't matter I don't know how we got on the subject of S Scala native I that's my fault. Um, yeah.

James Munns
Well I've got I've got the next thing that you you said I don't think webassembly will ever run on hardware. Are you familiar with what gisel is yeah I was going to say so ah Java yeah, well now they have both.

Eliza Weisman
Gisel is the the arm Java instructions or javascript instructions right? okay.

James Munns
Now they have gisel was that so like back in the day of r and v 5 um, which I've worked on surprisingly recently because embedded systems never die. Um yeah I mean it has something like hardware acceleration for like 150 of the 200 bit code operations that you can do.

Eliza Weisman
If if. Yeah, yeah.

James Munns
And it for exactly that reason is for tiny little devices where you want to run your your Java application. You want it to run reasonably fast so they just have a hardware acceleration. So I mean it's funny because you mentioned oh it'll never happen for webassembly. But if it gets big enough just like Javascript has these same like.

Eliza Weisman
Ah.

Eliza Weisman
I mean I guess.

James Munns
All right? Well turns out we spend all of our cpu doing this one macro op in Javascript might as well add 2 more instructions for it.

Eliza Weisman
Right? Yeah, and so you now have like floating point multiply or it's like fused multiplying ad javascript version which is just like a special instruction that has like whatever the Javascript semantics are instead of whatever the hardware semantics are.

James Munns
Um, yeah, and it's like I trippoli. Yeah, it's like so yeah, exactly.

Eliza Weisman
Yeah, okay so the Jiiselle thing actually and speaking of Gille the other thing I think about a lot is Java card. Um, and I think about it for 2 reasons and 1 of them is that people who live in the bay area like me who ride public transit use Java card. Yes.

James Munns
Mm.

James Munns
Um, does the bart card use Java Cards what okay

Eliza Weisman
The clipper card is a job the clipper. This is actually fascinating the person to talk to about this is not me but maneeche. Um, because all of the cool bark facts that I know I learned from Maneeche who is like the like ultimate transit geek. Um, however I can tell you a very cool story about how clipper card works. Um. Which is that clipper card is kind of unique among most of the transit cards in the United States at least because unlike most of them the clipper card is an actual store of value. So.

James Munns
Yeah, because most so for for other folks most cards just end up being a an id like sometimes there's some cryptographic proof for on there to like to make sure that you are the 1 true one but most of them are just like okay beyond all the layers you are proven to be this.

Eliza Weisman
Right? Yeah, yeah, yeah, yeah, it's a proof of your bank account or a proof of an account with the system that lives in the internet.

James Munns
Person. Yeah.

Eliza Weisman
Have you? you've been to the Bay area I Imagine you've probably used a clipper card. Okay, okay, so one so the thing about the clipper card is that the clipre card was introduced relatively early in the like history of transit smart cards and one of the things.

James Munns
Yeah, no.

James Munns
Um.

Eliza Weisman
They wanted to do with the clipper card is they wanted to make it. They wanted to make it so that you could use it for Bart obviously but also for San Francisco muni which is like San Francisco light rail um and bus system and also for Ac transit which is the Alameda County bus system

James Munns
M.

Eliza Weisman
Um, and also for Caltrain which is like heavy commuter row. Um, and some of those systems like okay so like the Ac transit buses don't have any kind of internet connection and this is like the 90 s and it might actually be hard to give them an internet connection now they kind of.

James Munns
Um.

James Munns
Um, and this is way before like tap to pay or like the oyster card or like any of this was a thing.

Eliza Weisman
Yeah, yeah, yeah, nowadays they do have an internet connection that you can use for tracking the bus but it like mostly doesn't work. Um, so like Bart like Bart Stations are huge. It's a subway system. The infrastructure is like there aren't that many stations they're giant. You could definitely run like fiber into all of those stations so you could make the bart machines when you like scan to go through the turnstyle that could just use a system like the 1 you described where the car just has an id the buses especially the Ac transit buses cannot do this. At the time that clipper card is being invented. Ah there is like and and when you get on a bus you scan on the machine on the bus. You know they're not like they they don't want to put every bus stop some internet connected device. So at the time they cannot really connect those buses to the internet. So what they have to do is they come up with a system where. When you're at a bart station. They have machines that you can use to like those are internet connected. You put your credit card in or you put your your bank account in and they put money on the clipper card and then the clipper card has like dollars stored in it that when you swipe the clipper card at like ah an. A reader it subtracts some of that and then stores the money in the bus and this is the best part. The best part is that at the end of yes, yeah, James's eyes just like bugged out. It was amazing. Um, so this is the best part.

James Munns
I Okay, also for audio is my eyes are huge right now.

Eliza Weisman
Every night at the end of bus service when all the buses go back to the Bus Depot They have an ethernet guy you know like okay like people go on the bus they start cleaning it doing maintenance stuff. Whatever one of the people is the ethernet guy just walks around with an ethernet cable.

James Munns
But Nope yeah.

Eliza Weisman
Plugs the ethernet cable into each bus all of the money that that bus has accumulated over its day of service is like downloaded and then goes into like AcTransit's bank account. Um.

James Munns
It downloads money.

James Munns
How did how did we end up in the future where we have bitcoin and not like clipper as the like number one store value I want ethernet.

Eliza Weisman
Right? clipper it. Yeah, unlike some cryptocurrencies the clipper card really is a durable store of values and I think about this a lot. Um because I just think it's hilarious.

James Munns
Ah.

Eliza Weisman
It also has caused me like practical problems in my life which is that you they have a thing now where you can like hook the clipper card up to your bank account. Um, so that like when your clipper card runs dry it just like automatically takes twenty bucks out of your bank account and puts it on clipper card.

James Munns
Um.

Eliza Weisman
And this is very nice, especially when you're a person like me who just like forgets to use the machine at the bart station to put money on my clip card. Um, the problem is that this doesn't work if you're getting on the bus because the bus has no way to talk to your bank account. So if you're so if you.

James Munns
Yeah.

James Munns
Mm.

Eliza Weisman
Like I used to live in Oakland and the place I used to live I would take the bus to the bart station. Um, and then I would get on the bart and I would go to my office. Um and the problem is that if I got on the bus I needed to know that my clipper card had like at least $2 for bus fare on it because it could not.

James Munns
Mm.

James Munns
Um.

Eliza Weisman
Like if you get on the bus and or if if you're you're you know, scanning to get on Bart like a big subway station turnsile your clipper card has zero dollars on it. It just downloads some money onto it. But if you get on the bus they say oh your clipper card has no money on it. You can't get on the bus unless you have like a couple bucks in your pocket or whatever and then the bus driver lets you on. You know? Um, so that actually has caused like real problems for me in my life nowadays the Bart like this actually happened like last year um it now also works with Apple pay and so if you have the like clipre card Apple Apple wallet thing. Um.

James Munns
Ah.

Eliza Weisman
That will just take money out of your bank account right? because your phone is connected to the internet because you have cell service but they never they never wired it up so that the buses could do like a direct deposit even though the buses are now internet connected and so. Like the Apple pay thing just sort of didn't end run around this but that happened like last year so the first couple years that I lived in the bay area I like the thing of like automatically putting money on the clip card like kind of useless for me because I had to get on the bus to get to the bart station where I could put money on the clipper card. Anyway, I just.

James Munns
He.

James Munns
I I love these like massively I'd say overengineered they feel overengineered now but like they were the only option at that point and I'm sure it was it was groundbreaking like the only thing that it can make me think of is like 90 sitcoms like the plot points of every 90 sitcom. All of them could be defeated if you could text.

Eliza Weisman
Um, yeah, yeah, um. Right? If if you have a cell phone. Yeah, yeah, yeah, right.

James Munns
Someone? Yeah yeah, like if you call someone and be like what this person has gone missing or oh no, they forgot this or oh no, they did this and in like hundred percent of like Seinfeld episodes could have been solved in 30 seconds with a text message and like the exact same thing of like oops.

Eliza Weisman
Yeah, yeah, the entire like overengineered Bart Java financial system could just like this is just like okay you put like a ah gsm modem in the bus. Yeah.

James Munns
Um. Yeah, oh we we put two G in ah in the bus. Oh. It's It's fine now like.

Eliza Weisman
Yeah, actually that's the other thing is that um bay area still has two g service specifically because of Ac transit buses. Um, they have like paid the service providers to keep running two g service yeah because they don't want to replace the two g modems that are used for the like.

James Munns
Oh yeah, that'll do it but like releasing the the spectrum and stuff.

Eliza Weisman
Crappy bus tracking system that doesn't really work that's supposed to tell you if the bus is on time. They don't want to upgrade that to three g ah so they just like keep paying whatever like telecom provider is like responsible if they just keep shelling out like more and more money to be like the only two g customer anyway, that's a cool Bart story.

James Munns
M.

James Munns
Yeah.

Eliza Weisman
Um, we got here because we were talking about Gille and then I like derailed us into Java card which I just think is like hilarious, um, the other thing I like about Java Card is that yeah do you know? but the Java card ring. Yes.

James Munns
Yes.

James Munns
Um.

James Munns
Yes, like the 1 wire ring like yeah.

Eliza Weisman
I think about that constantly I wish I had one of those I want to see if I can find 1 on like ebay or something because I just like really want the Java ring. Um I feel like that would be a very good like if you are getting married to someone who is like an even bigger nerd than you. You should like propose with like a Java ring.

James Munns
Ah, nice and like the final thing that I wanted to to point out on the the coming full way around I think I had something else but I'll wrap up with this one instead because my brain's totally off the rails too. But I love that you come. You came to your operating system.

Eliza Weisman
Anyway, yeah I'm I'm sorry we.

James Munns
From a perspective of like there is idle. Someone is wrong on the internet and I have to make it right? like the like the ideological I thought you werere gonna say like Ken Thompson but like.

Eliza Weisman
Will the person who's wrong on the internet is Linus Torvalds and well Kent Thompson before him Kent Thompson is fucking wrong actually I think Kent Thompson made a lot of like reasonable decisions like this is the thing I will actually defend Ken. Yes.

James Munns
Yeah, you and I talked about this at some point whereas like there was a Twitter thread that was like we were talking about something and you're like do you think Ken talk like if we could go back in time we were talking we were talking about something. It was like if you could go back in time. What do you think would blow his mind or would he even want this.

Eliza Weisman
Yes.

Eliza Weisman
Um, yeah.

Eliza Weisman
Right? That was actually that was an argument I had with um, a friend of the show Michael Gatasi um like couple years ago that I had brought back up when we were talking about this? yeah and it was like right.

James Munns
I Think we were talking about like would he want rust and I think. Okay, yeah. Yeah, my point was like as an engineer he probably would have been like that's great I Can't do it Now. So sounds great but you know you have fun with that like.

Eliza Weisman
Yeah, yeah, Michael was like oh the c programming language has caused so much problems and like if somebody had just told Canne about the borrow checker. It would have all been fixed and I was like I think that your thesis that the c programming language has caused so many problems is true. But I think that like. It probably wouldn't make sense for Ken to use the borrow checker because the reason that the c compiler like all of the function prototypes have to be declared before they're used is because the c compiler is a single pass compiler.

James Munns
Um, was already a problem like yeah.

Eliza Weisman
You know and it's a single pass compiler because you don't want it to take any longer to compile your C program on a pdp eleven than it already takes which is way too long and like the the Pdp Eleven probably doesn't have enough memory to run the kind of analysis that rust runs you know and so I'm like right.

James Munns
Yeah.

James Munns
Um, my computer often doesn't have the kind of memory necessary to run the analysis that rust runs.

Eliza Weisman
But yeah, right and the other thing is that no one's pdp eleven was connected to the internet unless they worked at Darpa there were like four pdp eleven s on the internet at the time. Yeah, and and all of those people work for the department of defense. So it's not like the internet is filled with people.

James Munns
Yeah, and they got to talk to each other and that was great. So.

Eliza Weisman
With like other pdp elevens that want to murder your Pdp eleven. That's the world we live in now. But that's not the world Ken lived in and I don't think that choice would have made sense for him. The person that fucked up is not Ken. The person or the people that fucked up to me in my like view of history is the people who kept using Ken's stuff instead of making new stuff for like all of the 90 s and like all of the the odds and like most of the 2010 s those people were making the mistake.

James Munns
But that's but that's exactly the point that I was getting at is that there has been I think the thing that has been holding so many people as people as like human the humans that do the engineering There is only so much.

Eliza Weisman
Of like.

James Munns
Context and complexity. 1 person can keep in their mind and there's maybe even an order of magnitude variance from person to person depending on the topic depending on the time of their life depending on whatever or the people that surround them and motivate them and stuff like that but like not a lot more than an order of magnitude I would say um.

Eliza Weisman
Yes.

Eliza Weisman
Yeah, this is like I don't know how to do anything useful on the computer like you know there's yeah.

James Munns
Well um, but you do but like everyone has a band of stuff or or ah, you know, even ah, a stripe of things that they can do and that's one of those like interesting things about Rust is sometimes it takes away some of that.

Eliza Weisman
Um, right? Yeah yeah.

James Munns
Complexity because one you can offload a lot of it to the compiler to be like well I wrote a library that was safe a month ago thanks computer me you you can keep checking that and I won't have to remember that or like I don't need to context switch whether I'm writing an application or a network stack or an operating system. Whatever like it's still or us like I'm using different.

Eliza Weisman
Right? It's all the same. Its all the same language right? and you even use the same crates. You can even sort of use Tokio and or or you can't use Tokio you can even sort of use tracing and embedded in someday someday someday. It's going to be better.

James Munns
It's a rust but like it's it's still rust and.

James Munns
Um, I know people who are trying to get Tokio working on.

Eliza Weisman
Um I just I can't fix some of it in V one but in V Two I'm going to fix a bunch of the stuff that makes it like not great for like embedded folks. Um I can't make it as fast as D format because it's like impossible to do that without doing the exactly.

James Munns
Yes.

James Munns
I'm just doing different stuff. Yeah, the only way the only way to go faster is to do less and like that's the difference is tracing is doing like deform doesn't do filtering. It's not doing aggregation or anything like that. Yeah.

Eliza Weisman
Without doing exactly the thing that you did It's impossible to make it that good. But I yeah more stuff that you can't not do yeah I did get rid of the one mandatory allocation.

James Munns
Nice, yeah.

Eliza Weisman
In v two so you can now use it without alloc at all. Um, and you can get rid of like mycelium used to have like a bump allocator that was used to allocate like 1 box for tracing before using the like real allocator. Um, and that it just like instantly leaked. Um, but eat.

James Munns
Button.

Eliza Weisman
Gap Part I got rid of so you can now compile it without linking live alllog. It's like it's going to be about as good as it can be for embedded people when I finish O two. Well yeah I actually think the D Format is like extremely good for my primary use case too in the like.

James Munns
Without compromising like your primary use case. You know what I mean.

James Munns
Um.

Eliza Weisman
A lot of the stuff that you're doing is very cool. It introduces like one hurdle which is that? Yeah okay, oh okay I sort of thought that was your thing. Oh it was. Jorge's thing got it

James Munns
I mean I I've never generally been involved with dformat other than hyping it. Ah so like I worked at Ferris for a number of years but like deform came out of Jorge's brain and then a lot of like um, there's a lot of people at Ferris who worked at it like but I think it was primarily jonis and Jorge.

Eliza Weisman
Okay.

James Munns
And tanks and lata I think who did most of the work I've just been the hype man for like a lot of stuff people associate with me because the 1 thing that I do is I'm a loud mouth better than a lot of other people are allowed mouth so like and.

Eliza Weisman
Um, yeah, that's fair. Yeah I'm going to be honest and like sorry to Jorge because I had always assumed that de format was like James's project because James is the only person who's ever talked to me about it me.

James Munns
oh no oh no no I'm just hype man like and almost all the stuff that you like or a lot of times at at Ferris likes people have been mentioning things and I'll go you spend that time on this and glue it together with this and like I can't take.

Eliza Weisman
Okay.

Eliza Weisman
I have.

James Munns
Any of the engineering credit but like the like go for it make time and then I just like shit post on Twitter for months and months and months until it rings around in people's head and they don't forget about it like that's absolutely my job whereas like the operating system stuff that I'm working on now is.

Eliza Weisman
Yeah, well same? Yeah yeah.

James Munns
I've come at it from a very different perspective because my approach has been how terrible can I make this and get away with it because I have such trouble keeping context and things like that like I remember weird details but like keeping motivation and things like that going where like my syscall interface is like.

Eliza Weisman
You certainly have. Yeah.

James Munns
Like you said reusing crates from other parts I literally use serde for my syscall interface because because I'm like yeah I'm like I'm not going to be able to keep together a binary format So serde cool like and like that's one of those like I'm going to push This is my like much more I.

Eliza Weisman
That's actually awesome to me that the fact that you can even do that right.

James Munns
I was a computer engineer when I went to school so like I didn't take the compiler classes or things like that I took a lot more embedded classes and things like that. But my approach has always been much more like all right? How bad can it get and we still get away with it and like but still deliver What I'm trying to do and like my goals are very low for my operating system and I know you feel this but like.

Eliza Weisman
Ah.

Eliza Weisman
Mother.

Eliza Weisman
Well same.

James Munns
My goal is like what can I put together that doesn't fall apart and maybe I can have a text editor or maybe make some like audio synthesizer music type stuff with it. But like my my goals are very low but like it's surprising how much you can get away with like it's It's the.

Eliza Weisman
Yeah.

James Munns
Does it bad solutions live forever or whatever it is like the good code. However, I mean there's there's something like good code something something bad code never dies like I think that's exactly the like the unix stuff is is like when you're putting this power into more people's hands.

Eliza Weisman
Never and then. Yeah, yeah.

James Munns
It it opens the door from more things because historically if you had to keep the context of how all this stuff like the Cys calls and the things like that like you'd get 1 person out of 100 that that either was able or willing to like sync that much time. Otherwise you just build on someone else's stuff because you go look I can't like Cys calls not a thing or database is not a thing or like.

Eliza Weisman
Of that enough.

James Munns
Network stacks not my thing and so you just go. That's a box and it's lovely and I can use it but I'm not going to touch it. Yeah yeah, you you build on top of it because that's all your brain has cycles for but like the more you can make that accessible to other folks is interesting because I think you can like get away with a lot of crimes.

Eliza Weisman
Um, writing it works I Guess yeah for sure. Nothing.

James Munns
And end up making some like really particularly interesting stuff. So.

Eliza Weisman
Well ironically the place that I really copped out is the place where it seems like you have been doing a bunch of like fun stuff for your your os and computer project is that you're making a computer right? like you are doing like.

James Munns
M.

Eliza Weisman
A bunch of really neat like firmware stuff and like hardware stuff that I totally copped out on I'm like my system is going to run on an x Eight six pc I'm not going to write a bios I'm not going to write a boot loader I'll go back and write the boot loader when the kernel's done.

James Munns
Yeah.

Eliza Weisman
You know, like that stuff I would like to learn I would like to do that I would like to write firmware I would like to write a Bmc I want to make a Bmc for my desktop just because I think it would be extremely funny I want to make like a Pci card that does like Bmc shit. Um, but I'm probably never going to do it because I have like this other project.

James Munns
He. Nice.

Eliza Weisman
So I copped out on going like I don't know I'm going to assume like I have a lot of problems with the way that like the hardware that we all have in our homes works like I think that X Eight six is kind of trash but like I'm just going to I'm not going to solve that problem I'm going to I'm going to accept.

James Munns
Um.

Eliza Weisman
Okay I have I think pad it has an x eight six cpu and it I'm probably always going to have an x eight six cpu in my house all'll write the operating system make sure it runs on that someday I'll make it run on risk five maybe that would be cool someday I'll write a boot loader someday I'll write my own firmware.

James Munns
You start from you start from like is is like 1 of those main things of teaching and learning and stuff like that like you to go anywhere. You have to have one solid foot and for me like I've been writing bare metal code for these microcontrollers and stuff like that and boot loaders and stuff so like that was my stable foot and I have.

Eliza Weisman
But for now I'm just going to make.

Eliza Weisman
Um, yeah.

James Munns
No operating system experience other than like you know I vaguely know how it's supposed to work because you write bare metal stuff that pretends to do that kind of stuff sometimes but like you've been coming at. It's been interesting to see you come from like the totally different direction. But I love that the 2 the place that we like intersect is like.

Eliza Weisman
And break.

James Munns
Data structures and concurrency are like you and I will send stuff to each other on Twitter where you're just like check this out or I'll be like I wrote this terrible allocator and you'll be like not check this out like that's been super fun. Yeah.

Eliza Weisman
Simply.

Eliza Weisman
Yeah, look at the dumb thing I did we could spend and we could fill another 2 hour podcast episode talking about lock free algorithms I think but we're not going to touch it today. We can't that's my other other love.

James Munns
Oh no, yeah, we can't ah.

Eliza Weisman
Sort of like elaborate ballet dance that you do on on thin ice while everyone's holding knives and you spin it. You speed it up to like 200% and then like try not to get murdered is my other fundamental like deep. Love.

James Munns
I Have a I have a guilty admission about lock Free algorithms is that I ah don't actually care about performance I Just really like putting data structures in static memory so that I can just use them everywhere and to do that you like.

Eliza Weisman
Um, right? But the other nice thing is yeah well, the other thing is that like in Mycelium we've had like a million problems where like the the.

James Munns
It's just easiest if you use lock freee algorithms because you use it Lumix for everything.

James Munns
Um.

Eliza Weisman
Like panic or cpu fault handler deadlocks because it touches something that has a lock in it because I wanted to dump its state. You know so it actually matters a lot in your like so totally single-threaded single core environments if you can like if like you can always write like oh force unlock all of the mutex because I'm in like an Isr but like it's.

James Munns
Oops yeah.

Eliza Weisman
Nicer to not have to write that you know because that always feels very dirty. Um, and yeah.

James Munns
And that's the thing that I'm avoiding right now is like okay I can load a program but ah 1 it has user space isolation which is great if you touch anything you'll get a hard fault but I haven't written a hard fault handler. So if you do something you're not supposed to it's still crashing the cpu crashes safely.

Eliza Weisman
Right? who.

James Munns
But it's still crashing the cpu and I have no idea how I'm going to exit program exiting a program is much scarier than entering a program. So.

Eliza Weisman
I spent like a ton of time on like the the fault and interrupt and panic handlers because I thought that like the first most important feature for the operating system to have. Is when it crashes it needs to make like a beautiful crash screen that gives you all of the information about what went wrong because you know you have to sort of. Are you familiar with um the writing of James Mickens oh you should look him up. He's hilarious. Um, he's.

James Munns
I I don't think so what would I know from him.

Eliza Weisman
A professor he works at Microsoft Research um but none of that's what's important about him because the important thing about him is that he has written these like usenix columns that are just like hilariously funny. Um, he's like 1 of the funniest writers in software.

James Munns
And.

Eliza Weisman
Um, he's written one about like systems programmers and like it's like why systems programmers are the people that I want to have like on my apocalypse team. Um, which is the one that I'm thinking of because there's a. Bit in it where he's sort of like I'm trying to like debug my like network file system and I like walk over into the other room where there's like someone from the like Hci research group at Msr and that person's like oh you know how? how's your like project going I'm like oh it's terrible I have like this like. Pointer. That's like missile it's like aligned on like ah a 7 byte alignment and like why would you ever have that because only like an evil pointer would be aligned on 7 and like what's happening and like this is just all insane and everything is broken. And the colleague is like oh have you tried like printing some like debug logs to the console and James Mickens is like well I can't do that because literally everything that I need to do in order to print some debug logs to the console is broken because I've broken all of my tools with my tools.

James Munns
Is this? Yeah yeah, that's exactly who I thought you were talking about I was like is this the guy who is like ah the tool like yeah I've broken all of my I've used my tools to break all of my tools.

Eliza Weisman
And yes, that's that's where we go yes. Right? That's why Mycelium's crash screen is like really good and I've put a lot of love into it because like sometimes it's the only way to get any information Out. Um.

James Munns
I.

Eliza Weisman
Because I have not written a file system or anything yet. So I can't like make crash dumps and save them on the file system which would be like very nice. So instead I just like draw a big red screen I'm like well something bad happened here's like all of the registers I can think of um.

James Munns
I I'm still cheating and so like my the actual kernel of my os is using Arc Tech which is like ah an embedded systems Framework in Rust but you can kind of it's structured into like you got some interrupts which are all of your Event-d driven tasks and you've got idle which is just your like user mode. But I.

Eliza Weisman
Okay.

Eliza Weisman
Right.

James Munns
Then as soon as you enter idle mode I jump to protected mode and launch apps from there. But every time you and there's actually 2 different stacks on cortex m there's the user so or the process stack and the main stack and there's a neat hardware feature that every time you jump into an interrupt it auto switches to a different stack for you.

Eliza Weisman
Hello.

Eliza Weisman
Another.

James Munns
Switches to the main stack rather than the process stack which means my user space application has its own stack and then every time I service and interrupt I go back to the main one and Arctic has no concept of ah of process stack like it assumes that you're running in privileged mode and and everything like that. So I get all of the like.

Eliza Weisman
Arab.

Eliza Weisman
Bright.

James Munns
Context switching for free because the hardware happens to do that and instead of having kernel logging I have deformat so I literally have my debugger attached and anytime I actually want to debug my kernel I use like bare metal embedded systems tools for that and then I use the console when I'm trying to debug that but eventually like you said I'm going to have to like.

Eliza Weisman
Right? right.

Eliza Weisman
Yeah.

James Munns
User space app it should at least have some in-band way where I don't need to have a physical debugger attached to figure out what was going wrong with my hardware.

Eliza Weisman
Right? Yeah, that's the cool thing about x Eight six is that you don't have any kind of debugging tooling right? There is no like JtagPort I mean there might be unlike some motherboards but all it lets you do is like debug the motherboard firmware.

James Munns
Um, well, there's like Apple ones where like over a usbc, there's like a special cable. You can make that basically ends up being like an in-circuit debugger for the kernel I think.

Eliza Weisman
There is not yeah.

Eliza Weisman
On on some future episode of the podcast. Please remember to ask me about the Apple Hdmi to usbc dongle unless you already know about this story. Yes, it is that one I think about that a lot I I love and hate that thing the 1

James Munns
Is that the one that's it's a computer inside of an adapter. Yeah well yeah I that's.

Eliza Weisman
The one that only works on Macs because only the Mac driver knows how to like download the like fucked up minux kernel onto it. Yeah.

James Munns
Yeah, yeah, that's the thing is every computer and this is like that was the the banner of an acro was your computer is a distributed system stop hiding from it like because that's how like we have these systems of systems.

Eliza Weisman
Moving right.

James Munns
And just every problem is a distributed systems problem which like I went to build the first. This is my second attempt at building a personal computer. The first attempt I fell down the rat hole of building a network stack because I realized to get my computers to talk to other computers I had to have a network stack and that's where like.

Eliza Weisman
Um, yeah.

James Munns
Things got bad and cursed for a while.

Eliza Weisman
Yeah, well this is kind of this is kind of like you're like a hardware guy looking up in a lot of ways and I'm kind of like a software girl like looking down and I also learned all of this stuff from trying to program x Eight six and you're like reading the manual and it's like oh there's the like.

James Munns
Um.

James Munns
So.

Eliza Weisman
The I don't remember the model number. There's this thing called a pick which is like a tiny chip with like 8 like 8 leads coming out of it. That's an interrupt controller and oh there's 2 of them and the second one is mapped to the first one and for some reason Intel made all of the interrupt factors that it likes it.

James Munns
That.

Eliza Weisman
When it boots. It's mapped to like these interrupt vectors and those are like those conflict with the ones of like some of the cpu exceptions. And yeah, it's programmable interrupt controller.

James Munns
Um, and for the embedded folks out there. That's not pick Microcontroller That's the programmable interrupt Controller which is basically a little computer that is your interrupt. It's like the Envic on Cortex M Yeah yeah.

Eliza Weisman
Yeah, a very little controller. It's barely a computer. It's just sort of a mux you know it like barely it. It is not like a microcontroller. It's just like a mux. Yeah, and now they actually have that you like also like this is the other things that this thing is obsolete and you're not supposed to use it? Um, but it's there and it works.

James Munns
It's digital logic. Yeah.

James Munns
Um, and it has to um.

Eliza Weisman
Ah, now. They also have a thing called Apic which is the advanced programmable interrupt controller and this actually is a bit closer to a microcontroller. It's a little bit smarter and it can do like stuff and you can like program it from like your code and it's like very smart. Um, but the problem is that if you want to talk to it. You have to like parse the hci tables and like that sucks and so I haven't done that yet. Um, but that's sort of 1 of my next big projects anyway. So for me like I'm a software person and I'm like looking at.

James Munns
Um.

Eliza Weisman
Like Intel manual in college and that was sort of when I learned like oh my computer is just like a bunch of computers that are all talking to each other and like the cpu is the one that like we all actually know how to program but it also is in many ways.

James Munns
So.

James Munns
And the cpu is secretly multiple computers.

Eliza Weisman
Oh yeah, I mean these days. It's super is but like in the Intel the Intel book is like written as though it isn't you know it's sort of like written as though it's like the 80 s and it's a 89 which like maybe actually is a single piece of computer on that die and then there's just like a bunch of like.

James Munns
Mm.

Eliza Weisman
Buy us chips and shit on the motherboard that it talks to um, but and the Intel book is sort of written as though this is still true. Even though it's like definitely not. But you're like oh like what this shit is like ah an io pick. Oh that's a computer and I have to program it and the way I program it is by like.

James Munns
And.

Eliza Weisman
Shooting a bunch of bites into it that all tell it like you have to be in this mode and for some reason why do it? Why did the interrupt vectors on the on the pick like why are they the same as the interrupts that the cpu fires. And the first the very first thing you do before you can handle any interrupts on x Eight six is you have to like put the pick into like programming mode and send it a bunch of commands that reprogram it to put all of its interrupt vectors in a place that don't like fuck it up.

James Munns
M.

Eliza Weisman
And it's kind of like why didn't they just do that. Well the reason they didn't do that is because like the very first like through like ah like 87 like yeah well but the reason they did it is because the very first like Intel Pc bios

James Munns
Um, non-volatile Ram was too expensive.

Eliza Weisman
Right? The like from Ibm the bios chip the one that like everyone then knocked off and opened up the like world of pc loans the Ibm Bios remapped the pick interrupts to put like I guess Intel didn't think of it. The. Ibm Bios remapped the pick interrupt so that they're like not in a fucked up place and then everyone cloned that bias because they figured out that they could reverse engineer it without like infringing Ibm's copyright and everyone made pc clones. Someone decided oh we want to put like a 89 in a pc clone so the 89 also has to start out this way because otherwise they'll get fucked up and like now like every x eight six device that you might ever buy is just like like this because somebody in the 80 s like. Thought that it would be cool to reverse Engineer Ibm's bios. We. we need to stop. yeah we need to stop

James Munns
okay okay I am calling it here. Yeah, we need to stop because I can talk to another talk to you for another 2 hours but it's getting about midnight here in Berlin so is oh no, it's no worries. So.

Eliza Weisman
Oh shit sorry hands.

James Munns
Before we wrap up is there anything you want to plug anything that you're super excited about that. You want people to see follow you on Twitter Twitter handle that you want people to go look at.

Eliza Weisman
Um, yeah, my my Twitter handle is myco liza m y c o l I z um, don't look at mycelium because it sucks and it only does 1 thing. Um, you should. Actually the thing that I would really like to get people involved with are Tokio console and tracing. Um, which I actually do for my day job and I would love like contributors with that said, if you are the kind of person who actually like knows about operating systems and stuff and you want to hack on mine I would love that because that would probably make me work on it more.

James Munns
That's my secret thing is I'm going to send you some hardware for my operating system and hope that we can just like smush the 2 of them together.

Eliza Weisman
So I'm very excited about that I'm I'm there I would love to see if I can pour some of the code that I've written to run on James's computer because I think. I think it's going to be very cool when you make your computer and I make my operating system and I can make my operating system run on your computer I think that's going to kick ass. That's the that that will make me that will appeal to all of my like desire to write everything by hand on my own.

James Munns
That would be doubt. Yeah.

Eliza Weisman
Um, which you no one can do because we're people and we exist in community and we rely on others and no one can specialize in everything So it's cool that there's like also someone who wants to like reinvent their world and because then maybe we can team up.

James Munns
And bridge the gap you know Definitely I Still need a better name for it. But yeah, okay, well it is excellent talking to you? Thank you so much for your time I am super pumped to talk again.

Eliza Weisman
So I'm very very excited to receive my James Pc in the mail and solder it together.

Eliza Weisman
Yeah, let's do another one. Maybe after I get my hardware from you.

James Munns
Yeah, yes, that would be an excellent follow up of like look we were both wrong about operating systems whenever we posted that I think this might end up having to be 2 episodes anyway. So.

Eliza Weisman
Right? Oh I am quite sure that I half the things I said are definitely wrong. Um, that's true. That's right. Okay, you get some sleep I'm going to turn my air conditioning back on.

James Munns
That's good it. It's more interaction. Okay awesome I will talk. Oh yeah, it's probably getting hot. Okay, talk to you later bye.

Eliza Weisman
This was a lot of fun peace.
</details>

## Credits

Thanks to [Louie Zong](https://louiezong.bandcamp.com/) for the music.
