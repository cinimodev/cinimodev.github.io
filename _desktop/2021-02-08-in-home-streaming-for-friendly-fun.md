---
layout: post
title:  "Streaming at home with NDI and virtual cams for family fun"
date:   2021-02-08 08:07:08 -0800
category: blog
tags: [obs, ndi, virtual cam, linux_streaming, linux_desktop]
---
I’ve used [OBS](https://obsproject.com/) for a long time for game and screen recording. I was well aware that was barely scratching the surface of what it can do. Yet, that’s basically all I needed it for, mostly for screen recording training videos. I never had a reason to go deeper into OBS, but now I’ve spent my entire vacation learning deep diving after running some fun experiments based on ideas I had while watching a few of my favorite streamers. In particular, virtual cams and NDI streaming.

Now that I’m playing more games with my kids, plus spending several hours a day in video conferencing for work, these two features of OBS has made it so much more fun. I’ve been using the NDI streaming to record my daughter and I play Minecraft, while using virtual cams to add overlays on my Zoom calls for work. Even though it is a flex, I love adding effects in team meetings like snow and looping gifs during the holidays.

Instead of writing a huge blog, with technical details and how to configure it all, there are a ton of great resources out there already. Rather, I’ll just give a quick synopsis of what I’m using it for then drop some links that I’ve found useful for configuring.

## Linux setup

You can absolutely install OBS, FFMPEG, NDI Source, v4l2loopback, and any of the other components manually on your Linux desktop of choice. For me, I never wanted to spend that much time setting everything up, plus troubleshooting whatever doesn’t work. Since I’m on an Ubuntu derivative, I just snap install obs-studio and literally everything I could ever need or want in my setup mostly done. There are just a couple things to configure after installing, which is all clearly laid out on the [Snapcraft.io](https://snapcraft.io/obs-studio) page.

For some reason I didn’t follow this advice when I first set it up and struggled to get NDI Source configured. The same with virtual cameras, but more on that in a minute. The snap is a little slow to open, but once its rolling everything just works.

One of (or maybe the only) maintainer of the OBS snap is famed Linux guru and dare say “Linux Influencer” [Martin Wimpress](https://wimpysworld.com/). He has a fantastic livestream/video of his OBS setup, which is well worth a watch.

<iframe width="560" height="315" src="https://www.youtube.com/embed/mduyk66lvb0" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

In addition to his livestreams, Martin also has a Discord server with a dedicated channel for Linux streaming and OBS discussions. If you are getting serious about your streaming setup, definitely give the channel a follow.

[Wimpy’s World Discord](https://wimpysworld.io/discord)

## NDI Source

Essentially, this allows you to enable another PC on your LAN as a source in OBS. This can be used to lessen the load on one PC that would be doing the heavy lifting of the game, streaming, and recording. You could solve this by getting a capture card or you can use NDI streaming on your LAN to funnel your game play to a separate machine that only has to handle passing the stream to Twitch, YouTube, or wherever. This can also be used to have multiple machines feed their screens to a single OBS Studio and then you can do scene switching and other effects on top of the streams, which is exactly how I use it.

My 5 year old daughter is crazy about Minecraft. Originally she was playing it by herself and occasionally I would sit next to her. As a certified Minecraft junkie myself, I eventually setup a vanilla server on my homelab then later adding a map for Stampy’s Lovely World. Now my daughter and I can play together, on our own computers, in a playground she adores.

A quick aside, there is a fantastic [Docker image](https://github.com/itzg/docker-minecraft-server) for running a Minecraft server. Using this container you can setup vanilla or modded Minecraft servers, along with a ton of other customizations. I run this on my LAN with the Stampy map, plus a coulpe other Forge servers with various mods for us to play. It is well documented and so much fun to build out with my little one.

Naturally I wanted to record these game sessions. Using OBS NDI I have both of our streams going into a single OBS instance and tiling the feeds, along with some overlays I customize occasionally. I’m extremely hard-of-hearing so we use Mumble to voice chat together in-game, even though we sit very near each other. This way I can crank her volume way up and hear everything she’s saying. This also means I can easily integrate our microphones into OBS as audio sources and in the end I have a great looking and sounding recording I will cherish forever.

With this setup I also enable the OBS monitor into fullscreen, then pass it along to our family Discord so Aunts, Uncles, Grandparents, and our extended family can join in on the watch party. With everyone being distant, this has kept people close while also introducing more of the family into something their granddaughter or niece enjoys.

Setting up NDI stream output is in the notes of the OBS Studio Snap. Once you’re in OBS, here is a short guide for enabling and using it.

[Create NDI Stream Output with OBS Studio](https://streamlabs.com/content-hub/post/create-ndi-stream-output-with-obs-studio)

## Virtual Cams

Of course if I’m doing fun stuff with OBS for personal use, why not start using it at the office too. It was actually this video by Stephen Helwig that got me excited about virtual cams.

<iframe width="560" height="315" src="https://www.youtube.com/embed/9thyPmpJcGQ" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Here’s a few things I’ve learned about virtual cams:

- Make sure to have the v4l2loopback dkms module and other bits installed.
- Follow the instructions in the snap notes to make sure the v4l2 modules are loaded at boot.
- Don’t forget to enable virtual cams before starting the program you want to pass the video to.
- Not every program, browser, or service supports virtual cams.

That last bit is important. I have only been able to pass a virtual cam to Zoom and Discord, not Google Meet unfortunately, and only in Firefox. No matter what tweaks I do I cannot get the virtual cam to appear in Chrome (or variations of Chrome) or in the dedicated desktop apps, even for Zoom and Discord.

It only works in Firefox and with specific services.

Now when it does work, it is awesome. I don’t give a lot of presentations for virtual conferences. I do give a lot of presentations at my job for internal employees, though. For those, I use the virtual cam and then use keyboard shortcuts to dedicated scenes for cam only, cam with lower thirds, cam with PowerPoint, PowerPoint only. It is so much simpler to switch scenes than to share screen, stop sharing, then share again when switching in Zoom or whatever video conferencing system.

When I was working in the office, I could give really good in-person presentations. I also worked hard at getting good at whiteboarding meetings. Now that I’m fully remote, I’ve been struggling to get the same skills and effect of a great in-person presentation over to a virtual one. Using OBS virtual cam has helped me with that, including dedicating a source to a digital whiteboard along with a stylus or for when I want to whiteboard for real, a separate source that is a second webcam pointed at my real whiteboard on my wall.

## More to come

This is a fraction of what OBS can do. I didn’t even mention the scene transitions or browser sources. Next up for me is integrating my tablet into this flow with the [StreamControl](https://play.google.com/store/apps/details?id=dev.t4ils.obs_remote&hl=en_US&gl=US) app on my tablet for better scene switching. Additionally, I’d like to use it more for our family Among Us games so more friends and family can participate, even if they don’t want to play, without exposing our game to the open internet.

Stay tuned to this post, I’ll continue to update as I experiment and find new useful guides and information.

## Links and sources summary

- [Martin Wimpress](https://wimpysworld.com/)
- [Wimpy’s World Discord](https://wimpysworld.io/discord)
- [Create NDI Stream Output with OBS Studio](https://streamlabs.com/content-hub/post/create-ndi-stream-output-with-obs-studio)
- [StreamControl](https://play.google.com/store/apps/details?id=dev.t4ils.obs_remote&hl=en_US&gl=US)
- [Snapcraft.io](https://snapcraft.io/obs-studio)
- [OBS](https://obsproject.com/)
- [Docker image](https://github.com/itzg/docker-minecraft-server)
- [Video – Leveling Up Your Virtual Presence with OBS Studio](https://youtu.be/9thyPmpJcGQ)
- [Video – Q&A: Tour of my OBS Studio setup on Linux](https://s.w.org/images/core/emoji/13.0.1/svg/1f427.svg)](https://www.youtube.com/watch?v=mduyk66lvb0&feature=emb_title)

* * *  

### Contact me

Would love to hear from you on this topic!

**Email**: [obscurednarration@gmail.com](mailto:obscurednarration@gmail.com)  
**Twitter**: [@domcorriveau](https://twitter.com/domcorriveau)  

### Get more

These blogs are just the tip of the iceberg. To go deeper and hear more stories around the tech and life around these journals, check out the DC Tech Talks podcast.

[Podcast RSS](https://anchor.fm/s/8af59bc/podcast/rss)  
[Apple Podcasts](https://gwth.us/dcttapple)  
[Spotify](https://gwth.us/dcttspotify)  

### Need even more?
Check out my sister podcast [Go With The Heat](http://gowiththeheat.com/). We just relaunched the show after going through all of the 80’s goodness that was Miami Vice. Now you'll find the best of the best from the greatest era of action movies.

[Go With The Heat Podcast](http://gowiththeheat.com/)  

### Digital marketing professional

Into digital marketing? Get a newsletter all about the best stuff in digital marketing over the last week plus deep-dives into this industry.

[Newsletter](https://corrteksolutions.com/marketing-mixer-newsletter/)  
