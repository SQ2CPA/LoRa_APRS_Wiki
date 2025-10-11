---
layout: digi
title: Configuration (Digipeater)
permalink: /lora_aprs_digi/configuration/
---

The device's configuration is managed through a web interface. You can access it in two ways:

-   **Access Point (AP) Mode**: When the device cannot connect to a saved WiFi network (or after a factory reset), it creates its own WiFi Access Point (AP). The SSID is your callsign (or `N0CALL` by default). Connect to this network and open `http://192.168.4.1` in your web browser.
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

-   **Callsign**: Your amateur radio callsign, including the SSID (e.g., `SQ2CPA-10`). This is a required field.
-   **Symbol Overlay**: A single character that acts as an overlay on your symbol on APRS maps (e.g., `L` for LoRa).
-   **Symbol Table**: The character that defines your station's symbol on APRS maps (e.g., `#` for a digipeater).
-   **Beacon Comment**: The text that will be sent with your position beacon.
-   **Beacon Path**: The APRS path for your beacon (e.g., `WIDE2-1`).
-   **Latitude / Longitude**: The fixed geographical coordinates of your station. This is required for the station's position beacon.

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

Configure the radio parameters for LoRa communication.

-   **Transmitter (TX)**:
    -   **Enable TX**: Check this to enable the transmitter module for sending beacons.
    -   **Frequency (MHz)**: The frequency for sending LoRa packets.
    -   **Speed**: A dropdown list to select LoRa modulation parameters which determine the transmission speed (bps).
    -   **Power (dBm)**: The transmission power of the radio module.
-   **Receiver (RX)**:
    -   **Enable RX**: Check this to enable the receiver module. This must be active for the digipeater function to work.
    -   **Frequency (MHz)**: The frequency for listening for LoRa packets.
    -   **Speed**: The LoRa speed setting for reception, which must match the transmitter settings of the stations you want to hear.

### Beacon Settings

Control how your station's position beacon is transmitted.

-   **Beacon Interval (min)**: How often (in minutes) the device sends its position beacon.
-   **Send via RF**: Check this to send the beacon over the LoRa radio.
-   **Send via APRS-IS**: Check this to send the beacon over the internet to the APRS-IS network (requires APRS-IS connection to be configured and active).
-   **Send Beacon**: A button to manually trigger a single beacon transmission immediately.

### Digipeater Settings

Configure the device to act as a digital repeater (digipeater).

-   **Mode**:
    -   `Disabled`: The digipeater function is off.
    -   `Repeat only if own call is addressed`: The device will only repeat packets that are specifically addressed to its callsign.
    -   `Act as WIDE1 (fill-in) digi`: The device will act as a WIDE1-1 fill-in digipeater, repeating packets with `WIDE1-1` in their path.
    -   `Act as WIDE2 digi`: The device will act as a WIDE2-x digipeater. Will also repeat `WIDE1-1` packets.

### Voltage Monitoring

This section allows you to monitor and report the voltage of the internal battery and/or an external power source.

-   **Send Internal/External Voltage**: Check these boxes to include voltage readings in your beacons.
-   **Send Voltage As Telemetry**: If checked, voltage data will be sent as APRS telemetry packets.
-   **External Voltage Pin**: The GPIO pin number where the external voltage source is connected.
-   **Voltage Divider R1 / R2 (Ω)**: The resistance values of your external voltage divider circuit.
-   **Internal/External Voltage Calibration**: These fields allow you to calibrate the voltage readings by mapping raw ADC input values (`Raw Input`) to actual measured voltage values (`Mapped Output`).

### Power Configuration

Manage the device's power-saving features.

-   **Cut-off Voltage (V)**: The battery voltage at which the device will power down to protect the battery (mainly for boards with an AXP power management chip).
-   **Enable sleep on low voltage**: For boards without an AXP chip, checking this will put the device into a deep sleep mode at the cut-off voltage.

### TNC Settings

Configure the device to act as a Terminal Node Controller (TNC) using the KISS protocol.

-   **Enable TNC Server**: Enables a KISS TNC server over TCP/IP (WiFi).
-   **Enable Serial KISS**: Enables a KISS TNC over the device's serial (USB) port.
-   **Accept Own Frames**: If checked, the TNC will also process packets sent by the device itself.

### APRS-IS Settings

Configure the device's connection to the global APRS Internet Service network.

-   **Enable APRS-IS connection**: Check this to connect the device to an APRS-IS server.
-   **Server**: The address and port of the APRS-IS server (e.g., `euro.aprs2.net:14580`).
-   **Passcode**: Your APRS-IS passcode. A **"Generate"** button is available to calculate it from your callsign.
-   **Filter**: An APRS-IS filter string to limit the traffic received from the internet (e.g., `r/lat/lon/dist`).
-   **Allow messages from APRSIS to RF**: If checked, packets received from APRS-IS that match the filter will be transmitted over LoRa (i-Gate functionality).

### WX Telemetry Settings

Enables the device to act as a weather station by sending telemetry data from a connected sensor.

-   **Activate Wx Telemetry**: Enables this feature. Requires a compatible sensor (e.g., BME280, SHT31) to be connected.
-   **Height Correction (m)**: A value in meters to add to the sensor's altitude reading for calibration.
-   **Temperature Correction (°C)**: A value in degrees Celsius to add to the sensor's temperature reading for calibration.

### Web Settings

-   **Web Password**: Set a password to protect access to this web configuration interface. Leave it blank for no password.

### Syslog Settings

Configure the device to send logs to a remote syslog server for monitoring.

-   **Enable syslog**: Turns the feature on or off.
-   **Mode**: Select a preset server from the list.
-   **Syslog server**: Manually enter the address and port of your own syslog server.

### Display Settings

Manage the settings for the device's built-in display.

-   **Enable display**: Check this box to activate the display.
-   **Display timeout**: Specify the time in seconds after which the display will automatically turn off to save power. A value of `0` disables this feature.

### Advanced Settings

-   **CPU frequency**: Select the operating frequency for the device's processor.
-   **Reboot Interval (hrs)**: Automatically reboot the device after a set number of hours. `0` disables this.
-   **Low Power Mode**: An experimental mode to reduce power consumption, primarily for solar-powered (PV) digipeaters.
-   **Ignored callsigns (blacklist)**: A comma-separated list of callsigns from which packets should be ignored.
-   **Don't send blacklisted packets via TNC**: If checked, packets from blacklisted callsigns will not be forwarded to the TNC interfaces.
-   **Admins callsigns (station operators)**: A comma-separated list of callsigns that have administrative privileges.

### Metrics, System Status & Last Received Packets

These final sections are for display only and show real-time information about the device's operation.

-   **Metrics**: Shows packet counters for received (RX), transmitted (TX), and digipeated packets.
-   **System Status**: Displays CPU speed, RAM usage, temperature, radio signal strength (RSSI), and WiFi signal strength.
-   **Last Received Packets**: A table showing details of the most recent LoRa packets heard by the device.
