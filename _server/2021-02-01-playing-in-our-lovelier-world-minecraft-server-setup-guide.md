---
layout: post
title:  "Playing in my our Lovelier World | LAN Minecraft server setup guide"
date:   2021-02-15 08:07:08 -0800
category: blog
tags: [minecraft, self-hosted, linux-server, gaming, blog,how-to]
---
# Stampy's Lovelier World
Having exclusively played the Java version of Minecraft for a decade, I was finally pulled into the Bedrock edition because of a new map from Stampy. In his recent videos he has been exploring his [Lovelier World](https://www.youtube.com/watch?v=kr45-OkOR4Y&t=1s) which my 5-year old has been devouring. Of course, this means I wanted to setup a server so both of us could play in Stampy's Lovelier World together.

For the last 4 months we've been playing Minecraft every night before bed. We play for about a half hour and I've installed a couple custom maps with mods on a Java Edition server running in a Docker container. One of the maps is a version of Stampy's Lovely World, which I would consider to be our "home". When the "Lovelier World" landed I looked at the video description and excitedly discovered the creators have released the map for download!

You can see the launch video and link to the map download here:
* [DannyIsDahBomb - Lovelier World Download Video](https://www.youtube.com/watch?v=exVPnXb0_nQ)
* [Lovelier World MediaFire Dowload Link](https://www.mediafire.com/file/bzw36829ytgkm3v/Lovelier_World.mcworld/file)

The trouble I ran into is this is a Bedrock version of the map and there isn't an official Bedrock version for Linux.

Lucky for everyone, there is a way to do this. Below is the setup and configuration I have on my LAN so my daughter and I can play Stampy's Lovelier World  together and allow for other people in the house to join from the phone, Xbox, or any other device that runs the Bedrock Edition of the game.

#### Setting up the Bedrock Edition client side on Pop_OS

First need to puchase the the Google Play edition of the game. I did this with the family payment option, so technically I only had to buy the game one and everyone in my family group got access to the paid version of the game. Google doesn't exactly make it easy to figure out how to setup a family group. You can see their directions [here](https://families.google.com/families). The key is that you have to set up and purchase the game with the family payment method. Even though you are part of a family, if you don't choose the family payment method no one in your family group will get access to the Google Play version of the game and will have to purchase again.

Next, go to the Linux machine you are going to be running the game on. I use Pop_OS and Ubuntu Mate, so here are the commands I run:
* `sudo dpkg --add-architecture i386`
* `sudo apt-get update`
* `sudo apt install libc6-i386 libx11-6:i386 libegl1-mesa:i386 zlib1g:i386 libstdc++6:i386 libgl1-mesa-dri:i386 libasound2:i386 libpulse0:i386`

Once you have the dependencies setup, just use Lutris to install the game. For the unititiated, Lutris is a great piece of software that handles installing games on Linux. In Lutris there is already a person that has created an install script for getting the Bedrock Edition setup on your device. It will install the AppImage and get everything configured. There are two versions, I installed *Christopher's AppImage Version* which has received more and more recent updates.

Here is the Lutris page about how to setup: [https://lutris.net/games/minecraft-bedrock-edition/](https://lutris.net/games/minecraft-bedrock-edition/)

Make sure to read through the notes and verify you have everything ready. After install, launch the GUI and go through the setup. This will include logging into your Google Account and Xbox/Microsoft account for online play. Last, edit your profile and download the most recent Google Play version of the game.

#### Building the Bedrock server with Docker
Setting up the server was an adventure to say the least. Below are the commands I used to set everything up. Be sure to change the folder locations for your `/data` folder for whatever you want/need your configuration to be. This is a raw copy/paste from my commands so if you do the same, it will name and use folders you probably don't have on your system.

This is all using Docker, so make sure you have that set up on your machine too. Here is the official [Docker Hub for the Bedrock Server](https://hub.docker.com/r/itzg/minecraft-bedrock-server).

`sudo docker run -d -it --name=minecraft_stampy_lovelier_op -e TZ=America/Los_Angeles -p 19132:19132/udp -e GAMEMODE=creative -e EULA=TRUE -v /san_junipero/local_server/minecraft_stampy_lovelier:/data --restart unless-stopped itzg/minecraft-bedrock-server`

Need to start the server, then after first launch let the game build the files. Then stop the container and delete the auto-generated world in the `worlds` folder in your `/data` directory. Now is the time to move over the world downloaded at the top of this how-to.  Extract the files, rename the folder and copy/paste into the `worlds` folder.

Next, edit the `server.properties` file. In this file, need to change the name of the world to the name of the Lovelier World folder you just dropped into the `worlds` folder.

Then, relaunch the container. You should now be able to access the server from your client. If you can't, make sure you have your firewall configured to allow data through `19132/udp` port.

One of the things I needed to adjust was the ability to build/destroy blocks. Even though it is a very beautiful world, my daughter and I want to add custom items and generally have the ability to destroy everything (including blowing things up, which we do a lot). Running this as a server means we can absolutely destroy this map and with a few short commands get a new map built.

To do this I need to change the permission level for players to "operator". This can be done by adjusting the `server.properties` file or pass the setting while creating the server. But, neither of them worked for me. Instead I just passed the command to the server after attaching to the container.

`docker attach minecraft_stampy_lovelier_op`

Then enter in the command to change the user to an "operator":

`op <gamertag>`

Here are the notes about the Bedrock server Docker container: [https://hub.docker.com/r/itzg/minecraft-bedrock-server](https://hub.docker.com/r/itzg/minecraft-bedrock-server)

For other server commands through `docker attach` [https://minecraftbedrock.fandom.com/wiki/Commands/List_of_Commands](https://minecraftbedrock.fandom.com/wiki/Commands/List_of_Commands)

Using the server commands I adjusted to not be always daytime and to enable cheats. Having nighttime in the game makes it for clean break points so we can stop for the night in real life too.

`alwaysday false`

As I mentioned above, this is only for our LAN. If you want to setup this server for people on the open internet to join, do not use this guide. There are several other considerations you need to take, including server security, whitelists, load/capacity, domains, and moderation. My goal for this was always just for a safe place for my daughter and I to play. We also record all our games and have fun watching later, sharing clips, and general fun stuff. I have a separate guide for that which you can read here.

* * *

### Contact me

Would love to hear from you on this topic!  

**Email**: obscurednarration@gmail.com  
**Twitter**: [@domcorriveau](https://twitter.com/domcorriveau)  

### Digital marketing professional

Into digital marketing? Get a newsletter all about the best stuff in digital marketing over the last week plus deep-dives into this industry.  

[Newsletter](https://corrteksolutions.com/marketing-mixer-newsletter/)  
