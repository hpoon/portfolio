---
layout: post
title: "The Dryer Stopped Spinning"
categories:
  - Repair
  - Appliances
image: assets/images/FixingDryer2.jpeg
description: "Diagnosing and repairing a dryer that still powered on but would no longer turn the drum"
---

The dryer would power on, but the drum would not spin.

That narrowed the problem down to the parts responsible for turning the drum: the drive motor, belt, idler/tension system, door switch, control circuitry,
or a safety component somewhere in the circuit.

## Getting Inside

Accessing the components required removing the top panel, front panel, and enough of the surrounding structure to expose the drum, blower housing, motor
area, and wiring. Had to look up on YouTube to find my dryer, but turns out my Kenmore dryer is a rebranded Samsung dryer.

![]({{ site.baseurl }}/assets/images/FixingDryer3.jpeg)

Dryers are more densely packed than they first appear. What looks like a simple appliance from the outside contains a belt-driven drum, motor, blower,
heater, sensors, switches, and a surprising amount of sheet metal.

## Diagnosis

Most Internet literature talked about broken heaters and what not, and suggesting using a multimeter to check the connectivity between the thermostat, the heating element, and the fuse as they are connected in series. Any break in those components would cause the dryer to not work.

![Dryer motor and ducting area during the repair]({{ site.baseurl }}/assets/images/FixingDryer1.jpeg)

All three components passed connectivity test. I later learned that if those components failed, the dryer would still spin, but not heat, which is not the problem I was having.

Next was to check the mechanical assembly. Turns out the drive belt had fallen off the pulley. The idler inside loses the tension which triggers a limit switch that cuts power to the heater so that the heating element cannot operate (safety feature).

![Dryer motor and ducting area during the repair]({{ site.baseurl }}/assets/images/FixingDryer2.jpeg)

# My Rudimentary Summary of How A Dryer Works

The AC motor drives a belt that spins the drum. There is an idler pulley that triggers a limit switch if the belt is not routed through the idler (my situation). Since the AC power drives the motor at a fixed AC voltage, the dryer motor runs at a single speed (adding a VFD is an option, but my dryer does not appear to have multiple speeds). While the motor spins and drives the drum, a circuit powers a heating element, a thermostat, and a fuse, which allows controlled heating and a safety stop. The spinning belt also drives a fan that circulates air through the heater and into the drum. The air goes through the drum and into the lint trap and then out the exhaust.
