---
layout: post
title: "Running LINE Messenger in Ubuntu 14.04"
categories:
  - Programming
  - Linux
  - Computer Stuff
image: assets/images/ubuntu.png
description: "How to run LINE Messenger on Ubuntu 14.04 using Wine"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2015/02/09/running-line-messenger-in-ubuntu-14-04/](https://blog.henrypoon.com/blog/2015/02/09/running-line-messenger-in-ubuntu-14-04/)

LINE is a messaging program kind of like WhatsApp, but it has a desktop client. However, this desktop client only runs on Windows. On Linux, it has to run under [Wine](https://www.winehq.org/), which allows running Windows programs (some) inside the Linux environment. **Caveat: sending stickers does not appear to work.**

**UPDATE 7 JULY 2015:** Since this post, my version of LINE has been updated to 4.0.3.367, and it looks like stickers work now!

**UPDATE 31 JULY 2016:** Looks like in July 2015, LINE released a Chrome app. Users of Chrome can just use that extension instead of using this method: [LINE Chrome Extension](https://chrome.google.com/webstore/detail/line/ophjlpahpchlmihnnnihgmmeilfjmjjc)

## Running LINE in Ubuntu 14.04

1. **Install Wine**

```bash
sudo apt-get install wine
```

2. **Install VC++ 2008 Redistributable**

```bash
winetricks vcrun2008
```

3. **Download and install [LINE](http://line.me/en-US/download) for Windows**

Without installing the VC++ 2008 Redistributable, LINE would intermittently crash (even though it was able to start correctly).

This worked on my Ubuntu 14.04 x64 system.

- LINE Version: 3.9.1.188
- Wine Version: 1.6.2
