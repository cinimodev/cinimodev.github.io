---
layout: default
title:  "Building the ultimate Android gaming console with a Nexus 5x & Razer Kishi"
date:   2022-05-06 08:07:08 -0800
category: blog
tags: [android, retro_gaming, android_gaming, game_streaming]
---
# Building the ultimate Android gaming console with a Nexus 5x & Razer Kishi
*May 6, 2022*  

I have been completely enamoured with the seriously amazing Android-based handheld retro gaming consoles. The idea of using Android as the base for a mobile retro gaming console inspired me to build my own using an old phone and an extendable mobile gamepad. This guide is a complete rundown on the OS, Android tweaks, emulators, and more to get just about any Android device in shape for a full retro gaming console. 

There are lots of all-in-one packages out there, such as the [GPD XP](https://www.androidauthority.com/gpd-xp-2732676/), [Retroid Pocket 2+](https://www.goretroid.com/collections/frontpage/products/retroid-pocket-2-plus-handheld-retro-gaming-system), and the various devices from [Anbernic](https://anbernic.com/). There is even a guide for setting up a [Steam Deck as an emulation machine](https://www.emudeck.com/). But I had the parts for this build already lying around and turned out to be a really fun project in which I learned a lot about emulation in general. 

## Hardware
For this setup I am using an absolutely ancient 32 GB [Google/LG Nexus 5x](https://www.gsmarena.com/lg_nexus_5x-7556.php) and a [Razer Kishi](https://www.xbox.com/en-US/accessories/mobile-gaming/razer-kishi) gamepad. This combination is perfect for my setup as the phone can be dedicated to gaming and I already had it. Because it is a Nexus device, there are tons of ways to unlock, root, and debloat down to the bare minimum to make it exclusively for gaming. It also has a USB-C port so it will work with the Kishi. Last is it is still decently easy to open and replace the battery. I've done it a couple times previously. Replacement batteries are getting long in the tooth and at some point I will probably have to retire this device. 

I love being able to take a phone from 2015 and save it from the landfill. It has a 1080p screen, dual band wifi, and is extremely light in the hand. There is no reason to buy a new device for this kind of build, unless you are looking to play some very specific, resource intensive games. Otherwise, PSX and lower emulators will work great. Game streaming is perfect and there are plenty of native Android games like Don't Starve that will work fine.

The only downside is that I can't for the life of me get charging passthrough to work with the Kishi and Nexus 5x. Which means I have to take the phone out to charge. I wish I could get it working and using a newer phone from the approved list would definitely be an upgrade. However, I got the Kishi on sale for under $50 and already had the phone. For the cost I'll be fine with removing the phone to charge. 

## Android Setup
#### Step 1: Install custom ROM  
This is my preferred way because it will clear out all bloatware and remove a lot of various Google/Carrier nonsense running on the device. It will also improve battery life. I install [LineageOS](https://wiki.lineageos.org/devices/bullhead/) with the pico GApps to get the absolute minimum running ROM. 

I am using an [unofficial build ](https://forum.xda-developers.com/t/rom-unofficial-lineageos-15-1-for-nexus-5x-bullhead.3724575/) of LineageOS for the [Nexus 5x](https://forum.xda-developers.com/c/lg-nexus-5x.4737/) since official support ended quite a while ago. I started using this unofficial build because there are some awesome people still publishing LOS updates for it. It is still running LOS 15.1, but getting LOS updates monthly.  

#### Step 2: De-bloat & disable unnecessary apps  
After installing the custom ROM, I then use [Universal Android Debloater](https://github.com/0x192/universal-android-debloater) from [0x192](https://github.com/0x192) to remove any unnecessary apps I don't need to have on a console. This is for things like the stock Music, Calendar, Phone, and message apps. In addition, using this software I can remove any background running apps that are for things I won't need like SMS notifications or Google account sync. 

You need to be cautious with what gets removed because it could cause unstable behavior with other apps that rely on the items removed. Luckily you can just factory restore and all are returned. Just make sure to test as much as you can before really diving in with RetroArch setup and other modifications. Make sure you audio works, bluetooth devices still connect, wifi speed is what is expected, etc.

For other apps that you might need at some point, I just disable them in Settings. For example I left the Email app just in case it will be useful for my gaming accounts to get the emails on the device. I might want it later, so left it installed and then disabled it. Do this for any apps that cannot be debloated as well. 

Last for this section is to be aggressive with putting apps to sleep. To maximize battery life and free up system resources I use the [SuperFreezZ App stopper](https://www.f-droid.org/en/packages/superfreeze.tool.android/) on [F-Droid](https://www.f-droid.org). I use this to put apps to sleep as fast as possible for the apps I have to have around. Like the F-Droid app. I need it to be on the device and active for app installs and updates, but I don't need it running in the background. 

Be super cautious using this app, though. If you are using it to put core/system apps to sleep you will use **more** battery than if you just allowed them to run in the background. Think things like the Play Store. This is supposed to run in the background all the time and will continually restart itself every time it is put to sleep. 

#### Step 3: Adjust Android
Here are a list of tweaks I do to Android modifying the apps that are running on the device:
1. **Change screen settings.** Go to Settings ➡ Display and adjust the how long the sleep stays awake (I like mine at 5 min.). 30 seconds is too short and super annoying to unlock the screen all the time. Disable Adaptive Brightness, LiveDisplay, Ambient display, Tap to sleep, and Wake on plug. Next, tap on Expand desktop, enable it, and set the desktop style to "hide both". This will maximize the screen and hide the top/bottom bars. You can still swipe to access, but won't be visible all the time. 
2. **Adjust battery optimization.** In addition to the SuperFreezZ app, Android also has its own battery optimization settings. Go to Settings ➡ Battery and then tap on the three dots in the top right and choose "Battery optimization". Then change the top menu from "Not optimized" to "All apps". We want Android to optimize essentially all the apps, minus anything that should run 24/7.  So the SuperFreezZ app should not be optimized so it can function correctly.
3. **Adjust notifications.** I detest notifications across the board, especially on a gaming device. Go to Settings ➡ Apps and Notifications and go through each app and turn off notifications. After you install other apps, you will need to do this again for each new install. Make sure to do this for the Google Play store and Google Play Services which both have a *ridiculous* number of notification categories. Last is to turn on Do Not Disturb mode in the quick settings. Pull down and enable DND with "Alarms only". 
4. **Turn off services.** Go to Settings ➡ Connected Devices and turn off NFC, Nearby Share (I use an alternate solution), and bluetooth. I don't plan on having headphones or other peripherals connecting wirelessly to the device, so I turn both off to save battery. Also, since this device will not have a SIM card, disable mobile data and location. I also turn off Find My Device, and Backup syncing to Google. Last is turn on Airplane Mode just to disable as much as you can.
5. **Misc. Home and unlock adjustments.** Since this is a gaming device, it will almost never leave my house, I'm not concerned about losing it or it being stolen. Plus, the device will almost always be connected to a gamepad, so reaching the fingerprint sensor on the back is a PITA. So, I just disable phone lock security. Using the Razer Kishi I can just push the Xbox button and the screen will unlock. I also like the home page to auto-rotate, so long press on the home screen, choose "Home settings" and allow screen rotation on the home screen.  

## File transfer & remote management
Playing retro games is one of the main reasons for building this Android console. This means transferring files, ROMs, apk's, and more will happen frequently. Of course I can always plug the phone in via USB to a computer to transfer, but I prefer to have a wireless setup. I have two apps setup to do this from my Linux computers. 

#### Warpinator
Developed by the Linux Mint team, [Warpinator](https://www.fossmint.com/warpinator-share-files-across-a-network-in-ubuntu-linux/) works great at sending one or many files across the LAN to other Linux PC's and Android devices. The app is probably in every distros repos and is on Flathub. There is also an unofficial [Warpinator for Android](https://f-droid.org/en/packages/slowscript.warpinator/) on F-Droid for connecting the desktop to the mobile device. In my testing this has worked fantastic and is super reliable.

[Gaming On Linux](https://www.gamingonlinux.com/2022/03/heres-how-to-transfer-files-from-your-pc-to-a-steam-deck/) highlighted Warpinator for moving files from a PC to the Steam Deck (which is also a Linux PC). It is essentially the same for moving files for Android. 

https://youtu.be/sHdQT6kI6Q8

#### Zorin Connect
In addition to sending and receiving files, I like to have a shared clipboard. This makes entering passwords so much easier to simply copy it on my laptop and paste on my phone. Plus, it would be nice to see when the device has a low battery and to ping it in case I left it somewhere else (most likely in the bathroom). This is why I love Zorin Connect.

[Zorin Connect](https://f-droid.org/en/packages/com.zorinos.zorin_connect/) is a fork of the amazing [KDE Connect](https://kdeconnect.kde.org/) project made by the [Zorin OS](https://zorin.com/) team for their distro. There is a KDE Connect Android app, but I have found that the Zorin Connect app is more reliable and sync up faster with both my laptop running Zorin OS and my desktop with Pop_OS. 

To work you will need either KDE Connect or GSConnect installed on your laptop/desktop and the Zorin Connect app on the mobile device. Once installed, pair the devices and then give the additional permissions needed to function. Zorin/KDE Connect can also send and receive files. But, it is really best for small, individual files. For large files, or if you need to send multiple at the same time, use Warpinator.

#### Good ol' ADB
No matter what, you will need `adb` installed on your PC and USB Debugging enabled on the mobile device to install a custom ROM or run the debloater. But, I also like to use it for sideloading apps and is super useful for remote screen sharing. 

Once the Developer Options are enabled and USB Debugging is turned on, I always tick "ADB over network" so I don't have to plug in the Android device to get an adb bridge. Once enabled, open up a terminal on your PC and connect to it with:

```
$ adb connect <device ip>:<port #>
```
#### scrcpy
Even better, once "adb over network" is enabled and connected, I like to use [scrcpy](https://github.com/Genymobile/scrcpy) to remotely view the screen on my PC. This means I can use my PC's keyboard and mouse to navigate the device, which makes setting up complicated apps much easier. It is also another way to share the clipboard for easier logins. You don't have to do this over the network, it will also work when connected to the PC via USB and will be much more responsive. 

When connecting over the network, there can be a delay or can be laggy. By default, scrcpy also mirrors the display and leaves it on while connected. To have a more responsive connection and leave the display off to save battery, I pass these flags when connecting:

```
$ scrcpy -b 2M -m 1024 -S
```

The `-b` flag will limit the bitrate, `-m` will reduce the resolution, and `-S` will leave the screen off.

https://www.youtube.com/watch?v=YztJ0H_lK8E

## Frontend & Setting Up RetroArch
These are lumped together because the frontend I chose will also assist with setting up RetroArch and other emulators. There are many awesome frontends to convert any Android device and some of the best are covered by [Retro Game Corps](https://retrogamecorps.com/) in their great guide for [Android emulation](https://retrogamecorps.com/2022/03/13/android-emulation-starter-guide/#Frontends). 

I ended up going with [Pegasus Frontend](https://pegasus-frontend.org/#downloads) because it is free, is highly connected to the [RetroPie community](https://retropie.org.uk/forum/topic/9598/announcing-pegasus-frontend), and there is a 3rd. party script that will set it up plus several other emulators including RetroArch. To be honest, my interest was piqued when the setup for it involved running commands in [Termux](https://termux.com/).

Here is the order I would set things up.

#### Transfer the ROMs
Pegasus by default expects all the ROM files to be in the `rom` folder on the device, with subfolders for all the platforms. This will be either in the internal storage or on the sdcard, depending on the device and your selection during the setup process. The device I'm using does not have an sdcard, so I created the `rom` folder right in the root directory and loaded up all my ROMs. 

You will also want to create a folder outside of the `roms` folder for any BIOS needed. I created a `Games` directory and then a subfolder for `bios`.

The folder structure is roughly like this:
```
/storage
├─ Documents
├─ Download
└─ **Games**
   └─ bios
├─ Movies
├─ Music
└─ **roms**
   └─ atari2600
   └─ nes
   └─ psx
```

Transfer the files by connecting to the PC via USB or send with Warpinator.

#### Install Pegasus and RetroArch
Although the script will install these, I ran into issues and it was just easier to manually install both Pegasus and RetroArch before starting the script. 

RetroArch is available on both F-Droid and Google Play, but to have the latest and greatest version it is best to download and install the [apk from their website](https://www.retroarch.com/?page=platforms). This means I will have to manually update it occasionally, so in the end it might be best to just add the [libRetro repo](https://fdroid.libretro.com/website/) to F-Droid and let the updates be managed there, even if it is slightly slower to receive the newest version.

[Pegasus for Android](https://pegasus-frontend.org/#downloads) is not in any repos or stores, so it can only be installed via manually downloaded apk. 

You can either download on the mobile device and install, or sideload with `adb` which is what I did. 

After both are installed, open RetroArch and let it run its initial setup. Do not change any settings or anything, just let it run the welcome setup and then quit the app.

#### Run the setup script
In order for the scrip to work the best, install the Termux app and give it "install unknown apps" permission, along with the default browser. Once installs and and permissions are ready, follow the instructions here:

[Pegasus Installer](https://www.pegasus-installer.com/)

The installer will prompt the installation of various other emulators, most from the Play Store and a couple as standalone apk's. It is okay if you don't install all of them. Just exit out of the Play Store and go back to Termux and continue the installation. 

#### RetroArch Setup
Once the script is complete and all the games have been scraped, I spent some time configuring RetroArch for the best playability for my mobile device. Again, Retro Game Corps has a great guide for configuring RetroArch, including the basics on how the app works with config files. 

[RetroArch Starter Guide – Retro Game Corps](https://retrogamecorps.com/2022/02/28/retroarch-starter-guide/)

#### Emulators thoughts
There are a lot of emulators out there and lots of people have thoughts about them. This is not the place to break down a list of emulators, where to get them, and the best BIOS files. There are lots and lots of other guides and do a great job breaking them down. 

Here is an unbelievable wiki on Reddit of emulators, gamepads, shader packs, and more. 

[wiki /r/EmulationOnAndroid](https://teddit.net/r/EmulationOnAndroid/wiki/index)

I do wish I can find an app that will play games from the Internet Archive Arcade like the [Internet Archive Game Launcher](https://forum.kodi.tv/showthread.php?tid=332966) for Kodi. 

## Internet Archive Arcade
While researching this project I briefly looked at using [Kodi](https://kodi.tv/) which supports playing games through [libretro](https://www.libretro.com/) integration. Though I decided against using it as my primary frontent for the device, I did end up installing and configuring it for a couple usecases.

I was unaware of a version of Kodi called [Retroplayer](https://forum.kodi.tv/showthread.php?tid=340684) which is a fork of the main Kodi branch with libretro natively hooked in along with easier ways to install emulators and retro gaming addons. I ended up having issues using it for my usecase, but it did lead me to discover an [Internet Archive Games Library addon](https://github.com/zach-morris/plugin.program.iagl/wiki/1.--Setup) that enables the ability to play games from the [Internet Archive Arcade](https://archive.org/details/internetarcade?tab=about) which is just fucking rad. 

Getting the IAGL addon installed is simple. The link above is a thorough setup guide for the addon and even walks through how to set it up using the sdcard as the primary storage device. My Nexus 5x doesn't have an sdcard slot, so I didn't go through that section.

During the install process, the setup wizard will prompt you if you want to install the emulators or if you want to use an existing install. Having gone both routes, I highly encourage you to skip installing the emulators and use an external source, which in 99% of the cases is RetroArch. If you choose to install the emulators through the setup wizard, it will take nearly an hour and will install literally every emulator on the face of the earth. It is much easier to manage the emulators in RetroArch, will use your custom config, and will be done much faster. 

When you select external launching Kodi will prompt you to select your RetroArch config file. If it is in the standard Android location, just select it from the list. If you have customized the folder location, just navigate through the directories and select the right config file. 

https://www.youtube.com/watch?v=522NoPf6dCE

## A Little Entertainment
Since I had to install Kodi for the IAGL addon, I figured I might as well finish setting up Kodi. Over 90% of my TV and movie watching is done from my [Jellyfin](https://jellyfin.org/) server on my LAN. Jellyfin has awesome integration with Kodi and provides an addon repository not only to setup a dedicated Jellyfin app, but also to integrate my Jellyfin library into Kodi as if they were native files. Rather than opening the Jellyfin app, the TV shows and movies will be in the TV and Movies tabs in Kodi. 

Here are the instructions to add the Jellyfin repo and then to install the Jellyfin addon:

[Jellyfin ♥ Kodi addon repository](https://jellyfin.org/docs/general/clients/kodi.html)

Now I have access to watch all my stuff and have another reason for installing Kodi on this gaming console. Kodi is fully functional with a gamepad, so playing games or navigating media with the Kishi is simple. 

Speaking of gamepad, I also decided to install a YouTube app. Again, this isn't necessary for a gaming console. But, YouTube and gaming go together like sun butter and jelly. I didn't install the standard YouTube app when I setup GApps on LineageOS mostly because the native YouTube app is terrible. Additionally, the standard YT app doesn't work well with a gamepad. 

Instead I went with [SmartTubeNext](https://github.com/yuliskov/SmartTubeNext/) which is a YouTube client for Android TV boxes. SmartTubeNext blocks ads, has integrated [SponsorBlock](https://sponsor.ajay.app/), and is designed as a TV interface which works perfectly with a gamepad. To install, download the latest release from Github and then use adb:

```
$ adb install <smarttube_release>.apk
```

The app has an update feature, so you don't need to worry about occasionally sideloading an update. 

## Game Streaming
Because this is an Android phone, game streaming apps from the big players work fantastically. Plus the phone has dual band wifi, so the speeds needed for game streaming on wifi is not a problem. 

#### Xbox game streaming
I own an Xbox and am an Xbox Game Pass Ultimate subscriber, so I setup both the apps on the Nexus 5x. Using the standard [Xbox app](https://play.google.com/store/apps/details?id=com.microsoft.xboxone.smartglass&gl=US) I can use [in-home streaming](https://www.xbox.com/en-US/consoles/remote-play) from my Xbox to this mobile game console and it looks great. [XCloud game streaming](https://www.xbox.com/en-US/xbox-game-pass/cloud-gaming) using the [Xbox Game Pass](https://play.google.com/store/apps/details?id=com.gamepass&gl=US) app also works great and both apps are optimized for the gamepad. 

#### Steam in-home streaming
I also have a ridiculously large Steam library and play games on my Pop_OS Linux PC. Using the [Steam Link](https://store.steampowered.com/app/353380/Steam_Link/) app on Android means I can stream games from my powerful PC to my hands while sitting on the couch. This is how I played and finished [Mutant Year Zero](https://store.steampowered.com/app/760060/Mutant_Year_Zero_Road_to_Eden/) and am now playing [Fight'n Rage](https://store.steampowered.com/app/674520/FightN_Rage/).

Needless to say, game streaming on Android is getting fairly mature and needs little setup to work great. 

## Backup
This has been a fair amount of setup and I really, really don't want to have to do it again for some silly reason like a failed update or a bored Sunday tweaking attempts. Also the weekend try-hard SysAdmin in me cringes at the thought of no backups.

Since I have fully narrowed down the entire device, rather than taking snapshots of specific folders I will take a full app backup of the device. Using adb we can make a full device backup. I really only need this after the initial setup and then any major changes rolling forward. 

```
$ adb backup -apk -shared -all -f backup_<date>.ab
```

On the mobile device, you will be prompted to accept the backup request. Just tap on the “Backup my data” button. You can enter a password if you want the backup to be encrypted.

When you want to restore, place the backup file in the same folder the adb files and use the below command. Just like before, you will see a prompt in your smartphone to accept the restore request. Tap on the “Restore my data” button.

```
$ adb restore backup_<date>.ab
```

Here is a decent guide to using adb for backing up individual apps or whole devices.

[Backup android app, data included, no root needed, with adb · GitHub](https://gist.github.com/AnatomicJC/e773dd55ae60ab0b2d6dd2351eb977c1)

After this is done I will only backup my saves folder, which I have in a custom location outside the RetroArch app directory and can shoot to my PC using Warpinator or Zorin Connect. 

For what it is worth, backing up a single folder can be done with adb using the `pull` command. So for my RetroArch folder:

```
$ adb pull /sdcard/Documents/Retro_Saves/
```

The folder will be pulled into whatever directory I am in on my PC.

## Conclusion
I can't put this thing down. I am head-over-heels in love with this gaming setup. Every moment I have 10-20 minutes of free time I have this console in my hands and I'm playing something, either a retro game or streaming from my Xbox or Steam library. I use it so much I have a hard time keeping it charged. 

I can see the allure now of the Switch and the Steam Deck. A handheld device for gaming is just so much fun. I can never get myself to get a Nintendo product because I don't want to re-buy a lot of games I already own. I'd love a Steam Deck, but I don't have any money to spend on a gaming device, especially since I already have a great Linux gaming PC and an Xbox. Going this route was natural for me, both in saving money and recycling some tech I have around the house. 

This Android setup truly is the best of both worlds. I can play some of my all time favorite classic games from my childhood and play the latest and greatest titles via streaming. I highly recommend that if you have any of these parts or can get them cheaply, go for it. Especially if you are considering buying one of these retro gaming consoles. Build one yourself and see how you like it first. If you love it, buy a dedicated machine. You don't even need an old Android to do it, you can build it with your main device and just leave all your standard phone apps.