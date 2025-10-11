---
layout: tracker
title: Bluetooth
permalink: /lora_aprs_tracker/bluetooth/
---

This firmware supports Terminal Node Controller (TNC) functionality over Bluetooth, allowing you to connect your device to APRS software on your computer or smartphone (e.g., APRSdroid).

---

## How It Works

The software is designed to be plug-and-play. It automatically detects the type of Bluetooth supported by your hardware and activates the correct mode. You do not need to manually select between Bluetooth Classic and BLE.

-   **Device Name**: Your tracker will be discoverable with a Bluetooth name identical to the **callsign** you set in the configuration.
-   **Protocol**: The only supported TNC protocol is **KISS**. We do not support the TNC2 format, as we consider it to be an inferior and less reliable format for modern applications.

To use this feature, simply enable Bluetooth in the `Configuration` page and then pair your computer or smartphone with the device.

---

## Hardware Support and Bluetooth Types

The type of Bluetooth protocol used depends entirely on the ESP32 chip on your board. Below is a general guide to help you identify which Bluetooth type your device likely supports.

| Device / Chip                   | Supported Bluetooth Type   |
| :------------------------------ | :------------------------- |
| TTGO T-Beam (all versions)      | Bluetooth Classic          |
| Standard ESP32 (e.g., WROOM-32) | Bluetooth Classic          |
| Heltec LoRa boards              | BLE (Bluetooth Low Energy) |
| ESP32-C3                        | BLE (Bluetooth Low Energy) |
| ESP32-S3                        | BLE (Bluetooth Low Energy) |

In summary:

-   Most older, common ESP32 development boards, including all T-Beam variants, use **Bluetooth Classic**.
-   Newer generations of ESP32 chips (like the C3 and S3 series) and specialized boards like those from Heltec typically use **BLE**.
