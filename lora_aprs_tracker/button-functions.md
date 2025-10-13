---
layout: tracker
title: Button Functions
permalink: /lora_aprs_tracker/button-functions/
---

The functionality of the buttons can differ depending on the specific LoRa APRS tracker device you are using. This page outlines the button operations for the most common devices.

---

## T-Beam

The T-Beam tracker has three buttons. The functions are consistent across all versions.

-   **Left Button (near the USB port):** This is the **power button**, managed by the internal AXP power management unit.

    -   **Press and hold for approximately 8 seconds** to turn the device on or off.

-   **Middle Button:** This is the **user button**.

    -   A **short press** will force the tracker to send a beacon immediately (provided a GPS fix is available).
    -   If you are using the `display timeout` feature, a short press will also wake up the screen.

-   **Right Button:** This is the **reset button**.
    -   A short press will restart the device.

---

## Heltec Wireless Tracker

The Heltec Wireless Tracker is equipped with two buttons. When holding the tracker with the USB port facing down, the buttons operate as follows:

-   **Left Button:** This is the primary **user and power button**.

    -   A **short press** will force the tracker to send a beacon or wake up the screen if it has timed out.
    -   A **long press (about 2 seconds)** will turn the device off by putting it into a deep sleep mode.
        -   ➡️ You can read more about how this works here: [Power Off Modes](/lora_aprs_tracker/power-off-modes/)

-   **Right Button:** This is the **reset/power-on button**.
    -   Use this button to **restart** the tracker.
    -   If the device was turned off using the left button, pressing this button will **turn it back on**.
