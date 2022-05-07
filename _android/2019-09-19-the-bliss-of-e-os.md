---
layout: post
title:  "The Bliss of /e/ OS – The UnGoogled Android"
date:   2019-09-19 08:07:08 -0800
category: blog
tags: [android, phone_repair, roms,]
---
# The Bliss of /e/ OS – The UnGoogled Android
*Sept. 19, 2019*  

**Listen to this post. Narrated by me!**

<iframe src="https://anchor.fm/dctalks/embed/episodes/The-Bliss-of-e-OS--The-UnGoogled-Android--DC-Tech-Talks-Podcast---Ep--38-e5f1ot" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

One of the biggest factors I take into consideration before purchasing an Android phone is if it is supported by 3rd. party ROM’s. Previously I’ve run devices without Google Apps after installing LineageOS, which had significant speed and battery performance in addition to privacy upgrades. Last week I installed [/e/ OS](https://e.foundation/) on my Honor 5x after stumbling on it on Twitter. There’s a few aspects of this really unique OS that I feel merit a test for anyone who has a supported device.

The /e/ operating system isn’t just a custom ROM. They’ve developed an integrated ecosystem of default apps to replace typical Google services along with utilizing [MicroG](https://microg.org/) framework to help more apps work without access to Google Play Services.

This isn’t a full review of the OS, but my initial takeaways of what might be the most interesting attempt at a non-Google Linux mobile OS and something I think I’m going to stick with for the long run.

## The /e/ mission

Back in May /e/ OS made news when they announced [refurbished Samsung devices](https://www.androidauthority.com/ungoogled-refurbished-smartphones-986985/) for sale on their site with their ROM pre-installed. Normally in the aftermarket Android ROM world you would need to unlock (and maybe root) a supported device yourself, with varying level of instructions geared towards the special kind of geek that enjoys doing this type of thing. Selling a modern device with /e/ OS pre-installed makes this ROM accessible to any person at any technical savviness.

In addition to the pre-loaded devices, /e/ is also available to geeks that want to do the install themselves which is available for a [surprising number of devices](https://gitlab.e.foundation/e/wiki/en/wikis/devices-list). This is the path I chose, already owning one of the supported devices.

According to the /e/ website what separates them from other mobile operating systems is that they aren’t in the business of collecting or selling data while also being passionately open-source.  

> “We build mobile operating systems, apps and code that put users’ privacy first before profit.”  

They can really be defined as “UnGoogled Android”, which is a growing space in mobile platforms. Apple consistently advertises that it is not a data company, squarely targeted at Google. Other smaller companies such as Purism is also building their [Librem 5](https://puri.sm/products/librem-5/) as a privacy by design that is “…a fully free, ethical and open-source operating system that is not based on Android or iOS.” Purism and the /e/ Foundation aren’t the first OS’s to make this attempt to sell to a niche audience that is both privacy focused and tech savvy. Ubuntu, KDE and other Linux distros have attempted to make alternate mobile systems to very low success with Ubuntu dropping their mobile OS years ago.

What I think makes /e/ different is that they’re not creating a totally new operating system, instead removing Google from Android and replacing the Google framework with FOSS alternatives such as MicroG. This means nearly all Android apps will work out of the box, instead of other operating systems like Jolla or PureOS finding workarounds to enable apps on their platform. At the end of the day users want their apps to just work.

## Making apps work

At launch you’re given a very iOS interface. The BlissLauncher was developed by /e/ and have made it available in the F-Droid store for others to use. If you’ve ever used iOS you’ll feel right at home. Icons are large and square while the app drawer has been removed in favor of folders and everything right on the desktop. This is the one aspect of the OS I’m not fond of and dabbled in other launchers before deciding to stick with the default during my testing. I love the app drawer and the ability to place icons wherever I like. This launcher feels like iOS and with all of Google services stripped out I could just get an iPhone. However I like the customization of Android and this launcher feels like it removes my ability to customize.

Getting past the launcher the rest of the OS works wonders. The default apps are a who’s who of open-source Android applications forked for /e/ including the K-9 email client, Etar calendar and Chromium. You’ll even find a competent mapping application (MagicEarth) and a fork of GoodWeather.

The real stars of the show are the /e/ online services and MicroG.

MicroG is a replacement framework for Google Play services, Maps API, Google Cloud to Device Messaging, and geolocation tools that come in Android. This is crucial for an “UnGoogled” Android as many apps are using some, if not all, of these services for notifications, messaging and location services. Without a replacement most apps from the Play Store simply won’t work.

I know this first hand. In previous attempts to go mobile without Google I would consistent run into issues with my two favorite apps (Todoist and Imgur) that would refuse to work without access to any of the Google underlying frameworks. MicroG is an open-source replacement those frameworks allowing the user to install apk’s that depend on it to function. I don’t know enough about the code to give a detailed breakdown on how this works, but as a user this is just magic and solves one of the biggest obstacles, just making apps work.

Included with the default apps on /e/ is an App Store which seems to have full access to the Play Store plus apps only found on F-Droid. I can’t find any information on how their app store functions and how it pulls apps from the Play Store. Part of that challenge is their name and search engines flat misunderstanding of the name, making search nearly impossible. The only apps that look to be unavailable in the store are not free. Paid apps and games are not available, although I wouldn’t expect them any way.

I’m not sure why a user who is thinking about privacy and removing Google from their mobile device would then install Facebook, Spotify or Skype but you have that choice if any of those are important to you. As I mentioned above the only dealbreakers for me were Todoist and Imgur, with Imgur really being optional. My life would come to a screeching halt without Todoist so I was very happy to see it available and installed without any issues.

## Amazed by Cloud Services

For as magical as MicroG and the /e/ implementation is, by far my favorite aspect of the OS is their online services. From the beginning /e/ has made it clear that a mobile OS is more than just a skin on Android, but an entire ecosystem. Part of their ecosystem is a whole host of strong open-source cloud programs giving you a replacement for all the Google services not on the OS.

The ecloud offering is essentially a professionally managed NextCloud service with office, calendar, contacts and email capabilities. It truly is a Google replacement for Drive, Gmail, Keep and Calendar. This doesn’t just work on the device. You can log into ecloud.global in the browser or use NextCloud desktop applications to sync your information. I exported some contacts from my Gmail and imported via the browser which appeared on my device moments later. Everything works as you would expect a Google or Apple cloud service.

Seeing the NextCloud implementation was a double-win for me. First, using existing open-source programs instead of inventing their own means it comes with a broader ecosystem. Using the NextCloud client on my Ubuntu desktop and in the browser meant I didn’t have to live with one foot still in Google. Their instance also made me rethink my former NextCloud days as well. Secondly, seeing it professionally deployed and managed I finally see the real power of it instead of my half-baked attempts on my LAN. NextCloud has come really far and pro team maintaining it gives me confidence in their cloud service.

The forks of K9-mail and Etar also support the ecloud.global cloud services, plus tasks, notes, contacts and more.

## Here to stay

This experience has shown that “UnGoogled” Android can work. With MicroG and their App Store, I never felt like I needed to grab my laptop or tablet to do that one thing missing. I’m not much of a fan of the BlissLauncher but since its Android I can easily pick a different launcher that will allow me to customize as much as I want.

For me the real eye-opener was their cloud services. I realized that not only was I impressed at how it integrated with the device, but that I would happily pay /e/ for their cloud infrastructure. Even more intriguing is that if you wanted to self-host your own instance of ecloud there is a beta available. But for me, as long as /e/ proves their security, I would have zero problems paying them for their cloud service.

I’m a big fan of what /e/ is trying to do. Without the overhead of managing a full custom operating system and allowing the entire Android ecosystem to function on their devices while providing a FOSS cloud it checks every box I would want out of a mobile OS. I don’t think I’ll be removing it any time soon and if the cloud continues to work as well as it has in these last 7 days, I’ll probably just sink deeper and deeper into their ecosystem.  

* * *

### Contact me

Would love to hear from you on this topic!

**Email**: obscurednarration@gmail.com
**Twitter**: [@domcorriveau](https://twitter.com/domcorriveau)

### Digital marketing professional

Into digital marketing? Get a newsletter all about the best stuff in digital marketing over the last week plus deep-dives into this industry.

[Newsletter](https://corrteksolutions.com/marketing-mixer-newsletter/)
