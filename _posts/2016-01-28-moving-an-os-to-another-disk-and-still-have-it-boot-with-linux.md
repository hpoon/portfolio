---
layout: post
title: "Moving an OS to Another Disk and Still Have It Boot with Linux"
categories:
  - Programming
  - Linux
image: assets/images/ubuntu.png
description: "Cloning a disk to a new drive using dd and resizing partitions with gparted"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2016/01/28/moving-an-os-to-another-disk-and-still-have-it-boot-with-linux/](https://blog.henrypoon.com/blog/2016/01/28/moving-an-os-to-another-disk-and-still-have-it-boot-with-linux/)

For the longest time, I had an 80 GB HDD running my Windows partition (dual-boot setup with Ubuntu on an SSD), but I finally upgraded the Windows partition to an SSD as well. I looked into how to clone my Windows partition onto the SSD, such that I could still boot the disk.

I already use Ubuntu as my main OS, so copying the disk was easy using [dd](http://linux.die.net/man/1/dd), which allows copying all the contents of one disk to another. This works well when the new hard drive is greater than or the same size as the current hard drive (I upgraded from an 80GB HDD to a 128GB SSD).

First I ran this to see which disks I was copying from and to:

```bash
fdisk -l
```

Then I ran dd. If I am copying from `/dev/sda` to `/dev/sdb`, then it is:

```bash
dd if=/dev/sda of=/dev/sdb
```

But sometimes the disks do not have the same size, so I used gparted to move/resize the partitions to make use of the extra space on the new disk. gparted complained that it might make my disk non-bootable, but the disk was still bootable for me nonetheless. I did not even have to mess with any grub bootloader settings either. I simply unplugged the old disk, left the new disk plugged in, and booted into the new disk with no problem.
