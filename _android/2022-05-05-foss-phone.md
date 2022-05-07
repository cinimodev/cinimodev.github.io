---
layout: default
title:  "A (mostly) free Android phone"
date:   2022-05-05 08:07:08 -0800
category: blog
tags: [android, fossdroid, f-droid]
---
# A (mostly) free Android phone
*May 5, 2022*  

This is how I've been testing a completely free phone, plus numerous blockers and ways to force looking at various websites in a free way. 

## F-Droid
This is an obvious place for all the apps. But, I have found others that are in their own repositories. 

I've used Aurora Droid in the past, which makes adding other repos easy. But its very slow and buggy, which is saying a lot compared to the stock F-Droid app. So, I've just been adding the repos directly to F-Droid. 

##### Izzy on Droid
Add this link:

```
https://apt.izzysoft.de/fdroid/repo
```

This will enable apps like the Shade Launcher, [Warden](https://alternativeto.net/software/warden/), and SongTube.

##### Bromite
Add this link:

```
https://fdroid.bromite.org/fdroid/repo
```

Bromite provides build of stock Chromium and then their own version with more privacy and an adblocker. 

##### NewPipe
Add this link to F-Droid to add the NewPipe repository:

```
https://archive.newpipe.net/fdroid/repo/?fingerprint=E2402C78F9B97C6C89E97DB914A2751FDA1D02FE2039CC0897A462BDB57E7501
```

A YouTube viewer that blocks ads and keeps all list, views, and history on the device.

#### DivestOS

```
https://divestos.org/fdroid/official?fingerprint=E4BE8D6ABFA4D9D4FEEF03CDDA7FF62A73FD64B75566F6DD4E5E577550BE8467
```

New to me Android ROM that amps up privacy and security. It is similar to CalyxOS. This repo adds access to their custom apps, which includes different versions of Firefox and Chrome. The also have a couple of cool utilities for wiping data and scanning for malware. 


## Blockers
Been testing using [TrackerControl](https://trackercontrol.org/) to limit the data usage of apps. Also allows to block the app from accessing the internet altogether without root. 

I have [PiHole](https://pi-hole.net/) on my LAN and use it for adblocking at the DNS level. I have added several additional lists ontop of the the default list which includes blocking data to Xiaomi & Huawei, access to porn sites, known Q sites, plus various marketing trackers.

#### My list:
- https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts		
- https://mirror1.malwaredomains.com/files/justdomains		
- http://sysctl.org/cameleon/hosts	
- https://zeustracker.abuse.ch/blocklist.php?download=domainblocklist	
- https://s3.amazonaws.com/lists.disconnect.me/simple_tracking.txt	
- https://s3.amazonaws.com/lists.disconnect.me/simple_ad.txt	
- https://hosts-file.net/ad_servers.txt	
- https://raw.githubusercontent.com/chadmayfield/my-pihole-blocklists/master/lists/pi_blocklist_porn_all.list	
- https://raw.githubusercontent.com/chadmayfield/pihole-blocklists/master/lists/pi_blocklist_porn_top1m.list	
- https://raw.githubusercontent.com/kboghdady/youTube_ads_4_pi-hole/master/youtubelist.txt
- https://raw.githubusercontent.com/rimu/no-qanon/master/etc_hosts.txt	
- https://raw.githubusercontent.com/unknownFalleN/xiaomi-dns-blocklist/master/xiaomi_dns_block.lst	
- https://blocklistproject.github.io/Lists/ransomware.txt	
- https://blocklistproject.github.io/Lists/tracking.txt	
- https://raw.githubusercontent.com/cinimodev/huawei-block-list/master/huawei-block-host.txt

I am also blocking a little extra on a couple devices using the **Groups** feature in PiHole. This group is also blocking social media, Samsung, and Google. I am also looking into blocking additional services to assist with a fully locked down phone. 

The extra blocklists:
- https://raw.githubusercontent.com/StevenBlack/hosts/master/alternates/fakenews-gambling-porn-social/hosts
- https://raw.githubusercontent.com/RPiList/specials/master/Blocklisten/samsung
- https://raw.githubusercontent.com/nickspaargaren/no-google/master/pihole-google.txt


Here is a great list of resources to add to PiHole or other DNS blockers:

* [StevenBlack/hosts](https://github.com/StevenBlack/hosts)
* [blocklists.info](https://blocklists.info/)
* [ nickspaargaren/no-google](https://github.com/nickspaargaren/no-google)


Additionally, I have been using [UntrackMe](https://f-droid.org/packages/app.fedilab.nitterizeme/) that forces links to the big social media networks to the free no-tracking versions. For example Twitter goes to Nitter, Reddit to Teddit, YouTube to Invidious, etc. It can also be configured to force the links to other apps, like Twitter to Fritter and YouTube to NewPipe. 

**Testing**: I need to dig deeper into [Warden (App Management Utility)](https://f-droid.org/packages/com.aurora.warden/). This promises to do what TrackerControl does, along with a debloat utility. I think the tracker blocker will run the same and the debloat utility requires root. 

### App Replacements

- YouTube >> [NewPipe](https://newpipe.net/#download) This selection is tricky. The app is open source and it blocks ads. However, it is just a frontend for YouTube which means it doesn't completely hide all the info from Google. I am still looking into options that provide the same features as NewPipe, but with all requests going through [Invidious](https://github.com/iv-org/invidious).
- Twitter >> [Fritter](https://github.com/jonjomckay/fritter)
- Google Maps >> [Magic Earth](https://www.magicearth.com/) (not completely FOSS). Although this isn't truly free, the /e/ OS organization has selected Magic Earth as their maps app. Privacy is really important to the /e/ OS folks, so them selecting it is good enough for me. See why they chose Magic Earth [here](https://doc.e.foundation/maps)
- Gmail >> [K-9](https://k9mail.app/) Remember this is just an email client, the service can still see all your email content. K-9 won't fix Google spying on your email in your Gmail account.
- Chrome >> [Bromite](https://www.bromite.org/) for Chromium-based, or [Fennec](https://f-droid.org/en/packages/org.mozilla.fennec_fdroid/) for Firefox.
- Google Calendar >> [Etar](https://github.com/Etar-Group/Etar-Calendar) & sync with [DAVx5](https://www.davx5.com/) to Nextcloud
- Messages >> [QKSMS](https://github.com/moezbhatti/qksms) Traditional SMS messages are insecure. Using a different client doesn't fix that. 
- Google Drive file sync >> [Nextcloud](https://nextcloud.com/)
- GBoard >> OpenBoard
- Spotify >> [SongTube (Download Media from YouTube)](https://f-droid.org/packages/com.artxdev.songtube) or add your own music iPod style. I prefer [Music Player GO](https://f-droid.org/packages/com.iven.musicplayergo/)
- Reddit >> [Stealth](https://f-droid.org/en/packages/com.cosmos.unreddit/)
- Podcasts (Spotify, Apple, Google, Pocket Casts, etc.) >> [AntennaPod](https://antennapod.org/)
- Google Cloud Backup - [Seedvault](https://github.com/seedvault-app/seedvault). There is a catch with this one. You cannont just install it. Seedvault needs to be rolled into the firmware. So, the only way to use this is to find a ROM that has it baked in, or roll your own ROM.

## Misc. Apps
- OpenDocument Reader
- Simple Clock
- Simple File Manager
- Simple Gallery 
- Simple Calculator
- Zorin Connect
- Nextcloud News
- Nextclout Notes
- Binary Eye
- [Native Alpha](https://github.com/cylonid/NativeAlphaForAndroid) for seamless web apps

## Camera
There are Google Camera ports that take the on device image processing and other photo tools from Pixel devices and add the functionality to other phones. I'm not sure on the privacy of these apps, but the camera performance is night and day better. 

For more recent devices, use this list to locate the phone and the corresponding GCam port:

```
https://www.xda-developers.com/google-camera-port-hub/
```

For older devices, I've had a lot of luck with one of these including on phones still running Android 8.1:

```
https://www.celsoazevedo.com/files/android/google-camera/dev-suggested/
```

If GCam is needed for a super low-end phone, there are GCam Go ports that work all the way down to Android 7.0 here:

```
https://www.celsoazevedo.com/files/android/google-camera/camerago/
```

## De-Bloat
For devices that don't have a LineageOS version or cannot be unlocked, I have had a lot of luck using this tool to debloat the crapware that is blocked from being removed. It will clear up a lot of room on the device, run faster, while keeping the GApps functioning. I know this doesn't make it a "free" device, but it is definitely better than living with the preinstalled crap.

[universal-android-debloater](https://github.com/0x192/universal-android-debloater)

It is written in Rust and has a Linux version. The Linux version is just a binary that can be run in place. 