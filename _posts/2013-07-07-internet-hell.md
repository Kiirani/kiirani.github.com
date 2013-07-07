---
title: I am in internet hell
layout: post
---

I'm moving in a month. Before they move my worldly goods, the relocation company has to assess the location where they'll be picking my stuff up from, and the volume of stuff they'll be picking up.  My tiny apartment is not going to be an appropriate place from which to relocate internationally, so I've moved everything to my parents' place. Including myself.

I got here yesterday afternoon, with my things and my computer. Setting that up is doublepluspriority, because I need to use it to work on Monday.

### Internet Hell: Problem 1 ###

Enter Internet Satan, stage left.

First up, the router is at the other end of the house. This shouldn't be an issue, because I've had wifi signals cross this house before, no problem. But the router is at the **low** end of the house this time, and I'm setting up at the **high** end.  I set up the desktop, playstation, and my android phone next to each other, and none of them could get a consistent enough signal to actually connect.

Did a bit of hunting around my things, pulled out the best router I own (my little netgear dgn2000) to try and use it as a relay in my bedroom, halfway between the two machines, to boost the signal strength. 

Delete two hours of my life trying to get the netgear to play nicely with the rest of the kit; I realised there's a phone line right where I needed the relay, and all of the computers in question have wifi cards.

Installed the netgear as the primary router & wireless AP for the house.  PS3 and android phone connecting successfully; desktop? Not so much.


### Internet Hell: Problem 2 ###

So I've got a decent enough wireless signal now and I go to connect with the desktop machine. 

I get into negotiations with the router and wicd freezes up and hangs, because it's trying to run an ifconfig command that's also frozen up and hung.

Meanwhile sudo -i no longer works... In fact sudo anything just hangs, and I can't connect to my local mpd server anymore either. 

([Corrupt routing tables?](http://serverfault.com/a/65373) sure, why not... I'm too lazy to go back and diagnose the exact mechanism by which the wireless adapter was screwing up my machine)

I shut down the machine and that hangs too, trying to shut off apache, ntpd and samba. Out of frustration I try booting into windows.

I hop onto windows 7 and try to connect to the network from there. 

I get into negotiations with the router and... Actually no, to its credit the windows drivers for the wireless card managed to create some form of nonfunctioning unidentifiable connection monster for windows to claim that I was connected to...  I suppose that's a better fail case than half the machine freezing up and dying. 

By this point I've decided that my little USB wireless adapter has been damaged in the 10 minutes of transit and is malfunctioning. 

It's sleep time, so I'll research a new one in the morning.


### Internet Hell: Problem 3 ###

Hopped out of bed this morning and straight onto my laptop to see what I can get in the market of USB wifi dongles, in person, on a Sunday afternoon.

Every couple of minutes, had my connection to the router die on me. Die on me as in, the laptop still thinks I'm connected, the router's still taking new connections, but **nothing works anymore**

Okay so this one was just [interference from another local wireless network](http://unix.stackexchange.com/a/38145). Changed channel, everything's fine.


### Internet Hell: Problem 4 ###

> Hysterical Laughter

I went down to pbetch and picked up another asus wifi dongle.

I don't know why I got another one of these; the one that just broke is a usb-n13, and the drivers for it [cause kernel panics](https://bbs.archlinux.org/viewtopic.php?pid=1124701) in kernel > 3.3

I think I'm just a sucker for wireless cards that come with a linux driver on a disc in the box, so I don't have to run a twenty metre cable to the box to download drivers.

Anyway, I picked up an N-53 N600.... thing.  It runs on a slightly different driver, so maybe I can upgrade my kernel off of 3.0-LTS now. 

Got the dongle installed no problem. One thing to be said for these drivers - if you're happy running an ancient, crusty kernel, they're great: just compile and go.

..... Aaaand my network doesn't show up on the scan. I **swear** I had a great signal last night... Sometime between leaving the house to buy the wifi dongle and now, the router decided to freeze up and stop working.

Reboot the router. Network comes back. Connection stable. Okay. It's now 17:08 Sunday evening, but at least I'll be able to work tomorow... Right?
