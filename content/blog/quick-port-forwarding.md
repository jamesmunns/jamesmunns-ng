+++
title = "Transparent Port Forwarding"
date = 2016-09-05
draft = false
# tags = ["tag1", "tag2"]
# category = "rust"
aliases = ["update/2016/09/05/quick-port-forwarding.html"]
in_search_index = true
template = "blog_post.html"
+++
I just wanted to share how I solved a little problem:

I have one device that is connected to two networks: A and B. The A network is semi-public, and network B is completely private. I would like to connect from a device on network A, to a specific socket on a device on Network B.

To do this, I need to forward a public port from Network A on my middle device, to a private port and IP on Network B. Heres what I did:

<!-- more -->

```bash
socat TCP-LISTEN:4567, fork TCP:192.168.10.20:1234
```

## Ugly diagram:

```
|        Network A         |         Nework B          |
<public device> --- <bridge device> --- <private device>

connect port 4567 --------->
                           forward port 1234 ---------->
                           <-------------------- respond
<--------------------respond
```