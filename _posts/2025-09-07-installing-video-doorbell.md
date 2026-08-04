---
layout: post
title: "A Video Doorbell, a Custom Mount, and a Hidden Transformer"
categories:
  - Home Automation
  - 3D Printing
image: assets/images/DoorbellTransformer.jpg
description: "Installing a video doorbell, designing a custom PETG-CF mount, and replacing an underpowered transformer"
---

Installing a video doorbell seemed like it should be a simple replacement: remove the old button, connect the existing doorbell wires, mount the new device, and finish setup.

It turned into a small project involving a custom 3D-printed mount, a voltage problem, and a surprisingly long search for the existing doorbell transformer.

## Reusing the Existing Wiring

The new video doorbell uses the existing low-voltage wiring from the old mechanical doorbell. Reusing the cable avoided running new wire through the exterior wall or door frame, but it also meant the installation depended on the condition and capacity of the existing transformer.

## A Mount for the Door Frame

The door frame did not leave enough flat space for the video doorbell to mount directly. The usable mounting area on the frame was too narrow, while the doorbell needs a wider surface behind it.

I designed and printed a tapered adapter plate to bridge that difference. The narrow end mounts to the available section of the door frame, while the wider end provides the mounting surface required by the doorbell.

The mount was printed in PETG-CF. For this application, the goal was a stiff, weather-tolerant part that would hold its shape and colour outdoors better than a more basic indoor-print material.

## The Voltage Problem

After mounting and wiring the doorbell, it still would not operate correctly.

The existing doorbell chime suggested that its transformer met the doorbell's minimum voltage requirement. In practice, the voltage reaching the video
doorbell was too low; the doorbell's own setup interface reported the problem. I assumed that if the existing doorbell ringer's minimum voltage was already met, but it was not.

At that point, the project became less about mounting the doorbell and more about locating an old transformer.

## Finding the Transformer

The transformer was not located near the electrical panel, which is where I initially expected to find it. I removed the doorbell chime from the wall,
traced the wiring as far as possible, and used a borescope to follow its path through the wall and ceiling space.

![]({{ site.baseurl }}/assets/images/Borescope1.jpg)

![]({{ site.baseurl }}/assets/images/Borescope2.jpg)

After a few hours, I found the transformer mounted above a light fixture.

As expected, it did not supply the necessary voltage. Replacing it with an appropriately sized transformer resolved the voltage problem, and the doorbell began operating normally.
