---
title: "PinePhone (Pro) Battery Charger Teardown"
categories: [ "teardown" ]
tags: [ "PinePhone", "PPPro", "Linux Mobile", "Teardown" ]
excerpt: "Teardown of the Pine64 Pinephone standalone battery charger"
---

# PinePhone Battery Charger

I recently picked up this little battery charger made specifically for the Samsung J7 battery used by the PinePhone (Pro). It features:

- A single USB-C port
- Red/green status LEDs

Yeah that's about it. Very simple, but that's good.

Seems to work just fine, but for shits and giggles I decided to break it open. I figured maybe this could be useful to someone making their own charger.

## Outside

For lack of better photos, here's the original product picture from Pine64:

![Product picture](/assets/images/2023-12-27-pinephone-battery-charger/product1.png)

## PCB

This is the very simple PCB inside. It's based around the MICRONE ME4057DSPG-N IC.

![PCB](/assets/images/2023-12-27-pinephone-battery-charger/pcb.jpg)

[Here][1] is a (somewhat poorly) translated copy of the datasheet.

The charging logic for this IC is as follows:

- Under 2.9V, trickle charge at <sup>1</sup>/<sub>10</sub> I<sub>BAT</sub>
- CC to 4.35V
- CV at 4.35 until current falls to <sup>1</sup>/<sub>10</sub> I<sub>BAT</sub>
- Off, showing (Green) STBY LED
- If voltage drops to 4.16V, charging is resumed from the CC stage

### Schematic

![Schematic](/assets/images/2023-12-27-pinephone-battery-charger/schematic.png)

From the datasheet, I<sub>BAT</sub> = 1100/R<sub>PROG</sub>, meaning the battery charging current is approx. 790mA or 0.26C of the original 3000mAh battery that comes with the PinePhone (Pro), and trickle & cutoff current is about 79mA.

[1]:{{ site.url }}/assets/downloads/2023-12-27-pinephone-battery-charger/Microne-ME4057DSPG-N.pdf
