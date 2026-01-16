---
layout: tracker
title: Button Functions
permalink: /lora_aprs_tracker/button-functions/
---

The functionality of the buttons can differ depending on the specific LoRa APRS tracker device you are using. This page outlines the button operations for the most common devices.

---

## Lilygo T-Beam

<img src="/assets/images/lora_aprs_tracker/lilygo-t-beam-buttons.png" alt="Lilygo T-Beam Buttons" style="max-width: 400px; width: 100%;">

The T-Beam tracker has three buttons. The functions are consistent across all versions.

- **Left Button (near the USB port):** This is the **power button**, managed by the internal AXP power management unit.
    - **Press and hold for approximately 8 seconds** to turn the device on or off.

- **Middle Button:** This is the **user button**.
    - A **double press** will enter or exit the on-screen menu.
    - A **short press** will force the tracker to send a beacon immediately (provided a GPS fix is available).
    - If you are using the `display timeout` feature, a short press will also wake up the screen.

- **Right Button:** This is the **reset button**.
    - A short press will restart the device.

---

## Heltec Wireless Tracker

<img src="/assets/images/lora_aprs_tracker/heltec-wireless-tracker-buttons.png" alt="Heltec Wireless Tracker Buttons" style="max-width: 400px; width: 100%;">

The Heltec Wireless Tracker is equipped with two buttons. When holding the tracker with the USB port facing down, the buttons operate as follows:

> ⚠️ **Note:** The Heltec Wireless Tracker does not have a dedicated power button because it lacks a PMU (Power Management Unit). To turn off the device, you need to use the [on-screen menu](/lora_aprs_tracker/menu/).

- **Left Button:** This is the primary **user button**.
    - A **short press** will force the tracker to send a beacon or wake up the screen if it has timed out.
    - A **double press** will enter or exit the on-screen menu.

- **Right Button:** This is the **reset button**.
    - Use this button to **restart** the tracker.

---

## Lilygo T-Beam Supreme

<img src="/assets/images/lora_aprs_tracker/lilygo-t-beam-supreme-buttons.png" alt="Lilygo T-Beam Supreme Buttons" style="max-width: 400px; width: 100%;">

The T-Beam Supreme has three buttons located on one side of the device. When looking at the device with the USB port on the right side, the buttons from right to left are:

- **Right Button (near the USB port):** This is the **user button**.
    - A **double press** will enter or exit the on-screen menu.
    - A **short press** will force the tracker to send a beacon immediately (provided a GPS fix is available).
    - If you are using the `display timeout` feature, a short press will also wake up the screen.

- **Middle Button:** This is the **power button**, managed by the internal PMU.
    - **Press and hold for approximately 8 seconds** to turn the device on or off.

- **Left Button:** This is the **reset button**.
    - A short press will restart the device.
