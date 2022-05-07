---
layout: post
title:  "Building the perfect CLI-only laptop with the Pinebook Pro"
date:   2021-02-17 08:07:08 -0800
category: blog
tags: [linux_desktop, cli_apps, tui_apps, pinebook_pro]
---
# Building the perfect CLI-only laptop with the Pinebook Pro
*Feb. 17, 2021*  

### Networking
These are popular and baked right into the OS.  

- nmcli
- [nm-tui](https://www.tecmint.com/nmtui-configure-network-connection/)

**speed-test**  
Went with this snap instead of `fast` because `fast` is not available for arm64 and I want to use on my Pinebook Pro. Instead I'm using `speed-test`.

[bartaz](https://github.com/bartaz) / **[speed-test-snap](https://github.com/bartaz/speed-test-snap)**

### CLI Management

**Fish Shell**  

[Finally, a command line shell for the 90s](https://fishshell.com)

This is much better than the standard bash shell. The directions on their site weren't the way I needed to set it up, however.

First download and install:

```
$ sudo apt install fish
```

Can launch with just `fish` and starts the shell. But if gonna have it, gotta set as default. To do so, first have to add it to the `/etc/shells` file.

```
$ echo /usr/bin/fish | sudo tee -a /etc/shells
```

Then change which shell is used for the system.

```
$ chsh -s /usr/bin/fish
```

**Terminator**  

[Terminator terminal emulator](https://gnome-terminator.org)

Setting this up as the terminal to open at boot on the Pinebook Pro. Since this laptop still has a desktop environment, I still want it to boot straight to a terminal emulator. I have it set to autolaunch with these commands:

* `-m` to maximize window
* `-x tmux` to execute tmux

**Tmux**   

[tmux](https://github.com/tmux) / **[tmux](https://github.com/tmux/tmux)**  
[https://tmuxcheatsheet.com/](https://tmuxcheatsheet.com/)  

Reading [Popey's blog](https://popey.com/blog/2021/02/command-line-only-laptop/), he has a short bash script set to run to spawn windows running specific apps. This is a simple script that I added one option so that each of the windows are named for easy recognition.

```
#! /bin/bash  
tmux new-window mc -n mc  
tmux new-window newsboat -n newsboat  
```

The flag `-n` is to give the window a name. I put this in `~/bin` in a file tilted "apps", then `chmod +x` to make it executable. Once the terminal opens, just run the script and all the services will spawn.

**bpytop**  

[aristocratos](https://github.com/aristocratos) / **[bpytop](https://github.com/aristocratos/bpytop)**

A very nice looking system monitoring tool and available as a snap.

```
$ sudo snap install bpytop
```

### Files

**duf**  

[muesli](https://github.com/muesli) / **[duf](https://github.com/muesli/duf)**

A disk usage analyzer for CLI that has a clean interface. It is essentially a TUI interface for `df` and `du` in one.

Written in Go and has installers for basically every architecture under the sun, including arm64. See all the notes and releases here - [muesli/duf - Github](https://github.com/muesli/duf).

Run with:

```
$ duf   
```

Or pass the path/location at launch.

**mc**

[Midnight Commander](https://midnight-commander.org)

Very simple to use file manager which behaves more like a GUI file manager instead of `cd` or `ls` all the time. Works out perfect for navigating Notes and other files from WebDav.

I wish I could use this while in `cadaver`, but that tool requires to `pull` documents to edit, then `put` to replace.

**NextCloud WebDav**  
This is technically possible, but it is so slow it is not worth using. Besides, I don't want to call the files as I need them, I want specific files to be local. I want the Nextcloud client to sync the files and then I use a file manager or editor to access them.

This is how to setup the webdav connection with Nextcloud.

[Accessing Nextcloud files using WebDAV](https://docs.nextcloud.com/server/18/user_manual/files/access_webdav.html)  

There is a specialized CLI utility for WebDav called `cadaver`. In brief testing this works MUCH better. Speed is not an issue using this client. It is in the official repos, just `apt install cadaver`. To browse a WebDav directory, start like this:

```
$ cadaver <path to mountpoint>
```

It will prompt for password.

To skip entering a password every time, create a file with the base URL of the webdav share plus username password. File should be named `.netrc` and located in the home directory.

```
$ nano ~/.netrc
```

```
machine my.server
	login <username>
	password <password>
```

Then change permissions:

```
$ chmod 600 ~/.netrc
```

**Samba**  

This is how I access files on my desktop around my LAN. Mostly for accessing files on my ZFS array that isn't mounted in Nextcloud. To he honest, instead of using `cadaver` I've just been accessing my Nextcloud files on my desktop via Samba. Then the files aren't local on my Pinebook Pro and I don't have to worry about the sync.

First, install:

```
$ sudo apt install cifs-utils
```

Next, add a folder where the share will be mounted.

```
$ sudo mkdir -p /mnt/my.desktop/cloud_bay  
```

Now I can mount it with this command:

```
sudo mount -t cifs -o username=<username> //<local.dns>/cloud_bay /mnt/my.desktop/cloud_bay/
```

This will mount this one directory that is part of my Samba setup. I don't want to mount at boot on the Pinebook Pro, which can significantly slow things down. Instead, I just want to make it easy to mount when I need it. So, let's create an alias to make the command easy, but not save the password and re-enter every time I want to use it.

```
$ alias smb_cloud_bay='sudo mount -t cifs -o username=<username> //my.server/cloud_bay /mnt/my.desktop/cloud_bay/'  
$ funcsave smb_cloud_bay  
```

Will need to make this for each one of the mounts, but will do it as I run into a situation I need access.

**vdirsyncer**  

[pimutils](https://github.com/pimutils) / **[vdirsyncer](https://github.com/pimutils/vdirsyncer)**

A good reference guide for setting up and using a CLI calendar: [Terminal calendar with Khal](https://www.dj-bauer.de/terminal-calendar-with-khal-en.html)  

This utility will sync CardDav and CalDAV to local folders, then can use these files with other programs. I am particularly interested in using this to sync CalDAV for CLI calendar and todo applications on my Pinebook Pro. On other desktops I can use GUI apps, plus the *Todo.org* app on mobile. This means I would have a self-hosted todo solution that is accessible on all platforms.

There is a steep curve to getting everthing setup.

First, install:

```
$ sudo apt install vdirsyncer
```

Next, need to setup some folders. First need the location of the configuration file plus status folder:

```
$ mkdir -p ~/.vdirsyncer/status
```

Then make a folder where you want the CalDAV info saved. For me:

```
$ mkdir ~/.config/todoist_corriveau_cloud
```

Now, need to setup the config file for the program.

```
$ nano ~/.vdirsyncer/config
```

Below is my configuration file.

```
[general]  
status_path = "~/.vdirsyncer/status/"  

[pair calendar]  
a = "todoist_pbp"  
b = "todoist_corriveau_cloud"  
collections = ["from a", "from b"]  
metadata = ["displayname"]  

[storage todoist_pbp]  
type = "filesystem"  
path = "~/.config/todoist_corriveau_cloud"  
fileext = ".ics"  

[storage todoist_corriveau_cloud]  
type = "caldav"  
#Can be obtained from nextcloud  
url = "https://<local.dns>/remote.php/dav/calendars/<username>/personal/"  
username = "<username>"  
password = "<password>"  
#SSL certificate fingerprint  
verify_fingerprint = "<fingerprint ID see command below"  
#Verify ssl certificate. Set to false if it is self signed and not installed on local machine  
verify = false  
```

To get your server SSL fingerprint, run this command:

```
$ echo -n | openssl s_client -connect your.calserver.lcl:443 | openssl x509 -noout -fingerprint
```

This will display the SSL information and in there will the be fingerprint ID. It will be a series of numbers and letters, similar to a IPv6 address.

Once everything is configured, run:

```
$ vdirsyncer discover  
$ vdirsyncer sync  
```

After syncing, you'll see a series of `.ics` files in the local storage (listed above as `~/.config/todosit_corriveau_cloud`. These can be used with a CalDAV compliant application.

Last, setup cron to run sync so it updates as changes happen across the devices.

```
$ crontab -e
```

and add:  

```
*/15 * * * * vdirsyncer sync  
```


### Email / Comms

**OfflineIMAP**  

[OfflineIMAP](https://github.com/OfflineIMAP) / **[offlineimap](https://github.com/OfflineIMAP/offlineimap)**

A tool to download all email from IMAP to a folder on the local machine. The configuration options are deep and complex. I have a working version of the file on the Pinebook Pro.

There is one gotcha to pay attention to and it has to do with the snap version. The "home" directory it is operates in and looks for files is in `/home/<user>/snap/<number>` not the user home directory in $PATH. For example, if you tell it the configuration file is in `~/Mail` it is going to look in `/home/<user>/snap/299/Mail` for the file, not `/home/<user>/Mail`.

Here are minimum config to get it to work:

```
[general]  
metadata =~/.offlineimap  
maxsyncaccounts = 1  
ignore-readonly = yes  
socktimeout = 60  

[mbnames]  
enabled = no   
filename = ~/Mutt/muttrc.mailboxes  
header = "mailboxes "  
peritem = "+%(accountname)s/%(folername)s"  
sep = " "  
footer = "\n"  
incremental = no  

[Account dom]  
localrepository = LocalGmail  
remoterepository = Gmail  
autorefresh = 15  
synclabels = yes  

[Repository LocalGmail]  
type = MailDir  
localfolders = ~/Gmail  
sep = .  
sync_deletes = yes  

[Repository Gmail]  
type = IMAP  
remotehost = imap.gmail.com  
ssl = yes  
sslcacertfile = OS-DEFAULT  
remoteport = 993  
remoteuser = <email address>  
remotepassfile = ~/.config/<file_name>  
```

Instead of putting a password directly in the config file, I opted to create a separate file with an app password, then point the offlineIMAP config to the file.

```
$ mkdir /home/<user>/snap/299/.config  
$ nano /home/<user>/snap/299/.config/<file_name>  
```

Paste in the app password, no other info or configuration needed. Then change the permissions of the file.

```
$ chmod 600 /home/<user>/snap/299/.config/<file_name>  
```

**Mutt**  

[The Mutt E-Mail Client](http://www.mutt.org)

The standard for all terminal email clients.

Once again, I ran into troubles with where files should live with a snap. In this case the configuration file `.muttrc` needs to live in `/home/<user>/snap/mutt/common` and not in the `../snap/mutt/appnumber` folder most other snaps use. After much fiddling I finally figured this out when I ran `snap info mutt` and it was the only note.

The mutt configuration file isn't too complex. The biggest thing to remember is to make some other folders and a file that are called in the configuration.

```
$ mkdir -p /home/<user>/snap/mutt/common/.mutt/cache  
$ mkdir /home/<user>/snap/mutt/common/.mutt/bodies  
$ touch /home/<user>/snap/mutt/common/.mutt/certificates  
```

Then, write the configuration file.

```
# About Me  
set from = "<email address>"  
set realname = "Dom Corriveau"  

# My credentials  
set smtp_url = "smtps://<user>@smtp.gmail.com"
set smtp_pass = "<app password>"  
set imap_user = "<email address"  
set imap_pass = "<app password>"  

# My mailboxes  
set folder = "imaps://imap.gmail.com"  
set spoolfile = "imaps://imap.gmail.com/INBOX"  
set postponed = "+[Gmail]/Drafts"  
set record = "+[Gmail]/Sent Mail"  
set trash = "+[Gmail]/Trash"  

# Where to put the stuff  
set header_cache = "~/.mutt/cache/headers"  
set message_cachedir = "~/.mutt/cache/bodies"  
set certificate_file = "~/.mutt/certificates"  

# Etc  
set ssl_force_tls = yes  
set mail_check = 30  
set move = no  
set imap_keepalive = 900  
set sort = threads  
set editor = "nano"  
set sort = "reverse-date-received"  
```

**Todoman**

[pimutils](https://github.com/pimutils) / **[todoman](https://github.com/pimutils/todoman)**

This is the CLI todo application I've started with. I would prefer it to be a curses-style application that I can just leave in an open tab, but this is okay because it works with Nextcloud Tasks, which writes the tasks to a calendar. This means can sync using any CalDAV client. On the CLI I am using `vdirsyncer` to pull down the ICS files for CalDAV, then using Todoman to manage on Pinebook Pro.

First, get Todoman installed and setup the configuration folder and file:

```
$ sudo apt install todoman  
$ mkdir ~/.config/todoman  
$ touch ~/.config/todoman/todoman.conf  
```

Now, edit the configuration file - `$ nano ~/.config/todoman/todoman.conf` and point it at the directory `vdirsyncer` is also writing files to.


```
[main]  
# A glob expression which matches all directories relevant.  
path = ~/.config/todoist_corriveau_cloud/*  
date_format = %Y-%m-%d  
time_format = %H:%M  
default_list = Personal  
default_due = 48  
```

That's it. When `todoman` is run, it will use the `.ics` files that are in the folder and when new tasks are added by `todoman` it will create an `.ics. file and be accessible in all the other notes apps, including Nextcloud Notes, Tasks.og, and Gnome To Do.

There is an awesome tabbed interface that makes entering and editing tasks much easier. First need to install `click-repl`:

```
$ pip3 install --user click-repl  
```

Then, when launching the app, use the `repl` flag to enter the new interface.

```
$ todoman repl
```

This interface will give you prompts for start and due date, priority, description, etc.. Once in the `click-repl` interface you can even run `new --interactive` and it will walk you through all the options for adding a task.


**calcurse**  

[calcurse](https://www.calcurse.org)

This is the best looking TUI application for calendar. But, I just couldn't wrap my head around how to configure it to work with a CalDAV setup. Took me forever to realize `calcursre-caldav` wasn't a separate package, but a utility built into `calcurse` itself.

Here's how to set it up with a CalDAV sync. First install it:

```
$ sudo apt install calcurse
```

Next, need to setup the folder along with the configuration file. Run it one time so it will create the base folder. Now, go to the directory `calcurse` uses and add a CalDAV directory.

```
$ mkdir ~/.config/calcurse/caldav  
$ nano ~/.config/calcurse/caldav/config
```

Here is my config file:

```
# If you want to synchronize calcurse with a CalDAV server using  
# calcurse-caldav, create a new directory at $XDG_CONFIG_HOME/calcurse/caldav/  
# (~/.config/calcurse/caldav/) and $XDG_DATA_HOME/calcurse/caldav/  
# (~/.local/share/calcurse/caldav/) and copy this file to  
# $XDG_CONFIG_HOME/calcurse/caldav/config and adjust the configuration below.  
# Alternatively, if using ~/.calcurse, create a new directory at  
# ~/.calcurse/caldav/ and copy this file to ~/.calcurse/caldav/config and adjust  
#  the configuration file below.  

[General]  
# Path to the calcurse binary that is used for importing/exporting items.  
Binary = calcurse  
# Host name of the server that hosts CalDAV.
Hostname = my.server  

# Path to the CalDAV calendar on the host specified above.  
Path = /remote.php/dav/calendars/<user>/<calendar_name/  

# Type of authentication to use. Must be "basic" or "oauth2"  
#AuthMethod = basic  

# Enable this if you want to skip SSL certificate checks.  
InsecureSSL = Yes  
HTTPS = Yes  

# This option allows you to filter the types of tasks synced. To this end, the  
# value of this option should be a comma-separated list of item types, where  
# each item type is either "event", "apt", "recur-event", "recur-apt", "todo",  
# "recur" or "cal". Note that the comma-separated list must not contain any  
# spaces. Refer to the documentation of the --filter-type command line argument  
# of calcurse for more details. Set this option to "cal" if the configured  
# CalDAV server doesn't support tasks, such as is the case with Google  
# Calendar.  
# SyncFilter = cal,todo  

# Disable this option to actually enable synchronization. If it is enabled,  
# nothing is actually written to the server or to the local data files. If you  
# combine DryRun = Yes with Verbose = Yes, you get a log of what would have  
# happened with this option disabled.  
DryRun = No  

# Credentials for HTTP Basic Authentication. Leave this commented out if you do  
# not want to use authentication.  
[Auth]  
Username = <username>    
Password = <password>   

```

Then, run this to import the info before opening `calcurse`:

```
$ calcurse-caldav --init=keep-remote  
```

Now can open `calcurse` and all is there. It is possbile to run multiple instances of `calcurse` for separate calendars, but won't show both together.

Last I setup a crontab to sync the calendar once an hour using the command above. Just add this line to cron:

```
0 * * * * calcurse-caldav --init=keep-remote
```

The official documenation for `calcurs-caldav`:

[calcurse-caldav](https://calcurse.org/files/calcurse-caldav.html)  

### Entertainment

**straw-viewer**

[trizen](https://github.com/trizen) / **[straw-viewer](https://github.com/trizen/straw-viewer)**

A YouTube CLI client that also has a GTK frontend. I've used this before for the frontend to avoid going to the YouTube website. This time I'm only using the CLI client and mostly so I can search for YouTube videos from CLI.

This is written in perl, so had to install a bunch of dependencies.

Install `cpan` to then install perl dependencies and one other program:

```
$ sudo apt install cpan  
$ sudo apt install libwww-perl  
```
Then start cpan:

```
$ sudo cpan
```
Which will drop you to a line and is ready to install perl dependencies.

```
cpan[1]> install Module::Build  
cpan[2]> install LWP::Protocol::https  
cpan[3]> install Data::Dump  
cpan[4]> install JSON  
cpan[5]> install LWP::UserAgent:Cached  
```
Now clone the repo:

```
$ git clone https://github.com/trizen/straw-viewer
```
Change into the directory and build:

```
$ perl Build.PL  
$ sudo ./Build installdeps  
$ sudo ./Build install
```
The [original version of this client](https://github.com/trizen/youtube-viewer) required each instance to have a YouTube API key created and inserted. I switch to this version because it uses the invidio.us API.

I only want to play audio version of videos as I mostly use it to listen to new Retro/Synthwave music. To change it to audio only, start it with:

```
$ straw-viewer --resolution audio
```

Rather than typing this each time, I just set up an alias.

```
$ alias strawyt='straw-viewer --resolution audio  
$ funcsave strawyt  
```
Runs great and I'm very happy to have this on my Pinebook Pro. If I do want to watch a video, can still start it with `straw-viewer` and when selecting a video it will open in MPV.

**Castero**  

[xgi](https://github.com/xgi) / **[castero](https://github.com/xgi/castero)**

A terminal podcatcher and podcast player. The key I was looking for was a way to stream podcasts and not just a downloader. Castero will do both with a pretty good looking interface. It is a Python app, but has support for arm64.

To install:

```
$ pip3 install --user castero
```

Before launching, there are a couple things to do. First, adjust the playback settings to use VLC as the default. Do this by editing the config file `~/.config/castero/castero.conf`. Next, need to set the pip3 install location into $PATH. I do this globally:

```
$ sudo nano /etc/environment
```

And add:

```
/home/<user>/.local/bin
```

Last, need to import the opml file.

```
$ castero --import /path/opml_file
```

**ncspot**  

[hrkfdn](https://github.com/hrkfdn) / **[ncspot](https://github.com/hrkfdn/ncspot)**

Easy enough. Install then run and login. Writes the username/password to file so then any terminal that launches it will automatically login.  

### Passwords

[KeePassXC](https://keepassxc.org/project/)

KeePassXC has a built in CLI client, which can be installed even on a headless system. This does require `xclip` to be installed as well.

Once installed, invoke with:

```
$ keepassxc-cli
```

This has very basic function and does not keep the database unlocked. But, it does work.

Step one is to search for the password. To do this use the `locate` command along with a keyword. The order goes like this:

```
keepassxc-cli locate <keepass-database-name> <search term>
```

This should return a result like:

```
/General/todoist.com
```

Once you have found the entry, use the `clip` command to copy the password to the clipboard. If multiple entries exist, but in different directories, put the directory ahead of the name.

```
keepassxc-cli clip <keepass-database-name> <entry name>
```

With the example above, you would clip like this:

```
keepassxc-cli clip keebass-2021-02-01.kbdx /General/todoist.com
```

Be sure to get the camel-case and syntax correct. Watch out for capital letters in a name that might return negative results just due to camel-case. Put double quotes around anything with spaces to clip the password.

**Official repo vs. Snap**  
In the beginning I tested out using the version in the official repos for Armbian. This version is several releases old and was missing a few features that make using the CLI version of KeePassXC much easier to use. The biggest difference is the ability to open a database and locate/clip passwords without having to enter the master password each time. The Snap is an officially supported version.

Installing the snap:

```
snap install keepassxc
```

Starting the CLI client and opening a database:

```
keepassxc.cli open <database-name>
```

Once this opens, it drops to a new line and then you can use all the same commands, but don't have to authorize each time.

Locating:

```
keybase-20160730> locate todoist
```

Clipping

```
keybase-20160730> clip /General/todoist.com
```

#### News

[Newsboat](https://newsboat.org)

I could not find a ncurses feed reader client that also supports FreshRSS connections. Instead, just using Newsboat and importing the OPML. Newsboat is in the repos and to import the OMPL just do:

```
$ newsboat -I <file>
```

You can manually add new RSS feeds by editing the "urls" file.

```
$ nano ~/snap/<number>/.newsboat/urls
```

#### Weather

[wttr.in](https://github.com/chubin/wttr.in) to get nice looking weather on CLI very fast. Easy to invoke, no installation needed, just run:

```
$ curl wttr.in
```

To call a specific city, run:

```
$ curl wttr.in/yelm
```

Instead of typing this every time, set up an alias in bash to run.

```
$ nano ~/.bashrc  
````

Then add:

```
alias wttr='curl wttr.in/yelm'  
```

Since I am running `fish shell` as my primary on the PBP, setting up an alias is different. Rather than editing the `~/.bashrc` file, just do:

```
$ alias wttr='curl wttr.in/yelm'
$ funcsave wttr  
```

and done.

### Remaining apps & Research
* Twitter (might have figured out Rainbow Stream, notes coming soon)
* Discord (unlikely)
* XMPP

* * *  

### Contact me

Would love to hear from you on this topic!

**Email**: [obscurednarration@gmail.com](mailto:obscurednarration@gmail.com)  
**Twitter**: [@domcorriveau](https://twitter.com/domcorriveau)  

### Get more

These blogs are just the tip of the iceberg. To go deeper and hear more stories around the tech and life around these journals, check out the DC Tech Talks podcast.

[Podcast RSS](https://anchor.fm/s/8af59bc/podcast/rss)  
[Apple Podcasts](https://gwth.us/dcttapple)  
[Spotify](https://gwth.us/dcttspotify)  

### Need even more?
Check out my sister podcast [Go With The Heat](http://gowiththeheat.com/). We just relaunched the show after going through all of the 80’s goodness that was Miami Vice. Now you'll find the best of the best from the greatest era of action movies.

[Go With The Heat Podcast](http://gowiththeheat.com/)  

### Digital marketing professional

Into digital marketing? Get a newsletter all about the best stuff in digital marketing over the last week plus deep-dives into this industry.

[Newsletter](https://corrteksolutions.com/marketing-mixer-newsletter/)  
