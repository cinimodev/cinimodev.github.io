---
layout: post
title:  "Why I jumped from Pop_OS to Zorin OS 16"
date:   2022-01-12 04:07:08 -0800
category: blog
tags: [linux_desktop, pop_os, zorin_os, ubuntu_based, zfs]
---
# Why I jumped from Pop_OS to Zorin OS 16
*Jan. 12, 2022*  

For the past few years I've been using Pop_OS on my primary desktop and I've been really happy. It has been solid as a rock, every update is smooth, and it seems to have more polish than other distros. However, in the last few weeks I've switched from Pop to [Zorin OS 16](https://zorin.com/) due to breakage of my workflows from updates. There is nothing wrong with Pop and it is still a great desktop OS. But it is not for me. 

I think that is the key point here. The direction of the team and the customer they have in mind don't match me. There are lots and lots of people it serves and does so fantastically. It is just not for me. And this is something missed in a lot of distro news, reviews, and breakdowns. If it is not for you, then that doesn't mean there is something wrong with it. It is just not for you. A recent example is all the coverage of [Linux Mint and their Firefox deal](https://blog.linuxmint.com/?p=4244). The Mint team is clearly against Snap and what they are building is going a different direction. If you don't like it, that distro is not for you. 

## My setup and workflow breakage
On my main workstation I have three ZFS pools for all of my files. Each pool is dedicated to a type of data and is configured so if I lose a drive, I don't lose all of my data. I've compartmentalized the pools based on the category of work. One pool is for my Google Drive and Nextcloud files, the second for content production, and the third for containers and VM's. I prefer this setup because I know I have data integrity for the files I need to do my job, access and plenty of storage for my content production, plus a pool that is just for playing around with various server and self-hosted stuff.  I also get the benefit of having all of my data outside my primary OS drive. So I can wipe at anytime, remount the pools, and away I go. 

Recently, Pop_OS has decided to push Linux kernels to the OS faster than what their base of Ubuntu does. This is important to them because they are known for being a great option for gaming and they have their own hardware they ship. Newer kernels mean better support for new hardware and the latest drivers for gaming. They have been able to roll out kernel 5.15 and are hot on the heels of 5.16. 

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Definitely going to evaluate 5.16 for Pop!_OS tomorrow ;-) <a href="https://t.co/oS7KJ0OnTH">https://t.co/oS7KJ0OnTH</a></p>&mdash; Jeremy Soller (@jeremy_soller) <a href="https://twitter.com/jeremy_soller/status/1480330088868630529?ref_src=twsrc%5Etfw">January 10, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 

When they updated Pop kernel 5.13 to 5.15 and my ZFS pools broke. This is nothing they did, except roll a newer kernel than what `zfs-dkms` and `zfsutils-linux` support. For a day or so I struggled to figure out what was going on. For me this was worse than my Nextcloud server going down. If that happens I have backups of the files locally in a ZFS pool. I can work locally until I get the server fixed, then sync all my new files. Not being able to mount my ZFS pools mean the files are totally inaccessible on my local machine. The drives are there, they work fine, my OS doesn't recognize them. 

For a week I booted into a previous kernel (5.13) and worked fine. The only trouble was I had to remember to boot the older kernel every time I turned off my PC, which turned into booting it and then rebooting when I remembered I needed to go back to 5.13. 

But then a week turned into a month. In that time another update purged 5.13 from my system and I had no choice but to use 5.15 and have zero ZFS support. The OpenZFS team wasn't ready to support 5.15. The next version came out and supported 5.14 at 6 weeks into my pools being offline. It completely broke all my workflows and was totally untenable. After a couple months OpenZFS support for kernel 5.15 was launched and I jumped on it right away and updated to Pop_OS 21.10 at the same time. 

What a glorious day. For about 10 minutes.

On first boot I imported the pools and everything worked, with all my data right there waiting for me. I had to drop many new files into the pools and then allowed all the syncing to happen. I had spent a lot of time working directly in the browser (which I hate), so a lot of new files needed to be downloaded. Things felt normal again. 

Part of the update to Pop_OS 21.10 is to Gnome 40. There has been much debate over Gnome 40, which I generally don't care about except for the extensions. A lot of the extensions I use everyday (like Emoji Selector which I will never apologize for) are not ready for Gnome 40. So again, workflow breakage. 

I was supremely frustrated. I had my desktop *exactly the way I wanted it* and the (completely warranted) decisions by others took it away. 

I get it, these are minor fixes and with time a lot of them do get fixed. But I had *exactly what I wanted*. I like my workflow. I don't want to change. I also don't like to sit down to do work and have to spend my time troubleshooting what was working yesterday and why it is not working today. I don't think fixing my workstation is fun. I have a separate laptop that is just for experimenting and that is okay to disrupt. My primary desktop? Needs to be rock solid and glacial with updates. 

This is not to say I don't like updates altogether. I just don't mind being 6 months or a year behind. All of my computers are hardware from at least a half decade ago. I have a budget of exactly $0 for new hardware and focus on always using upcycled or refurbished hardware. It is something I talk about a lot.

<iframe width="560" height="315" src="https://www.youtube.com/embed/gRUlyKbmO2s" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

These frequent kernel updates had me concerned. How long until something is broken again? Which update will break access to my ZFS pools again? 

I can't live like this.

## Where to next after Pop_OS
To avoid these kinds of disruptions is also why I don't use a rolling distro or even something close like Fedora. The more I thought about it I realized what I wanted was a LTS Pop_OS. I want the care and quality in a desktop environment, but with LTS underpinnings. I don't need the latest hardware support. Plus, with all the new Linux app packaging, I can get the latest software without having faster OS updates. 

I wrote up a short wishlist:
1. LTS kernel for the reasons above. 
2. Ubuntu-based. Nothing against the other distros, I'm just super used to `apt` and the directory structure in Ubuntu-based systems. I know the differences are minor, but it takes time to learn and I just don't want to. 😉
3. A quality software center. The Pop_OS software center truly spoiled me and I've gotten used to not jumping to the command line to install new apps, especially having a connection to Flathub.
4. Extra polish on the UI and UX of the desktop environment that is not Gnome 40+. I know I will eventually get there, but I have no problem waiting until some of my favorite extensions are either updated or have been integrated into the DE.

I realize theoretically I could setup Pop with an LTS kernel. Not interested. That is guaranteed to break at some point. I could also just go to the standard Ubuntu LTS. I'm not really interested in this either, although I did think about it. For one, the Ubuntu desktop seems to be lacking some pizazz. I mean, let's face it, Ubuntu is ugly. I also don't like how aggressive the push is for Snap. I use many Snaps, that is not a problem. But I don't like thinking I am installing a `.deb` and actually getting the Snap. I don't like having to figure out why something can't access files, connect to another app, or why it is opening so slowly only to find out Ubuntu gave me the Snap without telling me. There is absolutely a place for snaps, I want control over it though.

After a few days of thinking about other distros I've used before, I was hit with a lighting bolt. Isn't this what Zorin OS tries to be? It uses LTS Ubuntu and heavily tweaks the Gnome experience. I fired it up in a VM and was instantly impressed. Smooth and fast, looks great, and the software center is fantastic. In fact, the software center has the standard repos, Snaps, and Flatpaks and gives you the abiltiy to choose which version you want to install. 

I was immediately in love. 

I wiped my laptop and transitioned it over to Zorin. Everything has worked, including my favorite emoji extension 😎. This is not to say it doesn't have some rough edges. But, with the LTS kernel I am not concerned about breaking my ZFS pools and with a slower update cycle I'm likely to see other breakage unless something needs the absolute latest driver, firmware, or kernel module. I doubt it since my PC is an AMD CPU and GPU from 6 years ago. 

I am confident now I can switch to Zorin on my workstation and be comfortable. 

## Final thoughts
As I mentioned above, there is nothing wrong with Pop_OS. It is just not for me. Or at least, it is not for me anymore. They are going to a place I cannot follow. 



I have a device that is dedicated to moving fast and breaking things, but I don't need that on my the PC where I sit down to do serious work. Zorin has truly been a great experience and looking at their distro and business model, it feels like I can stay here for a long time. 

With Flatpak, Snap, and AppImages, I'm not concerned with needing faster OS updates. If a bit of software releases a big update, I know I don't need to update my OS, go find the latest PPA or build from scratch, just to get the experience. I don't mind being behind if it means I have less disruption.   
