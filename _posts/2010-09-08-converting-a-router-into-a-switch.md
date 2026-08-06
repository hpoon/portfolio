---
layout: post
title: "Converting a Router into a Switch"
categories:
  - Computer Stuff
  - Networking
  - Hardware
image: assets/images/ddwrt.jpg
description: "How to repurpose a router as a network switch to get multiple IPs and double bandwidth"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2010/09/08/converting-a-router-into-a-switch/](https://blog.henrypoon.com/blog/2010/09/08/converting-a-router-into-a-switch/)

By using a switch, I can get twice the bandwidth that I would have normally gotten from UBC Resnet. This is because I am getting more than one IP from Resnet instead of having the router to grab the one IP and rely on NAT for communication. Having one IP means I'd only get one computer's worth of bandwidth split among both computers.

**Warning**: After doing this, I've lost all contact with my router even with the IP of the router changed. This is probably because my router is acting as a switch. The only way that I've found to access the router page is to reset the router. This is probably due to the fact that my router is a piece of junk and I don't know if this is something consistent among all routers.

## Steps

1. Change the IP of the router to something else that is unused in the network (I changed mine to 192.168.0.254)
2. Disable the DHCP client on the router
3. Plug the ethernet cable from the wall/modem to one of the LAN ports on the router (Don't use the WAN port anymore)
4. Plug ethernet cables from each computer to any free LAN port on the router
5. Release/renew IP's on all computers

**Note**: Do not use the WAN port since the DHCP functionality has been disabled.

Despite the drawback of not being able to access the router afterward, I now have all my computers networked. Some people on forums had solutions on retaining access to the router, but those methods didn't work for me.
