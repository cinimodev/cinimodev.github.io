---
layout: post
title:  "Full walkthrough: Installing LineageOS on the Walmart onn. UHD streaming box"
date:   2021-12-04 04:07:08 -0800
category: blog
tags: [android, android_tv, lineageos]
---
# Full walkthrough: Installing LineageOS on the Walmart onn. UHD streaming box
*Dec. 4, 2021*  

My OTT streaming interface of choice is Android TV. But, I have been constantly frustrated with the amount of bloatware that comes on my TV and the official [Google TV](https://store.google.com/us/product/chromecast_google_tv?hl=en-US) dongle/device. Ideally I would have an open-source based OS that isn't built to spy on my living room. At the very least I can remove bloatware and whatever my TV manufacturer is running in the background. This is why I was excited to learn that a group of people have figured out how to get a TV version of LineageOS on [Amlogic G12\*/SM1 family devices](https://forum.xda-developers.com/t/unofficial-lineageos-18-1-for-amlogic-g12-sm1-family-devices.4313743/) which includes the Chromecast with Google TV and the [Walmart onn UHD streaming device](https://www.xda-developers.com/lineageos-18-1-android-tv-11-walmart-onn-4k-dynalink-tv-box/).

I have a Chromecast with Google TV device, but I didn't want to bork it playing around with installing an unofficial LineageOS build. Instead, I found that Walmart was running the onn UHD device on sale for the holidays at only $19. At that price it is worth the cost of admission to see if I can get it running and if I brick the device, it cost under $20 and I didn't ruin the only device I have for streaming.

After a couple of hours of tinkering I was able to not only get the device working with LineageOS, but also sideloaded [STubeNext](https://github.com/yuliskov/SmartTubeNext/) to vastly improve my YouTube experience.

Below is a guide on installing the unofficial LineageOS build on the Walmart onn UHD streaming device, codenamed `dopinder`.

### READ: Before you begin

Some extremely important info before you start this project:

1.  Use at your own risk, you have been warned.
2.  This will **void your warranty** on the device.
3.  There is a chance you could brick your device during this process. It is **not my responsibility if your device becomes unusable**. Be sure to review the links at the bottom of this post to see if anything has changed since I wrote this guide. It is on you to research before starting.
4.  This guide is **only for the Walmart onn UHD streaming device** and not for any of the other devices listed on the XDA post or any other Android TV device. Double and triple check you have the correct device with the codename `dopinder` given by the developers of this LineageOS build.
5.  Installing this build of LineageOS will more-than-likely break using Netflix. This didn't bother me as I only need Jellyfin, Disney+, and Amazon Video. But, that might be a deal breaker for you.

### Let's begin

For my setup I was able to use a micro-USB cable plugged into the device from my computer. Some people use a powered OTG cable so they can have power to the device and connect a keyboard. However, the USB port on my PC provided enough power to run the device and connect to it to run the commands. The guide below lays out the steps to install without having any peripheral connected to the onn device and can all be done from your main PC with `adb` and `fastboot`.

Speaking of which, you will need both of those installed on your PC. Plenty of guides out there for how to setup those on your PC OS of choice. I run Pop\_OS, so it was just a couple `sudo apt install adb` or `sudo apt install fastboot` away.

Last is you'll need to be able to see what is happening from the output of the device. You could run an HDMI cable to a monitor or TV. I prefer to use a cheap HDMI capture care and then use OBS to view the output. This means I am able to view it on my PC while I'm working, without having to run any cables to an additional screen.

I also created a video of the walkthrough below if that helps you get everything installed. This way you can see what happens on the device as the commands are run. You can watch that here:

<iframe width="560" height="315" src="https://www.youtube.com/embed/vLR-b2pZ8Sw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

#### Step one

First, turn on the device and allow it to update. Takes a while and is pretty large for such a basic device. But, it is important to let it get all the way up-to-date. Not shown in the video is an update to the remote control, which I did as well after updating the device.

#### Step two

Android TV will no longer let you skip logging into a Google account when setting up a new device. So on first setup I went ahead and logged into my main account using my phone to speed up the process. No matter what, Android TV will force you to log into a Google account. Just embrace it and move on.

After update is complete and logging in, go to Device Preferences -About and tap on Build Number until you are a developer. Go back and go into developer settings and enable USB Debugging.

On your PC, open up a terminal and verify the device is connected:

    $ adb devices

You should see the device. If not, the device will prompt you to confirm you want your PC to connect. After choosing Yes, run the above command again to make sure you are connected.

Next, reboot into the bootloader:

    $ adb reboot bootloader

#### Step three

Once in the bootloader, first verify you are connected:

    $ fastboot devices

Next, unlock the bootloader with:

    $ fastboot flashing unlock

Then, flash the custom recovery:

    $ fastboot flash recovery lineage[your-version-number]-recovery-dopinder.img

Finally, boot into the recovery:

    $ fastboot boot lineage[your-version-number]-recovery-dopinder.img

#### Step four

Now you should be booted into the custom recovery. I had some trouble getting the custom recovery to stick and had to flash it a couple times until I was finally able to get into it. Sometimes it would hang and never boot into the custom recovery and others it would boot into the stock recovery.

Since I don't have a keyboard attached to the device, we need to use `adb` to launch into sideload mode and flash the ROM. We are going to reboot to sideload the `.zip` for the custom ROM.

As noted above, the first couple times I tried this it kept booting into the stock recovery, not the custom one for installing LineageOS. You will be able to tell you are in the stock recovery because there won't be any LineageOS branding on it. After going back into the bootloader I flashed the custom recovery, then ran the command below to get into sideloading mode and it worked.

    $ adb reboot sideload

Now install LineageOS:

    $ adb sideload lineage[your-version-number]-UNOFFICIAL-dopinder.zip

Once complete, go back to the bootloader:

    $ adb reboot bootloader

Now, do a factory reset to wipe the cache before booting for the first time after installing the custom ROM:

    $ fastboot -w

And finally reboot the device into the new LineageOS install:

    $ fastboot reboot

Done.

### Link summary

Here are all the links to the files, guides, and the XDA forum with the discussion for this device. Be sure to look at all of them and make sure nothing has changed since I wrote this guide.

-   [https://wiki.oddsolutions.us/devices/dopinder/](https://wiki.oddsolutions.us/devices/dopinder/)
-   [https://wiki.oddsolutions.us/devices/dopinder/install](https://wiki.oddsolutions.us/devices/dopinder/install)
-   [https://updater.oddsolutions.us/#/devices/dopinder/builds](https://updater.oddsolutions.us/#/devices/dopinder/builds)
-   [https://forum.xda-developers.com/t/unofficial-lineageos-18-1-for-amlogic-g12-sm1-family-devices.4313743/](https://forum.xda-developers.com/t/unofficial-lineageos-18-1-for-amlogic-g12-sm1-family-devices.4313743/)
-   [https://forum.xda-developers.com/t/unofficial-lineageos-18-1-for-amlogic-g12-sm1-family-devices.4313743/page-3#post-85434073](https://forum.xda-developers.com/t/unofficial-lineageos-18-1-for-amlogic-g12-sm1-family-devices.4313743/page-3#post-85434073)
-   [https://www.xda-developers.com/lineageos-18-1-android-tv-11-walmart-onn-4k-dynalink-tv-box/](https://www.xda-developers.com/lineageos-18-1-android-tv-11-walmart-onn-4k-dynalink-tv-box/)
-   [https://github.com/yuliskov/SmartTubeNext/](https://github.com/yuliskov/SmartTubeNext/)

Flash stock on the device: [https://download.ods.ninja/Android/firmware/](https://download.ods.ninja/Android/firmware/)