---
layout: post
title: "My Brief Experience with iPodLinux and Rockbox"
categories:
  - Computer Stuff
  - Linux
  - iPod
image: assets/images/apple.jpg
description: "Comparing iPodLinux and Rockbox custom firmware for iPod - installation experiences and features"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2009/12/09/my-brief-experience-with-ipodlinux-and-rockbox/](https://blog.henrypoon.com/blog/2009/12/09/my-brief-experience-with-ipodlinux-and-rockbox/)

Sometime in 2005 I saw a video of someone playing Half-Life on an iPod and I thought it was kind of cool that it was possible. I found out that the person was running Linux on their iPod with id Software's Doom installed (a version ported to the iPod). I also found out that Linux on an iPod comes in two flavors: [iPodLinux](http://www.ipodlinux.org/) and [Rockbox](http://www.rockbox.org/). I decided to try both. I started with iPodLinux.

## iPod Linux

The installation of iPodLinux requires the user to download the source code from their Subversion Repository and then compile it. There were binaries available for download, but those were two years out of date. Downloading the source code required the installation of an SVN client, and compiling the source code required the installation of Qt with MinGW. I ran into a slight snag here as the installation guide on their site neglected to tell me that Qt would not set the system environment variables needed in order for me to follow the instructions in the guide as is. Typing "qmake" kept giving me "qmake is not recognized" error in the Windows command line. Once I set up the environment variables, I was able to compile the source code.

After compiling the code, I went onto installation. Whenever I tried to install iPodLinux, the installer would close while trying to partition my iPod. As a result, my iPod was left half partitioned with no OS. I had to restore my iPod with iTunes every time this happened. I figured it was because I was using Windows 7 Pro x64. Even after setting compatibility options and running as administrator, the installer wouldn't work. I then repeated everything I had done so far on a Windows XP Pro machine and was finally able to install iPodLinux.

The next step was to boot the OS for the first time. While loading the different modules, the OS would complain about how some modules were didn't exist or my iPod had run out of memory. Then the iPod later got stuck while initializing some module called "MPDc". So what I tried to do next was to install iPodLinux without this module. Stupidly enough, the installer refused to let me uncheck any of the options while clearly stating that I could uncheck certain ones if I didn't want them. What I don't get is why I'm getting all these errors with my iPod when the developers state that my 5th gen iPod Video is supported. Maybe I'm missing something?

Then I found out about the ZeroSlackr Project, which is supposed to provide a "simple, coherent, easy-to-use and newbie friendly method of installing iPodLinux on iPods". After downloading, first thing I did was look at the readme's to see how to install it. I opened up the readme and it gave me the worst formatting I'd ever seen in a text file. There were no line breaks. Rather than searching through this wall of text I just looked up how to install it on Google. I opened the batch file included with the install files and it gave me a message saying installation successful and that I could now boot ZeroSlackr from my iPod. I took out the iPod and booted it up just to see no option for ZeroSlackr in the Bootloader. Maybe I did something wrong.

I also tried a program called iPod Manager 2.0.5, but it didn't even open no matter how many times I tried to open it.

Afterward, I figure I could use a program to see the ext2 partition that iPodLinux makes and delete the modules manually from there. Browsing the iPodLinux forums and Google searches led me to a program called LTOOLS. It was supposedly able to let me modify the ext2 partition. No luck with that either. I kept getting stopped by the "Windows could not find file specified" error whenever I tried to look in the ext2 partition. Next program I tried was Ext2 IFS for Windows. I've used this program successfully in the past to grab files from my Ubuntu partition. For some reason this program didn't work either. Luckily using my Ubuntu 8.04 Live CD to open the ext2 partition on the iPod worked for me. The ext2 and the FAT32 partition appeared right away in Ubuntu and all I had to do was do a "gksudo nautilus" to delete the files I didn't want.

After removing the problematic modules, I finally loaded up the OS. However, the moment I selected any menu option, the iPod would freeze. I waited about 30 seconds with no response. This problem is probably quite beyond me so I stopped here.

## Rockbox

The thing I liked the most out of Rockbox is that the installation of it worked, without any hassles. All I did was download it, double click, follow the instructions and then bam it worked. It also installs without requiring you to partition your iPod to ext2. As a result, I could access the Rockbox files easily within Windows. I loaded up iTunes and it was still able to sync my stuff onto it.

Once I synced my music onto the iPod again, I tried playing music with it. Without looking at the manual, I could not use my library as one huge playlist. I find that if using the interface on an mp3 player needs a manual for people to know whats going on, its probably too complex. Take the iPod interface for example. It is very intuitive. There was virtually no learning curve in figuring out how to use it.

Another thing that really annoyed me on Rockbox is that even after setting the language options, I still was not able to see Chinese ID3 tags on songs. How am I supposed to be able to choose a song if I can't see the title?

What I did like about Rockbox are the apps. I know iPodLinux has them too, but seeing that I never got past the freezing problem, I couldn't try them out. My favorite was RockDoom. Being able to play a classic game like that on an iPod made me feel a bit nostalgic.

## Conclusions

iPodLinux needs a little bit more work in making installation of the OS easier. To be specific, their documentation needs to add solutions for problems like the one I mentioned before. It should also let people uncheck things in the installer. And most important of all, it should work without freezing up all the time. If all 5th gen iPod Videos are standard, then if I have a problem on mine, wouldn't that mean everyone else's 5G iPod will have problems with it?

Really, I liked everything about Rockbox except its interface and its lack of support for seeing Chinese characters. I was even able to play a Counter-Strike mod for RockDoom. I thought that was fantastic.

There are probably also some fixes out there that I don't know about that can solve my problems, but seeing that I only used iPodLinux and Rockbox so briefly, I probably never came across those fixes. I also feel that the sorts of problems I had should not need fixes, but rather they shouldn't occur at all.
