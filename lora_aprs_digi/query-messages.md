---
layout: digi
title: Query Messages
permalink: /lora_aprs_digi/query-messages/
---

Our firmware supports a set of remote commands, known as query messages, that allow you to interact with your device by sending APRS messages. You can check the device's status, get metrics, or perform administrative actions like rebooting or initiating a firmware update.

To use these commands, send an APRS message to your device's callsign with the command in the message body. For example, to get the firmware version, send a message to your station callsign with the text `?APRSV`.

The system distinguishes between public commands, available to anyone, and administrative commands, which can only be executed by callsigns defined in the device's admin list.

---

## Public Commands

These commands can be sent by any station and are used for retrieving general status information.

1.  **`?APRS`** (or **`?`**, **`HELP`**)

    -   **Action**: Requests a list of available commands.
    -   **Response**: Returns a list of all public commands. If sent by an admin, it will also include the admin-only commands.

2.  **`?APRSV`**

    -   **Action**: Retrieves the firmware version and build information.
    -   **Response**: A string containing the project name, board type, version number, and build date. Example: `SQ2CPA LoRa APRS ESP32_V1 v1.0.0 2025-10-11`

3.  **`?APRSS`**

    -   **Action**: Checks the APRS-IS connection status.
    -   **Response**: Shows the APRS-IS server the device is currently connected to. Example: `Connected to poland.aprs2.net`

4.  **`?APRSUP`**

    -   **Action**: Gets the device's current uptime.
    -   **Response**: Returns the time in seconds since the last boot. Example: `Uptime: 86400`

5.  **`?APRSGV`**

    -   **Action**: Reads the internal and external voltage levels.
    -   **Response**: Provides the battery and external power supply voltage readings. Example: `Batt: 4.15V Ext: 5.02V`

6.  **`?APRSGM`**

    -   **Action**: Fetches the packet transmission and reception statistics.
    -   **Response**: Returns the count of transmitted (TX), received (RX), and digipeated packets. Example: `Metrics - TX: 120 RX: 450 Digi: 55`

7.  **`?APRSGR`**
    -   **Action**: Gets the RSSI (Received Signal Strength Indicator) of the last received LoRa packet.
    -   **Response**: Returns the RSSI value in dBm. Example: `Current RSSI: -89.50`

---

## Administrative Commands

These commands perform sensitive actions and can only be executed by callsigns listed in the device's admin configuration.

1.  **`?APRSR`**

    -   **Action**: Immediately reboots the device.
    -   **Note**: The device will not send a response; it will simply restart.

2.  **`?APRSSB`**

    -   **Action**: Forces the device to transmit a beacon packet as soon as possible.
    -   **Response**: `Beacon will be send in a while`

3.  **`?APRSU`**

    -   **Action**: Initiates a remote Over-The-Air (OTA) firmware update to the latest available version.
    -   **Response**: `Remote update started to latest`

4.  **`?APRSU <version>`**

    -   **Action**: Initiates a remote OTA firmware update to a specific version number.
    -   **Response**: `Remote update started to <version>` (e.g., `Remote update started to v1.2.3`)

5.  **`?APRSMR`**

    -   **Action**: Resets the packet counters (TX, RX, Digi) back to zero.
    -   **Response**: `Metrics reset complete`

6.  **`?APRSGA`**

    -   **Action**: Retrieves the device's local IP address on the Wi-Fi network.
    -   **Response**: The local IP address (e.g., `192.168.1.100`) or `Not connected` if not on Wi-Fi.

7.  **`?APRSAP`**

    -   **Action**: Manually enables the Wi-Fi Access Point (AP) mode. This is useful for reconfiguring the device if it cannot connect to a saved Wi-Fi network.
    -   **Response**: `AP started` or an error message if it cannot be enabled.

8.  **`?APRSELP`**

    -   **Action**: Forces the device to exit from low-power mode. This command is only available if the low-power mode is enabled in the configuration.
    -   **Response**: `Exited low power mode!`

9.  **`?APRSNET`**

    -   **Action**: Reloads the network connection. If the device is configured as a Wi-Fi client, it will attempt to reconnect. If it cannot connect or is configured as an Access Point, it will start the AP mode.
    -   **Response**: Confirmation of the network reload action.

10. **`?APRSTX ON`** / **`?APRSTX OFF`**

    -   **Action**: Enables or disables the LoRa transmitter.
    -   **Response**: Confirmation that LoRa TX has been turned on or off.
    -   **Note**: When TX is OFF, the device will not transmit any LoRa packets.

11. **`?APRSDIGI OFF`** / **`?APRSDIGI OWN`** / **`?APRSDIGI WIDE1`** / **`?APRSDIGI WIDE2`**
    -   **Action**: Sets the digipeater mode.
        -   `OFF` - Disables digipeating functionality.
        -   `OWN` - Digipeats only packets with the device's own callsign in the path.
        -   `WIDE1` - Digipeats packets with WIDE1-1 in the path.
        -   `WIDE2` - Digipeats packets with WIDE2-1, WIDE2-2, WIDE1-1 in the path.
    -   **Response**: Confirmation of the digi mode change.

---

## Radio Range Testing

The device supports automatic responses to PING messages for radio range testing purposes.

-   **Message**: `PING`
    -   **Action**: When a message with the content "PING" is received via radio (RF), the device automatically sends a response.
    -   **Response Path**: The response is sent with the `RFONLY` path, ensuring it is transmitted only via radio and not forwarded to APRS-IS.
    -   **Purpose**: This feature is used for testing radio coverage and signal reach.
    -   **Note**: This automatic response only works for messages received via radio (RF). Messages received from APRS-IS will not trigger this response.
