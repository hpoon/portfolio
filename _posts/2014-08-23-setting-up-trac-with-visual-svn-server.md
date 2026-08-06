---
layout: post
title: "Setting Up Trac with Visual SVN Server"
categories:
  - Programming
  - Windows
image: assets/images/svn.png
description: "Configuring Trac bug tracking with Visual SVN Server for Windows"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2014/08/23/setting-up-trac-with-visual-svn-server/](https://blog.henrypoon.com/blog/2014/08/23/setting-up-trac-with-visual-svn-server/)

Bug trackers are an important part of developing software as they allow teams to manage bugs, features, planning, etc. There are a lot to choose from out there, but out of curiosity I decided to set up my own. I chose to use Trac for this purpose. Since I already use Visual SVN Server, I was able to set up Trac with Visual SVN.

**All instructions in this post use Windows.**

## Setup

I pretty much used the instructions here: [http://www.visualsvn.com/server/trac/](http://www.visualsvn.com/server/trac/). I did not do step 8 written in the instructions, and it still worked for me. However, what is not set up is the Trac administrator account. After the setup, I was able to access the Trac web app and was also able to view the SVN logs, revisions, etc. I initially got a message about "no changesets", but after a commit to the repo, everything showed up on the web app.

## Setting up the Admin Account

While the above instructions allow you to login to Trac using the existing SVN credentials, that user is not considered an admin user. All I had to do was run this command:

```bash
trac-admin /path/to/projenv permission add bob TRAC_ADMIN
```

After restarting the server, the admin tab was available in Trac. Now Trac is available for use for bug tracking with an existing SVN repo!
