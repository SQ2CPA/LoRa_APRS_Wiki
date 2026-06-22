---
layout: tracker
title: Battery Sleep Management
permalink: /lora_aprs_tracker/battery-sleep-management/
---

This feature is for trackers on boards **without an AXP/PMU chip** (for example the **Heltec Wireless Tracker**). These boards have no hardware battery protection, so the firmware takes care of low-battery sleep on its own. It works well in practice and lets you just leave the tracker running — in a car, a backpack, on a bike — without ever having to touch or restart it by hand.

To learn the difference between hardware power-off (AXP) and software deep sleep, see [Power Off Modes](/lora_aprs_tracker/power-off-modes/).

---

## What it does

When the battery gets low, the tracker reports **once** that it is going to sleep, and then sleeps quietly:

-   It does **not** transmit, does not turn on the radio or WiFi, and does not waste power.
-   It does **not** clutter the APRS network with repeated low-battery messages.
-   Every now and then it wakes for a moment just to check the voltage.
-   When you **connect charging**, it notices the voltage rising and brings itself back to full operation on its own once it is safe.

The tracker quietly **learns its own battery** over time, so it can tell the difference between a brief voltage dip (which happens normally while transmitting) and a battery that is really running out. This avoids the annoying loops some devices fall into, where they keep resetting or repeatedly sleeping and waking on a weak cell.

---

## Why it's nice to use

The whole point is that you don't have to think about it. The tracker manages its own battery sensibly:

-   No manual restarts — it returns on its own after charging.
-   No constant resets on a low battery.
-   No spam on the APRS network.

You can simply install it and forget about it until it's time to charge.
