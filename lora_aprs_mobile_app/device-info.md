---
layout: mobile_app
title: Device Info
permalink: /lora_aprs_mobile_app/device-info/
---

The Device Info screen provides detailed information and remote-control actions for your connected TNC. You can access this screen by tapping on your callsign in the **Top Status bar** on the Main Screen.

<img src="/assets/images/lora_aprs_mobile_app/device-info/access-device-info.jpg" alt="Accessing Device Info" style="max-width: 300px; width: 100%;">

> **Firmware Requirement:** Please note that this functionality is **only available** for devices running the official `SQ2CPA` firmware, which can be obtained from [flasher.lora-aprs.pl](https://flasher.lora-aprs.pl). It will not work with other firmwares.

---

This screen provides information about your device, divided into the following sections:

## TNC Connection

This section shows the live status of your connection to the TNC.

<img src="/assets/images/lora_aprs_mobile_app/device-info/tnc-connection.jpg" alt="TNC Connection Info" style="max-width: 300px; width: 100%;">

-   **Connection Status**: Confirms that you are actively connected.
-   **Connection Type**: Shows the protocol being used (Classic, BLE, TCPIP).

---

## Device Details

This area pulls specific hardware and software information directly from your device.

<img src="/assets/images/lora_aprs_mobile_app/device-info/device-details.jpg" alt="Device Details Info" style="max-width: 300px; width: 100%;">

-   **Supported Software**: Confirms if the app recognizes this as a supported `SQ2CPA` firmware.
-   **Board**: The exact environment name of your hardware (e.g., `heltec_v3`, `t-beam`).
-   **Software Version**: The current firmware version installed on the device.
-   **Background RSSI**: Shows the current background RF noise level on the frequency. This is very useful for checking for QRM (Interference). It includes a **Refresh** button to take a new reading.
-   **New Version Available**: The app will check and inform you if a newer firmware version is available from the flasher.

---

## Actions

This section provides remote-control actions for your TNC.

<img src="/assets/images/lora_aprs_mobile_app/device-info/device-actions.jpg" alt="Device Actions" style="max-width: 300px; width: 100%;">

-   **Enable WiFi AP**: Allows you to remotely turn on the device's WiFi Access Point (AP) mode.
-   **Reload WiFi**: A button to restart the WiFi module on the TNC (e.g., if it was disabled and you want to re-enable it without a full reboot).
