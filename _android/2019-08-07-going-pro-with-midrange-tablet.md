---
layout: post
title:  "Going Pro with a Mid-Range Android Tablet"
date:   2019-08-07 08:07:08 -0800
category: blog
tags: [android, android_tablet, lapdock,]
---

# Going Pro with a Mid-Range Android Tablet
*August 7, 2019*  

Being a tech enthusiast on a budget can be challenging. Not because there’s so many great things in the world and too little money to enjoy them, but the fear of wasting money on the wrong thing. This is really where other creators, YouTube and the like, can help cut through the noise and give an honest review of products. However that statement is full of crap. The biggest issue in this sphere (other than fake reviews that are actually ads, whole different conversation) is whether or not something is “pro”.

## Update: Nov. 12, 2022
I originally wrote this over three years ago and in that time I have had an on/off relationship with this tablet. It is not because it isn't good, in fact it continues to be a fantastic device that is still getting updates and performs exceptionally even after all these years. 

The reason why I have strayed from using it as a daily driver laptop is mostly Samsung DeX. I love DeX and, for being based on Android, performs admirally. The problem has always been it is not an actual desktop OS, rather a mobile OS pretending to be a desktop. Here are some examples of what I mean:

- Some apps refuse to open in a windowed mode. For example, I can't open my password manager or 2FA app in DeX, only when in tablet mode.
- No right click. I frequently attempt to right click and copy links, but I still have to long tap a link to get the menu. A lot of apps require pull to refresh or to drag, which is awkward with a mouse. 
- Apps are still... Mobile apps. I prefer to use Firefox and on my mobile I use Fennec. Not all of the addons I like are available on mobile Firefox/Fennec. They don't use tabs the same way. I can't use Firefox containers, which is arguably the best reason to use Firefox/Fennec.

Eventually I got tired of using mobile apps to get real work done. So, I switched to a laptop and stopped carrying the tablet as my mobile PC. But, I was always felt the pull back to the tablet because of the potential. When I need to pop into a service/app and make a quick update, doing so from Android with a keyboard and mouse is fast and convienient. The tablet is also a multimedia powerhouse and the screen real estate means I can multitask one-handed while lounging on the couch.

#### Termux & Proot Distros
About six months ago I learned there are many ways to run a full, virtualized Linux desktop in a proot environment with Termux. This was fun and I learned a lot about Termux in the process. Yet, none of them were really that good. It is a fun experiment and pretty rad you can do this inside of Android. But it is not what I am looking for. The desktops crashed - a lot. There was no way I could count on them for reliability or consistency. It truly is a toy.

For those interested, here are some resources:

- [AndroNix](https://andronix-app.gitbook.io/andronix-app/](https://andronix-app.gitbook.io/andronix-app/)
- [UDroid](https://github.com/RandomCoderOrg/ubuntu-on-android)
- [UserLAnd](https://github.com/CypherpunkArmory/UserLAnd/wiki/What-is-UserLAnd%3F)

#### X11 / Xwayland GUI on Termux
After much, **MUCH** testing, all of the Linux environments you can install are incredibly  unstable. I got frequent crashes after fumbling around trying to get things to work for 3 days. So far the best setup I have found is to install XFCE ontop of Termux, and then view with [Xserver XSDL](https://play.google.com/store/apps/details?id=x.org.server&hl=en_US&gl=US).  The XFCE experience is decent and it is stable. There are more GUI packages for Termux than I orignally thought, so it turns out running a full Linux desktop is unnecessary. 

Setup source: [https://wiki.termux.com/wiki/Graphical_Environment](https://wiki.termux.com/wiki/Graphical_Environment)

First, install the X11 repo:

`$ pkg install x11-repo`

Then install Xwayland:

`$ pkg install xwayland`

Next, install VNC server: 

`$ pkg install tigervnc`

After installation, execute this:

`$ vncserver -localhost` 

At first time, you will be prompted for setting up passwords.

Now install the desktop:

`$ pkg install xfce4`

Finally, to make programs do graphical output to the display 'localhost:1', set environment variable like shown here (yes, without specifying 'localhost'):

`$ export DISPLAY=":1" `

You may even put this variable to your bashrc or profile so you don't have to always set it manually unless display address will be changed.

I tested a couple different ways and landed on XServer XSDL as the client viewer. It looks the best with the lowest latency. 

First things first, before starting the server you need to open XServer XSDL and have it waiting for input. 

Now back to Termux and start the server:

```
$ vncserver -localhost
$ export DISPLAY=localhost:1
$ xfce-session &
```

#### Streaming desktops
The above setup works perfectly while I am out of the house and need to get some real work done. It will give me a full desktop feel along with a real browser. Yet, when I am at home I have many other options that work even better. 

First, I setup a [Sunshine](https://github.com/LizardByte/Sunshine) host, which is a low latency game streaming server for Moonlight using Nvidia's GameStream tech. Instead of using this to stream games, I am simply streaming my desktop to the tablet. Sunshine setup in minutes and is super stable. You could accomplish the same with [Parsec](https://parsec.app/) to stream from a Windows PC with similar results. However I wouldn't know because I don't have any Windows PC's to try it <wink>.

I don't use this often, unless there is something on my desktop I absolutely have to have access without going into my office. Although this is the most consistent and stable experience, I don't like to have my desktop running since it uses so much power. 

Instead, most of the time I stream a desktop from my homelab server using [Webtop](https://github.com/linuxserver/docker-webtop). Using Docker, this will give a full desktop experience and then stream the desktop to any browser. It is literally how I am writing this update. I am streaming an XFCE desktop from the server in a browser and set to fullscreen. I am writing this in Firefox using VSCode in the brower. 

I prefer this setup because I can access this destkop from anywhere. So, if I start a project and decide to call it a day, I can access this exact setup anytime on my tablet or from any other PC in the house. I can also access it by my Wireguard VPN into my home. I am rarely on a jobsite with good enough mobile data to stream a desktop. But, anytime I am at a place with good, safe wifi, I can get this same desktop the exact way it was when I last used it. 

## Going for a tablet

I recently purchased a Samsung S5e tablet. I upgraded slightly to get the 128 GB version, which happens to come with 6 GB of RAM. My goal in purchasing a tablet, the first brand new tech device I’ve bought in several years, was to stop carrying my Dell Lattitude E5440 while on the road. Secondary goal was to have something for getting work done while home either on the couch or at the kitchen table. Nothing against my E5440, its a true workhorse. It is gigantic though.

For some time I’ve been looking around at what the best deal would be for a ultra-portable that accomplishes a few things: Super small and light with great battery life, with at least a 10” screen. App support for a normal work day, including Google Drive, Gmail, Slack, Jitsi, Todoist and of course a browser. Fun while traveling with games, podcasts, YouTube. But small enough I can actually fit it on an airplane tray (unlike my E5440).

I searched for many months while squirreling away my money. No matter what the spend had to be under my $500 budget. I checked Chromebooks, ultra-portables, slimbooks and even glanced at a few old netbooks on eBay. In the end what I came to was this Samsung tablet (which is where I’m writing right now).

What was frustrating for me through the process was how many people said the Tab S5e was good enough to play, but not good enough for a road warrior or someone trying to get work done. Again and again and again I came across blogs and videos that demoted this tablet to a simple toy, rather than a real machine that can get real work done. The only reason I can see why “real work” is because every tech enthusiast always thinking that real work can only get done on something that costs a lot of money. That high cost equals high performance.

So for anyone that is considering using a mid-range tablet for “real work” I’m here to defend you. Yes, I could have waited for the newly announced Tab S6. But its way above my budget. I could have spent an extra $150 and got a S4 which was classified by many as a true work machine. But it didn’t seem worth it to spend the money just for S-Pen support, of which I’m not an artist or someone who takes hand notes. Not including that its still $150 more. I really had to stretch to pick up this S5e, every dollar counts.

Which is another thing mainstream tech people don’t seem to understand. If my budget is $500, that doesn’t mean I can stretch an extra $100 to $200 just because there’s another shinier object. I get it, the specs on the Tab S6 are newer and possibly faster (probably, but yet to be seen). But I have other bills to pay and a whole house full of people that depend on me. Being belligerent with money doesn’t help me sleep at night.

Back to to getting real work done. Here is a recent work day for me, a Digital Marketing Manager, exclusively using the Tab S5e as my primary driver.

#### Morning

-   After my normal morning routine (shower, eat breakfast, make a big cup of iced coffee - I do live in Arizona and it is August) I plop down on the sofa and load Buffer and my RSS app FeedMe side-by-side. I use this time to read the news and load up my social schedule for the day.
-   Before leaving for the office I review my Todoist list, make sure my podcast feeds have synced and are in the right order for my 45 min. drive to work.
-   On the drive I connect the tablet via bluetooth to my car to enjoy the latest episode of LinuxGameCast Weekly.

#### Office

-   Arriving I dock my tablet in a cheap UGreen USB-C dock and switch to DeX mode so I can have a more traditional desktop layout. I have a wired keyboard/mouse plus a 22” 1080 monitor. More coffee.
-   I post to my teams #daily Slack channel what I’m up to for the day, respond to a few emails, add to my calendar and see who put themselves on it via my Calendly link.
-   My morning is all meetings. Using the tablet plus a bluetooth keyboard I go from room to room taking notes, responding to more Slack and of course, more emails.
-   Before lunch I dock the tablet again and write a quick blog post in Google Docs and create a banner image with Canva.
-   During lunch I undock and read more of my RSS feed in FeedMe, chat with my wife in Telegram and have some more Twitter time.
-   After lunch I dock, review some proofs from our content team and update various projects in our project management suite (Wrike if you’re wondering).
-   More emails, more Slack, write up some team documentation and work on a spreadsheet of email performance in Google Sheets.
-   Video chat via Jitsi with a remote employee at the end of the day to review project status.
-   Head to the gym and fire up YouTube while running on the treadmill. I need all the motivation I can get.
-   Head home listening to Red War, the most recent Mitch Rapp thriller using Overdrive synced bluetooth.

#### Home

-   After dinner I write this blog post in Docs and add it as a draft to my WordPress site.
-   Kids go to bed and I find a comfortable spot on the living room floor to lay down, put on an episode of Futurama on Hulu with Imgur running side-by-side (Usersub rising) to close out the night.

## Conclusion

Never once throughout the day did I run into an issue. At times it may have been nice to switch back to my dual screen desktop, but I never felt like it was necessary. I realize I don’t do visual, audio or video production. But these tasks work best with specialized PC’s. For an average day in the office I say this tablet can accomplish real work.

The competition is in the “pro” name, which is where I started and the real problem with tech reviewers. Either they’re in video production (hence making content for YouTube) or a developer waiting to shit on anything presented with (they always think they’re the smartest people in the room), which are not use cases for a mobile workstation.

The real moral of the story here is what “pro” means to you, not what some jackass on YouTube or an Android blog says. Pro means what you need to get your job done. For me, its docs and notes while running around to meetings and chatting with my team all day. I’m tired of the play versus pro mentality. Don’t let these internet jackasses convince you not to make or accomplish something just because you have “inferior” equipment. The right tool for the job is the one you have in front of you. For me its a Dell E5440 and a Samsung Galaxy Tab S5e.