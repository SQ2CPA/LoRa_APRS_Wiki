---
layout: tracker
title: Query Messages
permalink: /lora_aprs_tracker/query-messages/
---

Our firmware supports a set of remote commands, known as query messages, that allow you to interact with your tracker by sending APRS messages. You can check the device's status, read sensor values, get its GPS position, or perform administrative actions like rebooting or forcing a beacon.

To use these commands, send an APRS message to your tracker's callsign with the command in the message body. For example, to get the firmware version, send a message to your station callsign with the text `?APRSV`.

The system distinguishes between public commands, available to anyone, and administrative commands, which can only be executed by callsigns defined in the device's admin list.

---

## Public Commands

These commands can be sent by any station and are used for retrieving general status information.

1.  **`?APRS`** (or **`?`**, **`?APRS?`**, **`H`**, **`HELP`**, **`?HELP`**)

    -   **Action**: Requests a list of available commands.
    -   **Response**: Returns a list of all public commands. If sent by an admin, it will also include the admin-only commands.

2.  **`?APRSV`**

    -   **Action**: Retrieves the firmware version and build information.
    -   **Response**: A string containing the project name, board type, version number, and build date. Example: `SQ2CPA LoRa APRS Tracker ESP32_V1 v1.0.0 2025-10-11`

3.  **`?APRSGV`**

    -   **Action**: Reads the internal and external voltage levels.
    -   **Response**: Provides the battery and external power supply voltage readings. Example: `Batt: 4.15V Ext: 5.02V`

4.  **`?APRSGR`**

    -   **Action**: Gets the RSSI (Received Signal Strength Indicator) of the last received LoRa packet.
    -   **Response**: Returns the RSSI value in dBm. Example: `Current RSSI: -89.50`

5.  **`?APRSL`**
    -   **Action**: Gets the tracker's current GPS location.
    -   **Response**: Returns the Maidenhead locator, latitude, longitude, altitude, speed, and direction. Example: `JO94 lat 52.40000 lng 16.90000 alt 85m spd 0km/h dir 0`. If the GPS has no fix, the response is `GPS no fix`.

---

## Administrative Commands

These commands perform sensitive actions and can only be executed by callsigns listed in the device's admin configuration.

1.  **`?APRSGA`**

    -   **Action**: Retrieves the device's local IP address on the Wi-Fi network.
    -   **Response**: The local IP address (e.g., `192.168.1.100`) or `Not connected` if not on Wi-Fi.

2.  **`?APRSAP`**

    -   **Action**: Manually enables the Wi-Fi Access Point (AP) mode. This is useful for reconfiguring the device if it cannot connect to a saved Wi-Fi network.
    -   **Response**: `AP started`

3.  **`?APRSNET`**

    -   **Action**: Reloads the network connection. If the device is configured as a Wi-Fi client, it will attempt to reconnect. If it cannot connect or is configured as an Access Point, it will start the AP mode.
    -   **Response**: `WiFi reloading started`

4.  **`?APRSR`**

    -   **Action**: Immediately reboots the device.
    -   **Note**: The device will not send a response; it will simply restart.

5.  **`?APRSSB`**

    -   **Action**: Forces the device to transmit a beacon packet as soon as possible.
    -   **Response**: `Beacon will be send in a while`
