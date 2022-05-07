---
layout: post
title:  "Gnome theming and tweaks on Pop_OS"
date:   2021-10-25 08:07:08 -0800
category: blog
tags: [linux_desktop, pop_os, gnome, gtk]
---
# Gnome theming and tweaks on Pop_OS
*Oct. 25, 2021*  

Although the default theming from Pop_OS is nice and hasn't been a problem for the 2 years or so I've been daily driving it, for whatever reason I got the urge to play around with new Gnome themes. I believe this was largely driving by an interview with Pop_OS principal engineer [Jeremy Soller](https://twitter.com/jeremy_soller) on the [Opt Out Podcast](https://www.optoutpod.com/coreboot-foss-firmware-pop_os-and-system76-w-jeremy-soller-special/).

In the interview, Jeremy Soller indicated that he has a vision that Pop_OS isn't necessary a distro, but a series of configurations and tools that can be applied to any distribution. Rather than thinking of Pop_OS as a complete package, like Windows or MacOS, my desktop really is something I own and can do what I want with it, which includes changing the look and feel. 

This idea is what originally made me fall in love with Linux and over the years I've kind of lost touch with it. More on that later. 

The guide below is a mix of cli and GUI apps for enabling themes and custom icons. You can do all of this through cli, but this is a desktop PC and if I'm customizing my theme using a GUI application makes sense. 

### Getting ready
First, create two new folders in your home directory. These are going to be used as the location for any themes or icons files for your user. 

```
$ mkdir ~/.themes  
$ mkdir ~/.icons  
```
If you would like to make these adjustments system-wide you will use the directories in `/usr/share`. I don't typically configure things globally since **A)** I almost never have multiple users, **B)** I try to run as many things as a can as user without any escalated privileges. 

Next, we need to install a tweak tool. You can do this without the tool, but as mentioned above, I prefer to do this through the GUI so I know how to make the changes again later if necessary. Since I won't be changing this frequently, I will absolutely forget the gtk commands to change the theme or icons. My default behavior is to hit the super key and search appearance, not look through my bash history. 

Gnome Tweaks will handle this job just fine.

```
$ sudo apt install gnome-tweak-tool
```
Now we need to install a Gnome extension called [User Themes](https://extensions.gnome.org/extension/19/user-themes/). The User Themes extension enables loading themes from the user directory, not just the global location. 

Pop over to the website and flip the switch to "on". Good enough for me. 

Last is to enable the extension. Open the Extensions app on Pop_OS and make sure it is toggled on. The Extensions addon is enabled in Pop_OS by default, so just hit Super and type "extension". 

### Finding and enabling themes
Custom themes for Gnome is nothing new and there are many places to get themes and icon packs. For me, I saw a theme on Twitter I really liked, all due to my fanatical adoration of anything Synthwave. Seeing the purple gradient in these screenshots immediately got my attention. 


<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Pop!_OS 21.04<br><br>By: @zwenderjuniorz<br><br>Tema / Theme: Pop, Sweet-Dark<br>Ícones / Icons: Tela-circle-black-dark<br>Shell: bash<br>Terminal: gnome-terminal<br>•<a href="https://twitter.com/hashtag/Linux?src=hash&amp;ref_src=twsrc%5Etfw">#Linux</a> <a href="https://twitter.com/hashtag/FreeSoftware?src=hash&amp;ref_src=twsrc%5Etfw">#FreeSoftware</a> <a href="https://twitter.com/hashtag/OpenSource?src=hash&amp;ref_src=twsrc%5Etfw">#OpenSource</a> <a href="https://twitter.com/hashtag/LinuxSetup?src=hash&amp;ref_src=twsrc%5Etfw">#LinuxSetup</a> <a href="https://twitter.com/hashtag/System76?src=hash&amp;ref_src=twsrc%5Etfw">#System76</a> <a href="https://twitter.com/hashtag/COSMIC?src=hash&amp;ref_src=twsrc%5Etfw">#COSMIC</a> <a href="https://twitter.com/hashtag/LigaLinux?src=hash&amp;ref_src=twsrc%5Etfw">#LigaLinux</a> <a href="https://t.co/7LEhrVo1b5">pic.twitter.com/7LEhrVo1b5</a></p>&mdash; O Pinguim Criativo (@PinguimCriativo) <a href="https://twitter.com/PinguimCriativo/status/1452285740327522314?ref_src=twsrc%5Etfw">October 24, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 


[Gnome-Look.org](https://gnome-look.org) is probably the easiest and most comprehensive place to look for customization on the desktop, which is also where I found the [Sweet Dark theme](https://www.gnome-look.org/p/1253385/)

Enabling a theme is simple:
1. Find and download the theme you wish to use.
2. Extract it and place the extracted directory in `~/themes`.
3. Open Gnome Tweak Tool, select the Appearance tab, and use the drop downs to choose the theme you just downloaded. 

Go through the same process if you would also like to adjust the icons with the only difference being the directory you place the extracted files (`~/icons`). Icons are a little more challenging because there may not be an icon for every app you have installed, which will break the *aesthetic*. 

Personally, I was drawn to [Candy Icons](https://www.gnome-look.org/p/1305251) which is made by the same person as the Sweet theme and to [BeautyLine](https://www.gnome-look.org/p/1425426) because it matches the Synth feel. 

At the same time as I enabled the Sweet Dark theme on my desktop, I went ahead and added the same [theme to Firefox](https://addons.mozilla.org/en-US/firefox/addon/sweet-dark/), obviously made by the same person. 

While you're at it, might as well add a new wallpaper on the desktop from the [Outrun sub-Reddit](https://www.reddit.com/r/outrun/search/?q=wallpaper&restrict_sr=1&sr_nsfw=).

Enjoy!

<iframe width="560" height="315" src="https://www.youtube.com/embed/FoXvsBN-dA0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>