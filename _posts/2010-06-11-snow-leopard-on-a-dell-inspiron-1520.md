---
layout: post
title: "Snow Leopard on a Dell Inspiron 1520"
categories:
  - Computer Stuff
  - Hackintosh
  - MacOS
image: assets/images/apple.jpg
description: "Complete guide to installing Mac OS X Snow Leopard on a Dell Inspiron 1520 laptop with working hardware"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2010/06/11/snow-leopard-on-a-dell-inspiron-1520/](https://blog.henrypoon.com/blog/2010/06/11/snow-leopard-on-a-dell-inspiron-1520/)

After a lot of reinstalling and kext testing I've finally managed to get my Inspiron 1520 to run Snow Leopard with the latest updates and things working. I tried my best to list the sources of info that I found, but I Googled so much useful and not so useful links that I don't remember which are which anymore.

## Computer Specs

- Intel Core 2 Duo T5250 Processor
- 2 GB RAM @ 667 Ghz
- Intel GM965 Chipset
- nVidia GeForce 8600M GT
- Dell Wireless 1390 802.11g

## Installation

I was lucky enough to only need the Retail Snow Leopard Disc (10A432) and the [myHack Installer 1.0.1](http://osx86.sojugarden.com/2010/06/myhack-installer-1-1-released/). I pretty much followed METHOD 2 in this guide (method 1 didn't really work out for me, but it might have had something to do with the disc restoration part of the guide):

<http://prasys.co.cc/2009/08/installing-snow-leopard-for-osx86/>

For the myHack installer, check the box for the kext that says something about PS2 in it. It will enable the laptop touchpad and keyboard. Also, read the description for each kext to see if you need it or not.

When I used method 1 in the guide, I had some trouble with an installation error that said "Could not verify BaseSystem.pkg" or something along those lines. That error appeared at about 10-15% installation progress. It went away then I used method 2. I did read somewhere that it may have had to do with the restoration in Disk Utility. Either way, it worked the second time around.

Once SL was installed, I ran the myHack Installer on my drive to get the Chameleon Bootloader on there so I wouldn't have to use my USB to boot all the time. Also, be sure not to install GraphicsEnabler as it will prevent your computer from shutting down completely (more on that later).

## Graphics

Since my laptop uses an nVidia card, there is an issue that prevents the computer from shutting down completely if the "GraphicsEnabler" option is used in the myHack Installer. I believe NVInject, NVKush, and NVDarwin all suffer from this same problem. What happens is that when the shut down command is invoked, the computer's screen will turn off, the HD will turn off, but the power stays on. When the nVidia graphics kexts aren't used, this problem goes away.

I've tried generating an EFI String and loading that with EFI Studio, but it didn't do the job. The resolution is still 1024x768 and I have no QE, CI or OpenGL support. What I did later on was install PC EFI to see if that would fix things (I didn't really know what I was doing here at this point). That didn't really work, but I did later find out that EFI Studio allows me to add boot flags. I added "Graphics Mode"="1280x800x32" to the boot flag so now it boots with the proper resolution. It gives the proper resolution, but still no QE/CI or OpenGL.

This guide has information on how to test for QE (Quartz Extreme) and CI (Core Image): <http://prasys.co.cc/tag/enable-qeci/>

Another thing I tried was to modify my DSDT to get my graphics card working using this link: <http://tonymacx86.blogspot.com/2010/01/advanced-dsdt-fixes-nvidia-graphics.html>. I managed to get the card recognized using the DSDT code, but when I got rid of the graphics kexts, and the boot.plist options as specified in the guide, I lost my graphics acceleration. I know my DSDT code is working here still since System Profiler tells me what card I have with the exact same names that I gave in the DSDT. It seems that having graphics acceleration and shutdown/restart working properly just isn't meant to be.

**The tradeoff:**

I either could have proper graphics acceleration and no shutdown, OR I could have shut down and no graphics acceleration. Graphics is the clear winner here, but I still hate having no shutdown. I have not found a fix for this.

## Power Management

There was a problem with high CPU temperatures with the laptop. I installed the VoodooPowerMini kext located here: <http://forum.voodooprojects.org/index.php/topic,1095.0.html>

## Audio

After looking for various kexts, I found that VoodooHDA worked for me. It can be found here: <http://www.kexts.com/view/70-voodoohda_(32--_64-bit,_recompiled_by_prasys).html>

## Wireless

Works after installation.

## USB Ports

They work since it can recognize my mouse and USB drive.

## Battery Indicator

I used the VoodooBattery kext located here: <http://forum.voodooprojects.org/index.php/topic,1092.0.html>

## Card Reader

I don't use this so I didn't install the kext for it. It can be found here: <http://www.dailyblogged.com/retail-snow-leopard-installation-guide/> or [SD Card Fix](http://www.dailyblogged.com/wp-content/uploads/2009/09/VoodooSDHC.kext.zip) (more direct).

## Touchpad

I had an issue where I couldn't tap the touchpad in order for it to "click". I fixed this issue by installing the VoodooPS2Controller kext (check the Trackpad option during the installation) <http://forum.voodooprojects.org/index.php/topic,235.0.html>. Then I installed the preference pane (this allows configuring the Trackpad through System Prefs) here <http://www.dailyblogged.com/retail-snow-leopard-installation-guide/> (command -f to find it). I opened System Preferences and pressed the Show All button, and I saw a "Trackpad" option, so I opened it and the option was there.

## Webcam

Works after installation.

## Conclusion

Everything I listed here works except for video and the card reader. There are other things like Ethernet, but I don't really use it.
