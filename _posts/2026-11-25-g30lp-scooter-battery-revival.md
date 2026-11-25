---
layout: post
title: "Reviving a Segway G30LP That Would Not Charge"
categories:
  - Repair
  - Electronics
image: assets/images/G30LPBattery1.jpg
description: "Fixing a Ninebot G30LP scooter battery that refused to charge after months in storage, by charging one low cell group with a bench power supply"
---

My Segway Ninebot G30LP scooter sat unused for several months. When I plugged in the charger, the scooter did not charge.

The cause was a deeply discharged battery. A lithium pack slowly loses charge while it sits, even when the scooter is off. After months, one part of the pack can drop below the voltage that the battery management system (BMS) accepts. The BMS then refuses to charge the pack. This is a safety feature.

## How The Pack Is Built

The G30LP battery is a 10S pack. It has 10 cell groups in series. The nominal voltage is 36V, and a full pack reads 42V. The stock charger outputs 42V. The BMS sits in the battery bay with the cells. It does three jobs:

1. It cuts off the output when a cell group gets too low.
2. It balances the cell groups while they charge.
3. It switches the charge current and the discharge current.

The BMS has a balance connector. This connector has one sense wire for each junction between two cell groups. The BMS reads each cell group through these wires. I used the same connector to find the weak cell.

## Diagnosis

The battery has three sets of wires:

- A thick red and black pair with an XT60 connector. This pair goes to the controller.
- A medium red and black pair. This pair goes to the charge port.
- A thin cable with many small wires. This cable carries the BMS data.

I measured the pack voltage first. It read 33V. That is an average of 3.3V for each cell group. The pack voltage does not show if one cell group is weaker than the others, so I measured each cell group.

To find B+ and B−, I used the multimeter on the nickel plates closest to the BMS board. The two plates with the pack voltage between them are B+ and B−.

Then I measured the cell groups at the balance connector:

1. I put the black probe on B−.
2. I put the red probe on the first balance pin and read the voltage.
3. I moved the red probe to each next balance pin in turn.

The voltage rises at each pin. Each rise is the voltage of one cell group, so the steps should be nearly equal. The step for cell group 10 was smaller than the rest. This is how I know that cell group 10 was the lowest. The step for cell group 7 was also small, but it was not small enough to block the charge.

The BMS refuses to charge the pack when one cell group is too low. So cell group 10 was the likely reason for the blocked charger.

## The Fix

The idea is simple. The BMS blocks the charger because one cell group is too low. If I raise that cell group above the cutoff, the BMS accepts the charger again.

I charged cell group 10 alone with a bench power supply:

1. I set the supply to 3.7V.
2. I set the current limit to 0.3A.
3. I put the red lead on the nickel plate of cell group 10.
4. I put the black lead on the balance connector pin for cell group 10.
5. I turned on the supply and watched the voltage.

![Red lead from the bench supply on the nickel plate of cell group 10]({{ site.baseurl }}/assets/images/G30LPBattery1.jpg)

The current limit is important. A cell group that is very low can take a lot of current if the supply has no limit. The limit keeps the charge slow and safe.

![The bench supply at 0.16A and 2.6V, before I raised the current limit]({{ site.baseurl }}/assets/images/G30LPBattery2.jpg)

In this photo the supply shows 0.16A and 2.6V. The current is low because I had not raised the current limit yet. I raised it to 0.3A after this photo. The supply stayed in constant-current mode, and the voltage rose slowly. I checked the cell group voltage often with a multimeter.

![The leads in place on the battery, with a multimeter ready]({{ site.baseurl }}/assets/images/G30LPBattery3.jpg)

When cell group 10 reached about 3.2V, I removed the bench supply. Then I plugged in the stock charger at the charge port. The BMS accepted the charge, and the stock charger took over.

## Circuit Diagram

This diagram shows how the parts connect. The dashed red and black lines show where I connected the bench supply. Everything else is the normal wiring of the scooter.

![Circuit diagram of the G30LP battery, BMS, controller and the temporary bench supply connection]({{ site.baseurl }}/assets/images/G30LPBatteryCircuit.drawio.png)

The path of the power is:

- The 10 cell groups connect in series. The B+ and B− leads of the pack go to the BMS.
- The sense wires go from each cell group junction to the balance connector of the BMS.
- The charge port goes to the charge input of the BMS. The stock charger plugs into this port.
- The discharge port of the BMS goes through the XT60 lead to the controller.
- The controller drives the hub motor. It also connects to the dashboard, the throttle, the brake and the lights.
- The data line of the BMS goes to the controller.

The bench supply connects to only one cell group. The red lead touches the nickel plate on the plus side of cell group 10. The black lead touches the balance connector pin for the same cell group. The BMS charge path and the controller are not part of this connection. That is why the method works when the BMS blocks the normal charge port.

## Safety

A lithium pack that was deeply discharged can have damaged cells. A damaged pack can catch fire. Follow these rules:

- Work outside or on a surface that does not burn.
- Check the cell temperature with a temperature gun while the battery charges.
- Do not leave the battery unattended while it charges.
- Keep the current low.
- Stop at once if a cell group gets warm, swells or smells strange.
- Do not revive a cell group that is below about 2V. Replace it instead.
- Never let the probes or the leads touch two points at the same time.

I did not follow the first rule. I assumed that a scooter left idle had a low chance of damaged cells. I did use a temperature gun to check the temperature while I charged. I still recommend that you follow all of these rules.

## What Is Next

Cell group 7 is still lower than the others. I will watch it over the next few charges. If it drifts out of balance, or if the pack loses charge fast, I will replace the cells.

To prevent this problem, charge the scooter every month or two. For long storage, keep the charge between 50% and 70%.
