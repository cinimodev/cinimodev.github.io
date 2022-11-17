---
layout: post
title:  "Archiving Podcasts & Serving Local RSS Feeds"
date:   2022-11-17 08:07:08 -0800
category: blog
tags: [podcasts, rss, self-hosted, linux-server, docker, blog, how-to]
---
# Archiving Podcasts & Serving Them in Local RSS Feeds | Internet-in-a-Box Project
*Nov.. 17, 2022* 

This project is to setup the automatic downloading of podcasts onto my `internet-in-a-box` homelab box and then serve each podcast in their own custom, LAN-only RSS feed.

#### Motivation
The reason why I want this setup is to have a fully functioning `internet-in-a-box` server for if I ever go offgrid or lose access to the public internet. My `internet-in-a-box` project is to build a server that will replicate many services I use to make it *feel like* I am still connected. There are many reasons why I may lose connection to the public internet, but in no way am I truly a doomsday prepper. Although there is some motiviation there just in case SHTF, most of my prepping is for a personal financial catastrophe. Like, if I lose my job and we have to make serious cuts to our budget. 

I love listening to podcasts and would want to keep that doing so even without the public internet. My goal is to automatically download podcasts to my NAS and then make it possible to serve those podcasts over my LAN into a podcatcher on my phone, just like it would normally with public internet access as if I was downloading straight from Apple Podcasts or Spotify. 

An additional benefit is there are several podcasts I would like to archive just in case they ever disappear. There are some shows I truly enjoy and I want to make sure I always have access to them. Some scenarios are if the back catalog is ever locked due to the show being purchased by a large podcast network (like Audible). Another would be the podcast simply ceasing production and the feeds removed. 

A tertiary benefit is some privacy. This setup could be used to obfuscate my personal info from platforms collecting data for ads. By having all the downloads go to one place, with no other user info other than IP address and some basic metadata, my listening habits will be private. At the moment I am not too concerned about this. But, it is something that is there if I ever want to take advantage of it.

#### LAN note
I am only using this on my LAN and using port numbers in my URL's doesn't bother me. However, if you want to setup Let's Encrypt certs with a reverse proxy that is totally fine and completely up to you. For me, it is not worth the extra effort for a total of 2 users. Theoretically, once this is setup, I won't interact with the services directly. The episodes will just appear in my podcatcher.

## Podgrab
First step is to have a system that will automatically download podcasts in the background. [Podgrab](https://github.com/akhilrex/podgrab) has a lot going for it and was an easy selection for this purpose. 

Now, Podgrab is both a podcast downloader and a server, which is a nice combination if I wanted to interact with podcasts in one interface.  The web interface allows adding podcasts, browsing iTunes directory for new shows, plus allows playback and downloading from your local server. This is nice if I am not using a podcatcher on another device. 

It also offers a single RSS feed for all shows in the library, which you could use in any standard podcatcher. For example, I loaded the RSS feed into AntennaPod and it gave me all the episodes from every show in the library as a single feed. I guess this is nice if I listen to every show in my list. However, this is not my usecase for this build. I will be using AudioBookshelf to serve the shows in individual feeds and allow the users on that service to choose what they want to subscribe to. 

The main reason I went with Podgrab was for the podcast archiving features. These are the features I am most interested in:

-   Download/Archive complete podcast
-   Auto-download new episodes
-   Tag/Label podcasts into groups
-   Add using direct RSS feed URL / OMPL import / Search
-   Existing episode file detection - Prevent re-downloading files if already present
-   Easy OPML import/export
-   Customizable episode names
-   Append episode number to the file name
-   Generage NFO files for podcasts

Using the web interface I can add podcasts, set a name and download settings (including how many back episodes to grab), and put podcasts into groups. I also need to append the episode number to the file at the very beginning, which will be important for AudioBookshelf. Everything else it can do is just icing on the cake. 

The final reason why I chose Podgrab is that I can run it as a Docker container. I prefer putting services in containers because I can map the volumes for configuration and assets, migrate it to any new system I create, and then just add it to my bi-monthly backups. Porting a Docker container to a new system is so easy that there is no way I am going back to running services on the base system. 

*Side note:* Reading through the issues on Podgrab's Github it appears there may be some issues with pulling new copies of the container and losing previous configs. It may also be true if the container is stopped. So, make sure you have backups of your config.

#### Docker setup

[Podgrab Installation Setup](https://github.com/akhilrex/podgrab#using-docker)  

Everything needed to get running in one line.  

This is my Docker setup. Your's will be different. Make sure to change the ports, volume mounts, and any other config info you want for your instance. 

```
docker run -d -p 8084:8080 --name=podgrab -e TZ=America/Los_Angeles -v /mnt/storage/podcast_archive:/assets -v /mnt/storage/docker_config/podgrab:/config --restart unless-stopped akhilrex/podgrab
```

The web interface will be available at `http://your-server-ip:8084` or however you have your reverse proxy configured. 

## AudioBookshelf
As mentioned above, what I really want to do is serve the downloaded episodes in their own RSS feeds. This way users can subscribe to the shows they would like to have, rather than the full feed. This is where [AudioBookshelf](https://www.audiobookshelf.org/) comes in. Audiobookshelf is for both podcasts and audiobooks, but I am only using it for podcasts. 

Setup for this is simple and also runs in Docker. All you need to do is point the podcast folder to where Podgrab is downloading the feeds. AudioBookshelf will parse each folder as individual shows and then allow you to generate an RSS feed for each in the web interface at `http://your-server-ip:8085`.

Again, I am not concerned about port numbers. Once the feeds are in the podcatcher, I won't even notice it in the URL. 

#### Docker setup

[AudioBookshelf Install Guide](https://www.audiobookshelf.org/install/)

This is my Docker setup. Your's will be different. Make sure to change the ports, volume mounts, and any other config info you want for your instance. 

```
docker run -d -e AUDIOBOOKSHELF_UID=99 -e AUDIOBOOKSHELF_GID=100 -e TZ=America/Los_Angeles -p 8085:80 -v /mnt/storage/dockerconfig/audiobookshelf/config:/config -v /mnt/storage/docker_config/audiobookshelf/metadata:/metadata -v /mnt/storage/podcast_archive:/podcasts --name audiobookshelf --restart unless-stopped ghcr.io/advplyr/audiobookshelf
```