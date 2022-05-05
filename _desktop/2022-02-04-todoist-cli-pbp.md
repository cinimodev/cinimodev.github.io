---
layout: post
title:  "Todoist CLI on the Pinebook Pro with Docker"
date:   2022-02-04 04:07:08 -0800
category: blog
tags: [linux_desktop, docker, pinebook_pro]
---

I have switched back to Todoist after an extended period with Nextcloud Tasks. There's nothing wrong with Nextcloud Tasks and worked perfectly over the last year. However, I am now working as a marketing freelancer and separately a partner in a landscaping business. I wasn't able to work with Nextcloud Tasks both personally and as a project management tracker and I didn't want to use two different productivity services. It just makes way more sense for all my work and personal tasks to be one place. I tested several self-hosted solutions and none of them matched my workflows. So, back to Todoist, which I reluctantly left to begin with.

Of course this means I really want a CLI interface for Todoist so I can use it on my Pinebook Pro. There are several projects that do this, but none of them are for `arm64`. Yet, I was able to get one setup using Docker and this [Todoist CLI client](https://github.com/sachaos/todoist).

I set this up on **Armbian**.

First, install Docker. I used the built-in utility to get Docker up and going.

    $ sudo armbian-config

Then navigate to **Software** and **Softy**. Select Docker and let it do its thing.

Next we need do some configuration updates for Docker. We don't want to [run containers as root](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user) and to do so:

    $ sudo groupadd docker  
    $ sudo usermod -aG docker $USER

Log out and verify the configuration is working.

    $ docker run hello-world

Now it is time to setup the Todoist container. This Github repo as all of the info to get up and running.

[sachaos/todoist](https://github.com/sachaos/todoist)

Here is how I set it up on my Pinebook Pro.

1.  Clone the repo and build the container. I keep all these types of files and executables in my home directory in a folder labeled `bin`.

    $ cd ~/bin
    $ git clone https://github.com/sachaos/todoist.git
    $ cd todoist
    $ make docker-build token=xxxxxxxxxxxxxxxxxxxx

To find your API token, log into Todoist in the browser and go to Settings then Integrations.

2.  In order to run it you need to `cd` into the cloned repo and run `make docker-run`. I'm never going to remember all of that. Instead I created a bash script that will do that for me. As always I'm using `micro` as my text editor.

    $ cd ~/bin  
    $ micro todoist_app.sh

Here is my super basic script:

    #! /bin/bash
    
    cd ~/bin/todoist &&
    make docker-run

Mark it as executable:

    $ chmod +x ~/bin/todoist_app.sh

3.  Last I created an alias in my shell so all I have to remember is a single command. I am using `fish` as my shell.

    $ alias todoist_app='sh /home/dominic/bin/todoist_app.sh'

And that is it. Now running `todoist_app` will exec into the container and I can access, edit, and manage my Todoist in the terminal.