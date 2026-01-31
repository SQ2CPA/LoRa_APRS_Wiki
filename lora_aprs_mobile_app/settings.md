---
layout: mobile_app
title: Settings Screen
permalink: /lora_aprs_mobile_app/settings/
---

The Settings screen allows you to configure all aspects of the app, from your station identification to connection protocols and UI preferences.

---

## Station Info

This section is for your primary station identification.

<img src="/assets/images/lora_aprs_mobile_app/settings/station-info.jpg" alt="Station Info Settings" style="max-width: 300px; width: 100%;">

-   **Callsign**: Your amateur radio callsign, max. 6 characters length. This callsign is used as a user identifier and is **not** included in any transmitted frames. Its only purpose is to associate incoming messages with your station.

---

## Manage Devices

To add a device, tap the **Manage Devices** button visible in the settings screen. This will take you to the device management screen where you can add and configure all your devices.

For more details, see the [Multi-Device management page](/lora_aprs_mobile_app/multi-device/).

---

## APRS Settings

These settings control APRS-specific behaviors, primarily related to messaging.

<img src="/assets/images/lora_aprs_mobile_app/settings/aprs-settings.jpg" alt="APRS Settings" style="max-width: 300px; width: 100%;">

-   **Path**: The digipeater path to be used when sending messages (e.g., `WIDE1-1`, `WIDE2-1`, `WIDE1-1,WIDE2-1`).
-   **Max Retries**: The maximum number of times the app will try to re-send an unacknowledged message.
-   **Retry Interval**: The time (in seconds) the app will wait before retrying an unacknowledged message.

---

## Recent Stations Settings

This section customizes the 'Recent Stations' card on the Main Screen.

<img src="/assets/images/lora_aprs_mobile_app/settings/recent-stations-settings.jpg" alt="Recent Stations Settings" style="max-width: 300px; width: 100%;">

-   **Distance Display**: Choose how to calculate the distance to a heard station:
    -   `Current`: Distance from your _current_ location to the station.
    -   `At Reception`: Distance from _where you were_ when you heard the station.
    -   `Both`: Show both distances.
-   **Auto-ping**: Automatically sends a ping to stations in your recent list to see if they are still reachable. This is very useful for testing two-way (TX/RX) connectivity, especially with beacons that may only transmit every 30 minutes, leaving you unsure if you are still in range. You can set this to `Off`, `5 min`, `10 min`, or `15 min`.
-   **Show last stations**: Filters the recent stations list to only show stations heard within a specific timeframe (`1h`, `3h`, `6h`, `24h`).

---

## Other Settings

General application preferences.

<img src="/assets/images/lora_aprs_mobile_app/settings/other-settings.jpg" alt="Other Settings" style="max-width: 300px; width: 100%;">

-   **Auto Connect**: When enabled, the app will automatically try to connect to your last used device as soon as you open the app. This saves you from having to press the "Start" button every time.

---

## App Management & Utilities

At the bottom of the settings screen, you will find several important utilities.

<img src="/assets/images/lora_aprs_mobile_app/settings/app-management.jpg" alt="App Management Settings" style="max-width: 300px; width: 100%;">

-   **Save Settings**: You must press this button to save any changes made on this screen.
-   **Debug Logs**: Tapping this allows you to save and export the app's internal logs. This is extremely useful for diagnosing problems. You may be asked to send this log file to the developer to help fix a bug.
-   **Allow working in background**: This button opens the `https://dontkillmyapp.com/` webpage. This external site provides instructions on how to adjust your specific Android phone's settings to prevent the system from "killing" (shutting down) the app when it's running in the background. **This step is required for the app to function correctly in the background.**
-   **Factory Reset**: Clears all app data and restarts the application. Note that for a truly thorough cleanup, you should clear the app data from Android system settings (Settings → Apps → LoRa APRS → Storage → Clear Data).
