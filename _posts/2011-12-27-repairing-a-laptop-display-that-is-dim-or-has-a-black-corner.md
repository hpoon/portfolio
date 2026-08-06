---
layout: post
title: "Repairing a Laptop Display That Is Dim or Has a Black Corner"
categories:
  - Hardware
  - Electronics
image: assets/images/laptop_blackscreen.png
description: "Diagnosing and fixing LCD backlight and CCFL tube issues causing dim or black corner displays"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2011/12/27/repairing-a-laptop-display-that-is-dim-or-has-a-black-corner/](https://blog.henrypoon.com/blog/2011/12/27/repairing-a-laptop-display-that-is-dim-or-has-a-black-corner/)

## Background

After about three years or more of laptop use, one of the components that is likely to break is something in the LCD assembly. The LCD assembly is a collection of components that allows the laptop to display things on the screen. The following is a list of the primary components and their purpose:

- **LCD Panel** - the part of the assembly that displays the images and is what people are looking at when using the laptop
- **CCFL Tube/Lamp** - provides the light on the display. The LCD panel provides the image, and the lamp provides the light required to see the image.
- **LCD Inverter** - transfers power to the CCFL lamp

The following instructions are general and do not pertain to one specific model of laptops. The theory still applies however.

## Problem Symptoms

In problems regarding a laptop display, these are the common problems among others that are quite prevalent among laptop users.

- **Black corner** - on one corner of the screen, a black triangle can be seen. The mouse can be moved under it, which shows that the LCD is just not displaying that part of the screen. The black corner is also hot to the touch. In some cases, the black triangle can change size over time (on the order of a few minutes or hours).

- **Dim screen** - the LCD is still displaying a picture, but it cannot be seen because there is no backlight. Shining a bright light (such as a desk lamp) illuminates the screen slightly, but not to the brightness that the screen was at before.

The first problem tends to lead to the second one. The CCFL tube burns out and leaves a dim display.

## Determining the Cause

In general, if one experiences at least one of the problems above, there is a clear hardware issue. Some exceptions are when one has turned the brightness all the way down, but this usually isn't the case for people.

If one simply sees a dim display, it is due to **either the CCFL tube or the Inverter**. It is not possible to determine which part is the culprit without opening up the laptop. Refer to instructions specific to the laptop in question to open up the screen assembly. During disassembly, take note of what screws go where. Different sized screws get used for different places and it is very easy to forget which ones go where.

### CCFL Tube

Finding the CCFL Tube on the laptop is a lot more involved than finding the Inverter. It involves opening the LCD panel (see [this website](http://www.laptoprepair101.com/laptop/2007/12/09/replace-laptop-backlight-ccfl-lamp/) for instructions for a Dell Inspiron 1520). Visual inspection of this part can sometimes show clear signs of damage. Burn marks should be apparent.

If burn marks are not apparent, then the cause is likely due to the Inverter. One can also test the CCFL Tube, by turning on the computer with everything still plugged in (but disassembled). If the CCFL Tube lights up, then there is nothing wrong with the CCFL Tube.

### LCD Inverter

It isn't possible to test this part directly without the proper tools. However, if one has a dim display but has checked whether the CCFL works, one can be more certain that the Inverter is the culprit by process of elimination.

## Solution

Once the cause has been determined, the next step is to replace the part. However, one has a choice:

- Replace the entire LCD assembly - costs more (~$100), but the labour is easier
- Replace the problematic parts individually - costs less (~$5 - $20), but more difficult labour

One source for parts is eBay, but it might take around three weeks for the part to arrive. This is cheaper than the $300 that Dell charges for shipping the laptop, buying the components and the labour. Replacing these parts is an involved process will take at least one hour.

Here are some things to watch out for when replacing the CCFL Tube:

- It is difficult to take the part out of the LCD panel
- Watch out for dust that could get in between the layers in the LCD (will show up as black specs *under* the screen)
- It is hard to lay out the layers flat again when the CCFL Tube is replaced so there might be some uneven lighting after the CCFL Tube is replaced

After replacing the parts, turn on the computer again and the screen should be bright again.
