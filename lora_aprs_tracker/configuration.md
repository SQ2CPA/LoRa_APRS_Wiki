---
layout: tracker
title: Configuration
permalink: /lora_aprs_tracker/configuration/
---

The device's configuration is managed through a web interface. You can access it in two ways:

-   **Access Point (AP) Mode**: When the device cannot connect to a saved WiFi network (or after a factory reset), it creates its own WiFi Access Point (AP). The SSID is your callsign (or `N0CALL-9` by default). Connect to this network and open `http://192.168.4.1` in your web browser.
-   **Station (STA) Mode**: When the device is connected to your local WiFi network, its IP address will be displayed on the screen. Enter this IP address into your web browser to access the configuration page.

---

## Navigation Bar

At the top of the page, you'll find the main navigation menu:

-   **Configuration**: The main page with all the settings described below.
-   **Received Packets**: A table showing the most recent LoRa packets received by the device.
-   **Update**: Page for updating the device's firmware.
-   **Backup**:
    -   **Create Backup**: Downloads a file with all your current settings.
    -   **Restore Config**: Allows you to upload a previously saved backup file to restore your settings.
-   **Device Reboot**: A link to safely restart the device.

---

## Configuration Sections

The settings are grouped into logical sections. After making changes, remember to click the **"Save Configuration"** button at the bottom of the page.

### Station Configuration

This section contains the basic identification settings for your station on the APRS network.

-   **Callsign**: Your amateur radio callsign, including the SSID (e.g., `SQ2CPA-9`). This is a required field.
-   **Symbol Overlay**: A single character that acts as an overlay on your symbol on APRS maps.
-   **Symbol Table**: The character that defines your station's symbol on APRS maps (e.g., `>` for a car).
-   **Beacon Comment**: The text that will be sent with your position beacon.
-   **Beacon Path**: The APRS path for your beacon (e.g., `WIDE1-1,WIDE2-1`).

### WiFi Settings

Here you can configure how the device connects to WiFi and how its own Access Point behaves.

-   **Connect to WiFi Network**:
    -   **SSID**: The name of the WiFi network you want the device to connect to.
    -   **Password**: The password for that WiFi network.
    -   **Connection Timeout**: How many seconds the device should try to connect before giving up.
    -   **Reconnect interval**: How many minutes the device should wait before trying to reconnect if the connection is lost.
-   **Access Point Settings**:
    -   **Auto AP Password**: The password for the device's own WiFi Access Point.
    -   **Disable Auto AP after (minutes)**: The time in minutes after which the device's Access Point will automatically turn off to save power. `0` means it will stay on indefinitely.

### LoRa RF Settings

Configure the radio parameters for LoRa communication. This section allows selecting preset transmission frequencies or defining custom parameters for the transmitter (TX) and receiver (RX).

-   **TX Frequency Selection**: Select one or more preset checkboxes to transmit beacons on specific frequencies with predefined speeds.
    -   `434.855 MHz (1200bps)`
    -   `433.775 MHz (300bps)`
    -   `439.9125 MHz (300bps)`
    -   **Custom (below)**: Check this to manually set the transmitter parameters in the fields below.
-   **Transmitter (TX) - Custom Settings**:
    -   **Custom Frequency (MHz)**: Manually define the frequency for sending LoRa packets if the "Custom" option is selected.
    -   **Custom Speed**: A dropdown list to select custom LoRa modulation parameters (Bandwidth, Coding Rate, Spreading Factor) which determine the transmission speed (bps).
    -   **Power (dBm)**: The transmission power of the radio module.
-   **Receiver (RX)**:
    -   **Frequency (MHz)**: The frequency for listening for LoRa packets.
    -   **Speed**: The LoRa speed setting for reception, which must match the transmitter settings of the stations you want to hear.

### Beacon Settings

Control how your position beacons are transmitted.

-   **Beacon Interval (seconds)**: How often the device sends its position beacon.
-   **Smart beacon**: Enables an algorithm that adjusts the beacon rate based on speed and direction changes. This is useful for mobile stations to report their position more frequently when turning or changing speed, and less frequently when stationary or moving in a straight line. Options are `Disabled`, `Car`, `Bike`, or `Runner`.
-   **Send Extra Info**: Allows you to include additional data in your position beacon. Options are `None`, `Course + Speed`, or `Altitude`.
-   **Send Beacon**: A button to manually trigger a single beacon transmission immediately.

    -   ➡️ You can read more about Smart Beacon vs Beacon Interval: [Understanding Smart Beacon](/lora_aprs_tracker/smart-beacon/)

### Digipeater Settings

Configure the device to act as a digital repeater (digipeater).

-   **Mode**:
    -   `Disabled`: The digipeater function is off.
    -   `Repeat only if own call is addressed`: The device will only repeat packets that are specifically addressed to its callsign.

<!-- ### Telemetry Settings

-   **Enable Telemetry**: Check this box to enable the transmission of telemetry data.

    -   ➡️ You can read more about Telemetry: [How Telemetry works](/lora_aprs_tracker/telemetry/) -->

### Voltage Monitoring

This section allows you to monitor and report the voltage of the internal battery and/or an external power source.

-   **Send Internal/External Voltage**: Check these boxes to include voltage readings in your beacons.
-   **Send Voltages As Telemetry**: If checked, voltage data will be sent as APRS telemetry packets (requires Telemetry to be enabled).
-   **External Voltage Pin**: The GPIO pin number where the external voltage source is connected.
-   **Voltage Divider R1 / R2 (Ω)**: The resistance values of your external voltage divider circuit.
-   **Internal/External Voltage Calibration**: These fields allow you to calibrate the voltage readings by mapping raw ADC input values (`Raw Input`) to actual measured voltage values (`Mapped Output`). This helps correct for inaccuracies in the ADC or voltage divider components.

### Power Configuration

Manage the device's power-saving features, especially for battery-powered operation.

-   **Cut-off Voltage (V)**: The battery voltage at which the device will power down to protect the battery. This is mainly for boards with an AXP power management chip (like the T-beam).
-   **Enable sleep on low voltage**: For boards without an AXP chip, checking this will put the device into a deep sleep mode at the cut-off voltage instead of shutting it down completely.

### Bluetooth Settings

-   **Enable Bluetooth**: Activates the Bluetooth module to provide a KISS TNC interface over Bluetooth (either Classic or BLE, depending on the hardware). The Bluetooth device name will be your callsign.

    -   ➡️ You can read more about Bluetooth: [Bluetooth](/lora_aprs_tracker/bluetooth/)

### TNC Settings

Configure the device to act as a Terminal Node Controller (TNC) using the KISS protocol.

-   **Enable TNC Server**: Enables a KISS TNC server over TCP/IP (WiFi).
-   **Enable Serial KISS**: Enables a KISS TNC over the device's serial (USB) port.
-   **Accept Own Frames**: If checked, the TNC will also process packets sent by the device itself.

### Web Settings

-   **Web Password**: Set a password to protect access to this web configuration interface. Leave it blank for no password.

### Display Settings

This new section allows you to manage the settings for the device's built-in display.

-   **Enable display**: Check this box to activate the display.
-   **Display timeout**: Specify the time in seconds after which the display will automatically turn off to save power. A value of `0` disables this feature, keeping the display on permanently.

### Advanced Settings

-   **CPU frequency**: Select the operating frequency for the device's processor. Options include `40 MHz`, `80 MHz`, `160 MHz`, and `240 MHz`.
-   **Admins callsigns (station operators)**: A comma-separated list of callsigns that have administrative privileges (e.g., for remote commands).
-   **Ignored callsigns (blacklist)**: A comma-separated list of callsigns from which packets should be ignored.
-   **Don't send blacklisted packets via TNC**: If checked, packets from blacklisted callsigns will not be forwarded to the TNC interfaces.
-   **Don't send initial telemetry frames**: If checked, the device will skip sending the initial telemetry setup frames (`PARM`, `UNIT`, `EQNS`) upon startup.
-   **GPS baudrate**: Allows you to override the default serial communication speed for an external GPS module. Select "Use board default" for most built-in modules.

### System Status & Last Received Packets

These last two sections are not for configuration but for displaying information:

-   **System Status**: Shows real-time metrics like CPU Speed, RAM Usage, Temperature, and WiFi Strength.
-   **Last Received Packets**: A table showing details of the most recent LoRa packets heard by the device, including timestamp, packet data, RSSI, SNR, and frequency error.
