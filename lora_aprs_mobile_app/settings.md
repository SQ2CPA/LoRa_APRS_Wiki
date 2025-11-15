---
layout: mobile_app
title: Settings Screen
permalink: /lora_aprs_mobile_app/settings/
---

The Settings screen allows you to configure all aspects of the app, from your station identification to connection protocols and UI preferences.

---

## Station Info

This section is for your primary station identification.

![Station Info Settings](/assets/images/lora_aprs_mobile_app/settings/station-info.jpg)

-   **Callsign**: Your amateur radio callsign, max. 6 characters length.
-   **SSID**: Your Secondary Station Identifier. This **must** be a valid number between 0 and 15.

---

## Connection Settings

Configure how the app connects to your TNC (LoRa APRS device). We currently support the KISS protocol over several transports.

![Connection Settings](/assets/images/lora_aprs_mobile_app/settings/connection-settings.jpg)

-   **Bluetooth Classic (BT)**: For standard Bluetooth devices. You must pair your device in your phone's system settings first. You can use the **Open System Bluetooth Settings** button to get there quickly.
-   **Bluetooth Low Energy (BLE)**: For modern, low-power devices.
-   **TCPIP**: For connecting to a device over Wi-Fi or a local network. The default port is `8001`.

---

## APRS Settings

These settings control APRS-specific behaviors, primarily related to messaging.

![APRS Settings](/assets/images/lora_aprs_mobile_app/settings/aprs-settings.jpg)

-   **Path**: The digipeater path to be used when sending messages (e.g., `WIDE1-1`, `WIDE2-1`, `WIDE1-1,WIDE2-1`).
-   **Max Retries**: The maximum number of times the app will try to re-send an unacknowledged message.
-   **Retry Interval**: The time (in seconds) the app will wait before retrying an unacknowledged message.

---

## Recent Stations Settings

This section customizes the 'Recent Stations' card on the Main Screen.

![Recent Stations Settings](/assets/images/lora_aprs_mobile_app/settings/recent-stations-settings.jpg)

-   **Distance Display**: Choose how to calculate the distance to a heard station:
    -   `Current`: Distance from your _current_ location to the station.
    -   `At Reception`: Distance from _where you were_ when you heard the station.
    -   `Both`: Show both distances.
-   **Auto-ping**: Automatically sends a ping to stations in your recent list to see if they are still reachable. This is very useful for testing two-way (TX/RX) connectivity, especially with beacons that may only transmit every 30 minutes, leaving you unsure if you are still in range. You can set this to `Off`, `5 min`, `10 min`, or `15 min`.
-   **Show last stations**: Filters the recent stations list to only show stations heard within a specific timeframe (`1h`, `3h`, `6h`, `24h`).

---

## Other Settings

General application preferences.

![Other Settings](/assets/images/lora_aprs_mobile_app/settings/other-settings.jpg)

-   **Auto Connect**: When enabled, the app will automatically try to connect to your last used device as soon as you open the app. This saves you from having to press the "Start" button every time.

---

## App Management & Utilities

At the bottom of the settings screen, you will find several important utilities.

![App Management Settings](/assets/images/lora_aprs_mobile_app/settings/app-management.jpg)

-   **Save Settings**: You must press this button to save any changes made on this screen.
-   **Debug Logs**: Tapping this allows you to save and export the app's internal logs. This is extremely useful for diagnosing problems. You may be asked to send this log file to the developer to help fix a bug.
-   **Allow working in background**: This button opens the `https://dontkillmyapp.com/` webpage. This external site provides instructions on how to adjust your specific Android phone's settings to prevent the system from "killing" (shutting down) the app when it's running in the background. **This step is required for the app to function correctly in the background.**
