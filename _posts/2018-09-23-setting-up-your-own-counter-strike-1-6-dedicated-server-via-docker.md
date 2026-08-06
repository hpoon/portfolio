---
layout: post
title: "Setting Up Your Own Counter-Strike 1.6 Dedicated Server via Docker"
categories:
  - Programming
  - Gaming
  - Linux
image: assets/images/docker.png
description: "Running a Counter-Strike 1.6 dedicated server using Docker with Metamod, AMXModX, and Podbot"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2018/09/23/setting-up-your-own-counter-strike-1-6-dedicated-server-via-docker/](https://blog.henrypoon.com/blog/2018/09/23/setting-up-your-own-counter-strike-1-6-dedicated-server-via-docker/)

Once upon a time, you had to run the HLDSUpdateTool, and then SteamCMD. But now, awesome people on the internet have created Docker images for setting up a Counter-Strike 1.6 dedicated server. Now, all you have to do is:

1. Install Docker on your machine
2. Get a Docker image for a CS 1.6 server (I created [this one](https://github.com/hpoon/HLDS-CS1.6), which is based off of an [existing one](https://github.com/kriansa/cs-16-server). Mine has:
   - A lot of maps
   - Metamod
   - AMXModX (with high ping kicker, podbot control menu, round money, rock the vote, and admin all in one)
   - Podbot
3. Customize the server (e.g., editing the server.cfg, amxx.cfg, and other config files, etc.)
4. Start it up! (the README.md in the above linked Git repos has more info on this)

As far as ports go, I only needed to forward 27015 on my machine, but your mileage may vary. Others have reported that [some more ports](https://developer.valvesoftware.com/wiki/Half-Life_Dedicated_Server) must also be forwarded on some machines.

## Setting up as a systemd service (Ubuntu)

If you are running Ubuntu and you want this server to start up like a service via systemd, you will need the following:

1. An executable script with path `/usr/local/bin/hlds` with the following contents (make sure the DIR variable matches your installation directory):

```bash
#!/bin/sh

# Do not change this path
PATH=/bin:/usr/bin:/sbin:/usr/sbin:/usr/local/bin

# The path to the game you want to host
DIR=/opt/cs-16-server/bin
DAEMON=./server

start()
{
    echo  -n "Starting HLDS"
    if [ -e $DIR ]; then
        cd $DIR
        $DAEMON start
    else
        echo "No such directory: $DIR!"
    fi
}

stop()
{
    echo -n "Stopping HLDS"
    if [ -e $DIR ]; then
        cd $DIR
        $DAEMON stop
    else
        echo "No such directory: $DIR!"
    fi
}

reload()
{
    echo -n "Restarting HLDS"
    stop
    sleep 1
    start
}

case "$1" in
    start|stop|reload)
        "$1"
        ;;
    *)
        echo  "Usage: $ 0 {start | stop | reload | status}"
        exit  1
        ;;
esac

exit  0
```

2. A service file with path `/etc/systemd/system/hlds.service` with contents:

```ini
[Unit]
Description=HLDS

[Service]
Type=oneshot
ExecStart=/usr/local/bin/hlds start
ExecStop=/usr/local/bin/hlds stop
ExecReload=/usr/local/bin/hlds reload
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

3. Then execute:

```bash
systemctl daemon-reload
systemctl enable hlds
service hlds start
```

Feel free to check out my server that is running right now with the same Docker image! Here is the command to connect via the console:

```
connect henrypoon.com:27015
```
