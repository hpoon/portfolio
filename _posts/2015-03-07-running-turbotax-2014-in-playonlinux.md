---
layout: post
title: "Running TurboTax 2014 in PlayOnLinux"
categories:
  - Programming
  - Linux
  - Taxes
image: assets/images/playonlinux.png
description: "Step-by-step guide to running TurboTax 2014 on Linux using PlayOnLinux and Wine"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2015/03/07/running-turbotax-2014-in-playonlinux/](https://blog.henrypoon.com/blog/2015/03/07/running-turbotax-2014-in-playonlinux/)

This guide describes how to run TurboTax 2014 in [PlayOnLinux](https://www.playonlinux.com/en/). The PlayOnLinux (in combination with [WINE](https://www.winehq.org/)) software allows users to install Windows-based software.

**CAVEAT:** NETFILE did not work for me. I had to submit my taxes through an installation done on Windows.

## Steps

1. Install PlayOnLinux and then run it (e.g. starting it through the Terminal)

```bash
sudo apt-get install playonlinux
```

2. Click "Tools" > "Manage wine versions"
3. Choose 1.7.27 under "Available Wine versions" and then click the right arrow ">"
4. Go through the steps in the installer and let it finish
5. Back in the PlayOnLinux main screen, click "Install" in the menu, and then click "Install a non-listed program" on the bottom left
6. Choose "Use another version of Wine", when asked, and then choose 1.7.27
7. Choose "Install a program in a new virtual drive", when asked
8. Choose "32 bits windows installation", when asked
9. Find the location of setup.exe for the TurboTax installer (I copied the files off of the disc to a place on my hard drive)
10. Ignore the message "Error in FS_Check" if it appears
11. Let the install complete, but do not launch TurboTax right away
12. Choose "tt2014.exe", if asked to create a shortcut
13. Back in the PlayOnLinux main screen, select entry for TurboTax and click "Configure" in the menu
14. Make sure the "Wine version" is set to 1.7.27
15. Under "Install components", install the following in this order (some of these may not be required, but I don't know which since this is the configuration that worked for me):
    - vcrun2012
    - Microsoft Core Fonts
    - msvc100
    - RegisterFonts
    - vcrun2010
    - dotnet40
    - d3dx9
    - mono28
    - Internet Explorer 8 (click "Restart" in the installer)
    - crypt32
16. Back in the PlayOnLinux main screen, clicking "Run" for TurboTax 2014 should now work!

This is what worked for me, so hopefully this will work for others.
