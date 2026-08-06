---
layout: post
title: "Attempting a 3D-Printed Steam Engine"
date: 2025-11-20
categories:
  - 3D Printing
  - Hardware
image: assets/images/SteamEngine.jpeg
description: "Prototyping a single-stroke reciprocating steam engine, then discovering the limits of PET-CF near a heating element"
---

I attempted to build a small, single-stroke reciprocating steam engine.

The initial goal was simply to see whether I could make the mechanism work: convert the back-and-forth motion of a piston into rotation using a connecting
rod and crankshaft. I was less interested in building a highly efficient engine than in making a physical mechanism that could run under steam.

## Starting With PLA

I first printed the engine in PLA.

PLA was not intended to be the final material. It was only a low-cost way to prototype the design, assemble the moving parts, and check whether the piston,
connecting rod, flywheel, and crankshaft could move together as intended.

The mechanism worked well enough to justify trying a version that could handle heat.

## Trying PET-CF

For the next version, I used PET-CF: PET filament reinforced with carbon fibre.

According to the filament datasheet, the material should not deform at boiling water temperatures. That seemed promising, since the engine was intended to
use steam generated from water.

To keep the plastic away from direct contact with the heater, I used a metal cup as the boiler. The metal cup made contact with the heating element, while
the printed components formed the engine around it.

That reasoning turned out to be too optimistic.

## Heat Was Still the Problem

The PET-CF parts eventually deformed.

The problem was likely that the heating element itself was substantially hotter than the boiling water inside the cup. Even if the water stays close to 100°C,
the surrounding air, metal, and nearby surfaces can become much hotter.

The material therefore had to survive more than just the temperature of the water. It also had to survive radiant and ambient heat from the heating element
and the hot metal cup.

<video controls preload="metadata" class="centered post-video">
  <source src="{{ site.baseurl }}/assets/images/SteamEngine.mp4" type="video/mp4">
  Your browser does not support embedded video.
</video>

If I revisit the project, the next version would need a more deliberate approach to heat isolation and would likely require metal parts around the
boiler and heating area rather than relying on printed plastic.

> This was an experimental prototype, not a pressure-rated boiler design. Steam and heated vessels can create hazardous pressure, so I would not treat this construction as safe for unattended or enclosed operation.
