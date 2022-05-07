---
layout: post
title:  "Giving Anbox Android emulator a shot"
date:   2020-12-28 00:07:08 -0800
category: blog
tags: android, andbox, linux_desktop,
---
# Giving Anbox Android emulator a shot
*Dec. 28, 2020*  

**Listen to this post. Narrated by me!**

<iframe src="https://anchor.fm/dctalks/embed/episodes/Giving-Anbox-Android-emulator-a-shot-entmh9" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

**Subscribe to get all narrated posts**

[RSS](https://anchor.fm/s/8af59bc/podcast/rss) | [Spotify](https://gwth.us/dcttspotify) | [iTunes](https://gwth.us/dcttapple) | [Google](https://www.google.com/podcasts?feed=aHR0cHM6Ly9hbmNob3IuZm0vcy84YWY1OWJjL3BvZGNhc3QvcnNz) | [Pocket Casts](https://pca.st/p5Fy) | [YouTube](https://www.youtube.com/dominiccorriveau) | [Breaker](https://www.breaker.audio/dc-talks-podcast) | [Overcast](https://overcast.fm/itunes1450176844/dc-talks-podcast) | [Stitcher](https://www.stitcher.com/podcast/anchor-podcasts/dc-talks-podcast)

After seeing the news of a new Ubuntu-based distro using /e/ OS app store, my interest was piqued about running Android apps on my desktop. Having recently played around with screen mirroring on my Pop_OS desktop, running the apps directly seems like a much better experience.

Testing Ubuntu Web Remix with beta /e/ OS app store support has been fun, but I would rather have it on my desktop of choice. Which for the most part is the one I already have installed because I don’t want to go through all the work of configuring my computer. Pop_OS has been great and I haven’t seen a distro that has made me want to go through all that work for a DE change.

Using Anbox has been much better than running a full x86 Android OS in a VM as well, primarily because the apps function as just another desktop window instead of a fully virtualized environment on a secondary screen.
This is a very established way of installing Android apps on the desktop. You can build from source, but Ubuntu has a Snap available that works out-of-the-box.

## Install the Anbox snap
I ended up going the snap route, which installing the Anbox snap is very simple:
```
$ sudo snap install --devmode --beta anbox
```

There are a couple notes in the Git repo about running the snap, in particular it using `--devmode` and automatic updates.
* * *
> At the moment we require the use of --devmode as the Anbox snap is not yet fully confined. Work has started with the upstream snapd project to get support for full confinement.
>  
> As a side effect of using --devmode the snap will not automatically update. In order to update to a newer version you can run:
>  
> `$ snap refresh --beta --devmode anbox`
> Information about the currently available versions of the snap is available via:
>  
> `$ snap info anbox`
* * *

[Anbox Github](ttps://github.com/anbox/anbox/blob/master/README.md)  

## Install and Run Android Applications
Sideloading applications using `adb` is easy.  

`adb install someapp.apk`  

The Google Play Store will not work as is, because it relies on the proprietary Google Play Services, which are not installed. This is an important point, because Anbox also doesn’t come with MicroG GmsCore installed either. This is one aspect that I truly enjoy about using /e/ OS, which is able to run nearly any GSF dependent app. In recent tests on my Honor 5x running /e/ OS I haven’t run into any application that hasn’t worked, minus official Google Apps that I’m not installing on my Google-free Android instance.

There is a lengthy thread on the [Anbox Github](https://github.com/anbox/anbox/issues/27#issuecomment-293486105) about this exact topic, which reiterates the point that the user should implement GSF or MicroG and is not the responsibility of the Anbox developers.

F-Droid is obviously a source of FOSS apps, but there are three other locations to get apk’s.

#### Aurora Store
Can download this store from the F-Droid repo. So technically could download F-Droid apk, install it and then use it to install the Aurora Store. There are two Aurora apps. Aurora Store is for the mirror of Google Play. Aurora Droid is a better designed UI/UX for F-Droid.

The Aurora Store also lists if the app is depenedent on Google Framework (GSF). These apps will not work in Anbox.

#### APKMirror
Super popular place to download APK's. They also have an official installer. I have not used APKMirror, the site leaves much to be desired in design and interface. But, can download directly from the site and can sideload the apk from CLI.

#### Uptodown
I just learned of this store after reading the [Vivaldi Browser blog](https://vivaldi.com/blog/app-store-alternatives-uptodown-vivaldi/), which I stumbled on after installing the browser after a recent announcement about integrating a full email client into the browser.

Well, actually it comes from following a new list on Twitter which someone else had retweeted the blog, which I only saw because I had just installed the browser on my primary desktop and was paying extra attention to any mentions of Vivaldi. Then, once on the blog about the integrated email client, I saw another post that mentioned they also post their Android APK on Uptodown.

This site will allow direct apk downloads from the site or using their installer. Very similar to APKMirror, just nicer looking. To be honest, what caught my eye was an app stating they officially publish to Uptodown. I have not seen this for 3rd. party app stores, other than FOSS apps publishing to F-Droid.

I think what is most interesting about this site is the official nature. Not only do they have official publishers submitting apps, but they tout again and again that its legal and they have a security stack in place. They publish the SHA256 and signature, so you could verify your download. That doesn't mean much if the app was corrupted before upload. But, I guess they are saying they would catch that, then can verify signature to eliminate MiTM attacks.

## GSF dependant apps troubles
I spent a significant amount of time attempting to get MicroG and the associated core services working in Anbox with no luck. Well, I had lots of luck installing MicroG and about 95% of the services.

First I tried adding the [MicroG repo](https://microg.org/fdroid.html) to F-Droid inside Anbox. But F-Droid would never refresh and therefore the MicroG apps were never made avaialble.

There is a way around, though. Using F-Droid I installed the Aurora Droid store in Anbox, which is just an Aurora frontend for F-Droid. You can get this app inside of F-Droid, too. Once you launch Aurora Droid you can select a series of repos or add your own. In the pre-defined repos is the MicroG repo. Tap the checkbox and sync, then install all the MicroG services.

Inside the MicroG app there is a self-check feature which makes it super simple to make sure you have everything needed to use the drop-in replacement for GSF. The one hangup I ran into was signature spoofing. [Anbox directly calls this out](https://github.com/microg/GmsCore/wiki/Signature-Spoofing) in their installation notes, with Anbox not listed as an official ROM that supports signature spoofing.

I tried all three of the options listed on the Abox signature spoofing page to get MicroG signature spoofing complete. Alas, I was unsuccessful. This doesn’t mean its not possible, all three of the repos for signature spoofing specifically say they can be used for MicroG. The problem is with Anbox. I’m sure there is a way around it, but I can’t figure it out and my attempt at running Android apps that require GSF is at an end.

It does work fantastically for F-Droid and non-GSF dependent apps. But the number of mobile apps I would run on my desktop that don’t already have a native version and/or replacement is minuscule.

I have HUGE hopes for Ubuntu Web Remix and a direct collaboration with /e/ OS app store. Instead of attempting to roll-my-own Anbox + MicroG, this distro could solve that problem, including making the code available for others to easily implement a similar framework. Especially for a distro based on Ubuntu, like Ubuntu Web Remix and Pop_OS.  

* * *

### Contact me

Would love to hear from you on this topic!

**Email**: obscurednarration@gmail.com
**Twitter**: [@domcorriveau](https://twitter.com/domcorriveau)

### Digital marketing professional

Into digital marketing? Get a newsletter all about the best stuff in digital marketing over the last week plus deep-dives into this industry.

[Newsletter](https://corrteksolutions.com/marketing-mixer-newsletter/)
