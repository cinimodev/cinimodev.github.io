---
layout: post
title:  "I'm thoroughly impressed with CloudReady on a nearly 8 year old Dell"
date:   2021-11-01 04:07:08 -0800
category: blog
tags: [linux_desktop, chrome_os, chrome, cloudready, neverware]
---
# I'm thoroughly impressed with CloudReady on a nearly 8 year old Dell
*Nov. 1, 2021*  

Being able to re-purpose old hardware for modern uses is one of the pillars of tech I strongly believe in. I've been repairing PC's for over 10 years, trying to squeeze as much life out of hardware other people felt deserved to be in the trash heap. With this mindset, I recently had a chance to install [CloudReady](https://www.neverware.com/freedownload#intro-text) onto an old laptop for a coworker and I have to say: I am thoroughly impressed. 

### Choosing from my laptop arsenal
When refurbishing laptops or desktops for my own house, Linux is the primary option. Over the last 6 months I've gotten my hands on some various enterprise laptops, including:  
* [2011 Dell Lattitude E6320 ](https://www.laptopmag.com/reviews/laptops/dell-latitude-e6320) (my current carry laptop)
* [2016 Dell Lattitude E5270](https://www.laptopmag.com/reviews/laptops/dell-latitude-12)
* [2012 Dell Precision M4700](https://www.notebookcheck.net/Review-Dell-Precision-M4700-Mobile-Workstation.81505.0.html) 
* [2014 Dell Lattitude E5440](https://www.notebookcheck.net/Review-Dell-Latitude-E5440-4668-Notebook.116181.0.html)


A few days ago a coworker reached out to me and asked if I had any spare laptops, which I might have a few laying around I guess. In her home she has a freshman college student and one in elementary school; both of them having laptop issues. After explaining what each of them use for school, the laptops from my arsenal I chose were the E5270 for the college student and the E5440 for the younger. 

A lot of businesses just throw out old enterprise laptops and computers. What I do is collect them, refurbish, then give away to anyone who needs a working computer. There are a lot of people who pay top dollar for the latest and greatest. But, there are an order of magnitude more people who just need a working PC and don't have the means to acquire one. Buying a used laptop comes is fraught with peril for this group as they don't have the technical capabilities to repair or replace hardware, or install a Linux desktop. They just need something that works. I get them for free so I give them away for free. 

The reason why I chose the E5440 for the elementary school student was because the portability was less of a factor. They will be working from a desk most of the time, not from the couch or a cafe. In addition, the newer hardware doesn't matter much when just doing school work in Chrome, with maybe up to 3 tabs open at the same time. For the most part, just one browser tab and no need to install anything else. 

For the OS, this situation is the exact reason Chrome OS is so popular. To be honest, I kinda love Chrome OS myself. A very targeted user experienced with a focused desktop. Don't need to do a lot, but need to do one thing really, really well. This is exactly what Chrome OS does, it runs Chrome really, really well. 

### The setup
At the end of last year [Neverware](https://cloudreadykb.neverware.com/s/article/Neverware-is-now-part-of-Google-FAQ) was acquired by Google. Neverware makes [CloudReady](https://www.neverware.com/freedownload#intro-text), which transforms almost anything into a Chrome OS laptop. You install it the same way you would a Linux distro: Download the image, write to a USB, and pop it into any PC. In addition to the Home edition, they also have enterprise options that will even connect to the Google Admin console for centralized management. This is brilliant for schools or organizations that already have loads of fully functional older devices and don't have the budget to purchase all new hardware. CloudReady can covert your entire fleet to Chromebooks, keeping costs lower and reducing the amount of e-waste.

With this in mind, it was a slam dunk to install CloudReady on this E5440. The laptop has 8 GB of DDR3 RAM along with a [Haswell Core i5-4300u processor](https://ark.intel.com/content/www/us/en/ark/products/76308/intel-core-i54300u-processor-3m-cache-up-to-2-90-ghz.html). It is nowhere near latest and greatest, but for a Chromebook, it is more than enough. The E5440 also has support for a mSATA HDD, which I happened to have lying around, so this laptop has some decent speed. After a cleaning, it looks and runs essentially brand new. 

Installing CloudReady was incredibly simple. Downloading from Neverware as a zip, all I needed to do was extract the `.bin` image and write to a USB stick using `dd`. The image was surprisingly large, clocking in at just over 6 GB, so it took a while for `dd` to do its thing. As always, be sure you have the right disk before running `dd`, you will nuke your entire system if you get it wrong. Check and double check. Don't say I didn't warn you.
  
```
$ sudo dd if=/path/to/bin of=/dev/sd(X) bs=4M && sync
```

Before booting on the laptop, you need to make sure UEFI boot is enabled in the BIOS. I still had legacy boot enabled, which when left on will give an "invalid partition" warning. To get around that, just leave UEFI as the only boot option. 

CloudReady will run straight from the USB stick and on first boot jumps straight into configuring networking and your Google account. Hidden away at the bottom of the screen is the "install" button. But while running from the USB stick, it was fast and snappy. I could see running CloudReady exclusively from a USB as a live desktop for situations when you need to use a Google environment, but don't want it to stick around forever on the HDD. 

After installing it all just worked. I logged into my Google account and everything functioned exactly as a Chrome OS laptop. I was even able to run Powerwash and scrub my account from it before handing off to my coworker. The only complaint I have is a General Chrome OS issue. Requiring your Google password to unlock the desktop has to be the dumbest decision in the whole ecosystem. All of my Google passwords are 40 characters plus. Having to enter that every time the laptop reboots or goes to sleep is infuriating. I eventually used a different Google account for testing and changed its password to something easier to type. 

In the end, it felt like I had purchased a new Chromebook and I was thrilled at the results. My coworker is happy, which is the most important part. However, I'm left impressed with CloudReady and I have been thinking about other miscellaneous projects where I could use a Chromebook. 

My experience has also lead me to recommend to more people with kids using laptops for school, whether in-person or fully remote. There are so many used devices in the world that are still high quality computers, just without a supported operating system. Converting them to a CloudReady Chromebook reduces e-waste and creates a high quality experience for the user. I know there are many households that have an old Windows 7 computer that just needs a new battery and a supported OS to be useful again. Because CloudReady doesn't need any additional configuration, I feel confident telling someone to even install it themselves, as long as they can at least follow directions and have someone a text away for support. 

If you've never given it a whirl, I encourage you to give CloudReady a try.  