---
layout: post
title: "Snow Leopard on a Virtual Machine"
categories:
  - Computer Stuff
  - Hackintosh
  - Virtualization
image: assets/images/apple.jpg
description: "Guide to installing Mac OS X Snow Leopard in VMWare on a Windows host"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2010/06/08/snow-leopard-on-a-virtual-machine/](https://blog.henrypoon.com/blog/2010/06/08/snow-leopard-on-a-virtual-machine/)

Here is an article that teaches you how to install Snow Leopard in VMWare using a Windows host.

## Links

- <http://www.ihackintosh.com/2009/12/install-snow-leopard-in-vmware-7-windows-edition/>
- <http://www.online-tech-tips.com/mac-os-x/install-snow-leopard-on-pc/>

## Notes

The `darwin_snow.iso` must always be mounted in the VM's CD/DVD drive in order for the OS to boot. Shutting down the VM by pressing shut down in the OS will cause a kernel panic. The workaround is to open the `.vmx` file associated with the virtual machine and change `smc.present` from `true` to `false`.
