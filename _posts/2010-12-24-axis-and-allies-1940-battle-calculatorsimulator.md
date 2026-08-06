---
layout: post
title: "Axis and Allies 1940 Battle Calculator/Simulator"
categories:
  - Programming
  - Games
  - Java
image: assets/images/aa40calc_thumb.png
description: "A battle calculator and simulator for Axis and Allies 1940 board game with full combat rules"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2010/12/24/axis-and-allies-1940-battle-calculatorsimulator/](https://blog.henrypoon.com/blog/2010/12/24/axis-and-allies-1940-battle-calculatorsimulator/)

This is a program I made for calculating the odds for battles in Axis and Allies 1940. It follows the combat rules for the game and counts the average probability of victory/defeat including IPC values lost. This program is released under the GPL.

For an updated version with attacker/defender swap functionality, see: [Axis and Allies 1940 Battle Calculator/Simulator Updated to v1.0]({% post_url 2010-12-29-axis-and-allies-1940-battle-calculatorsimulator-updated-to-v1-0 %})

## Download

[Download from SourceForge](https://sourceforge.net/projects/aa40battlecalc/files/Battle%20Calculator%20Binary/) (requires [Java](http://www.java.com/en/download/manual.jsp))

## Features

- Land and naval battles
- Coastal bombardments from Cruisers and Battleships
- Option for ground units that must survive to capture the territory
- Option for aircraft that must land on an Aircraft Carrier
- User specifiable option for how many trials to do
- Follows combat rules from Axis and Allies 1940 (Europe and Pacific) such as:
  - Regular land battle rules (dice rolling)
  - Order of taking casualties
  - Submarine first strike and can be negated by Destroyer
  - Planes cannot hit Submarines unless the planes are accompanied by a Destroyer
  - Artillery-supported Infantry and Mechanized Infantry
  - Fighter-supported Tactical Bombers
  - Wounds on Battleships and Aircraft Carriers

## Statistics

- Attacker/defender win/loss/tie percentages
- IPC cost of both armies
- IPC loss of both armies
- Units remaining of both armies

## Links

- **SourceForge Page**: <http://sourceforge.net/projects/aa40battlecalc/>
- **Source Code**: <https://sourceforge.net/projects/aa40battlecalc/files/Battle%20Calculator%20Source/>
