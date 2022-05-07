---
layout: post
title:  "Configuring wireless adb and Android screen mirroring with scrcpy on Pop_OS"
date:   2021-10-23 08:07:08 -0800
category: blog
tags: [android, scrcpy, adb, pop_os, networking]
---
# Configuring wireless adb and Android screen mirroring with scrcpy on Pop_OS
*Oct. 23, 2021*  

This is a way to connect to an Android device wirelessly through `adb`. Doing this will enable using `scrcpy` over the network, which is important because my phone cannot currently use it's USB-C port. 

The downside to this setup is that you need to be able to connect to the device over USB at least once. 

### Configure adb
First, need to setup connecting to the device via `adb`.

1. Turn on Developer Options on the mobile device
Go to Settings -> About and tap on Build Number until Developer Options are enabled. Then, go back and into System -> Advanced -> Developer options and enable both USB Debugging and Wireless Debugging

2. Install `adb` on desktop
Super easy on Ubuntu-based distros. Just `sudo apt install adb`. Start `adb` with `adb start-server`. 

3. Plug in device & configure connection
Once plugged into the computer, tap to accept the connection on the mobile including to always accept connections from this device. 

Check to see if the device is connected with `adb devices`. 

Next we need to change the port for connections over the network. Run `adb tcpip 5555`. For whatever reason every guide on the internet uses the same `5555` as the port for their configuration. I don't know why, but this is the only port I was able to use to get it to work. 

**Do this for each device you want to connect over the network.**

4. Connect over network
Disconnect the mobile device from USB and drop into a terminal on your PC. Run `adb connect <device ip>:5555`. Double check connection with `adb devices`.

When not using the device, be sure to disconnect. 

```
$ adb disconnect <device ip>:5555
```

### Screen mirroring
`scrcpy ` is a command line tool that will mirror the Android screen over USB and network connections via `adb`. 

Installing is easy on Ubuntu-based systems:

```
$ sudo apt install scrcpy
```

Once a device is connected via `adb`, can just run `scrcpy` and it will show the mobile device in a window on the PC. 

Personally I prefer to pass a couple of additional commands for a better experience. First I don't want the window border, just the floating screen. Second, I want to keep the device from going to sleep while it is being mirrored. Last, I don't want the mobile device screen to be on while mirroring to save battery. 

To accomplish this, pass these commands:

```
$ scrcpy -Sw --window-borderless
```

Full list of options here: [scrcpy](https://github.com/Genymobile/scrcpy)

### Running scrcpy
Rather than first connecting to a device with `adb` then entering the `scrcpy` command, I just create a bash script along with a fish shell alias. 

Create the script:

```
$ touch ~/Apps/scrcpy-tab.sh
```

My text editor of choice is `micro`, which is in apt repos. Just install with `sudo apt install micro`. I prefer this because it has more standard keyboard shortcuts and syntax highlighting. I'm not a developer or a SysAdmin for my job, I spend most of my time using standard text editors for copywriting. Having to learn esoteric commands for emacs, VIM, and others is a huge waste of my time. Just give me something that uses commands I actually use on a regular basis. 

```
$ micro ~/Apps/scrcpy-tab.sh
```

Then enter the steps to get the device connected and start `scrcpy`. I have static IP addresses for all my devices, so this should always work. However, I'm not sure if the port will remain long-term. This means I might need to connect the mobile over USB and run `adb tcpip` again.

```
!# bin/bash
adb connect <device ip>:5555 &&
scrcpy -Sw --window-borderless
```
Save and exit, then mark the file as executable:

```
$ chmod +x ~/Apps/scrcpy-tab.sh
```

Now I will create an alias so I can run this script. I use `fish shell` as my primary shell. So, set it up like this:

```
$ alias scrcpy-tab='sh /home/dominic/Apps/scrcpy-tab.sh
```

Then save it:

```
$ funcsave scrcpy-tab
```

To launch, just run the alias:

```
$ scrcpy-tab
```

When done, be sure to disconnect the device from the `adb` server. Otherwise there will be a conflict with `scrcpy` when there are multiple devices connected via `adb`. This only matters if you plan to connect to more than one device using `adb` over the network. 

```
$ adb disconnect <device ip>:5555
```