---
layout: general
title: Support for New Device
permalink: /general/support-new-device/
---

## Before You Request Support for a New Device

Before asking for support of a specific board or device in the Tracker or Digi/iGate firmware, please consider the following. Adding support for a new device requires development time and (more important!) ongoing maintenance. Not every request makes practical and economical sense.

## Use the Right Device for the Right Purpose

Each LoRa APRS project is designed with a general specific use case in mind:

- **Tracker** - a portable, battery-powered device with GPS for position reporting
- **Digi/iGate** - a stationary device for digipeating and/or internet gateway functionality, without GPS

If you have a device that was designed as a tracker (e.g. with built-in GPS and battery holder) and you want to run iGate software on it - **that doesn't make sense**. The hardware was built for a different purpose. Similarly, trying to use a stationary iGate board as a portable tracker is not a good idea.

Use the device for what it was designed to do.

## Your Device Is Broken? Fix It First

If you have a device like a Lilygo T-Beam with a broken GPS module, the solution is to **repair or replace the broken component** - not to request a firmware variant that works without GPS. A tracker without GPS is not a tracker.

The same applies to other broken components. Fix the hardware issue and continue using the device as intended.

## When Does Adding a New Device Make Sense?

Adding support for a new board makes sense when:

- **A significant number of people will benefit** - for example, a local club or a large group of operators want to use the same board
- **The device is (commercially) available and popular** - not a one-off custom build
- **The hardware is suitable for the intended purpose** - a tracker board for Tracker firmware, a stationary board for Digi/iGate firmware

Adding support does **not** make sense when:

- You have **one specific device** and want custom firmware just for yourself
- The device is **not designed** for the intended use case
- You want to work around a **hardware defect** instead of fixing it

For a single unique device, the development and maintenance effort of an individual implementation is simply not justified.

## DIY Option

There are ready-made DIY variants available with a defined pinout. If you want to build your own device, simply wire it according to the pinout specified in the variant and it will just work:

**[DIY Variants](https://github.com/SQ2CPA/LoRa_APRS_Flasher/tree/master/variants)**

Each variant defines a specific combination of processor and LoRa module (e.g. ESP32 + SX1278, ESP32-C3 + SX1262, etc.) with a fixed pin configuration. You pick the variant that matches your components and build your hardware accordingly - you do **not** modify the pinout to match your custom wiring.

## Currently Supported Boards

Check the list of officially supported boards for each project:

- [Tracker - Supported Boards](/lora_aprs_tracker/supported-boards/)
- [Digi/iGate - Supported Boards](/lora_aprs_digi/supported-boards/)

If your board is already on the list, no additional support request is needed.
