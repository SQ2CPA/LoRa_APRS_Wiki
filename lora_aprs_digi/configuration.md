---
layout: digi
title: Configuration
permalink: /lora_aprs_digi/configuration/
---

The device's configuration is managed through a web interface. You can access it in two ways:

- **Access Point (AP) Mode**: When the device cannot connect to a saved WiFi network (or after a factory reset), it creates its own WiFi Access Point (AP). The SSID is your callsign (or `N0CALL-10` by default). Connect to this network and open `http://192.168.4.1` in your web browser.
- **Station (STA) Mode**: When the device is connected to your local WiFi network, its IP address will be displayed on the screen. Enter this IP address into your web browser to access the configuration page.

---

## Navigation Bar

At the top of the page, you'll find the main navigation menu:

- **Configuration**: The main page with all the settings described below.
- **Received Packets**: A table showing the most recent LoRa packets received by the device.
- **Update**: Page for updating the device's firmware.
    - ➡️ Read more about the update process: [Firmware Update](/lora_aprs_digi/updating/)
- **Backup**:
    - **Create Backup**: Downloads a file with all your current settings.
    - **Restore Config**: Allows you to upload a previously saved backup file to restore your settings.
- **Device Reboot**: A link to safely restart the device.

---

## Configuration Sections

The settings are grouped into logical sections. After making changes, remember to click the **"Save Configuration"** button at the bottom of the page.

### Station Configuration

This section contains the basic identification settings for your station on the APRS network.

- **Callsign**: Your amateur radio callsign, including the SSID (e.g., `SQ2CPA-10`). This is a required field.
- **Symbol Overlay**: A single character that acts as an overlay on your symbol on APRS maps (e.g., `L` for LoRa).
- **Symbol Table**: The character that defines your station's symbol on APRS maps (e.g., `#` for a digipeater).
- **Beacon Comment**: The text that will be sent with your position beacon.
- **Beacon Path**: The APRS path for your beacon (e.g., `WIDE2-1`).
- **Latitude / Longitude**: The fixed geographical coordinates of your station. This is required for the station's position beacon.

### WiFi Settings

Here you can configure how the device connects to WiFi and how its own Access Point behaves.

- **Connect to WiFi Network**:
    - **SSID**: The name of the WiFi network you want the device to connect to.
    - **Password**: The password for that WiFi network.
    - **Initial WiFi client connection attempt (seconds)**: How many seconds the device tries to connect to your WiFi on startup. After this time, the device switches to the **AP+Client fallback** (it keeps its own Access Point running while continuing to retry the client connection).
    - **Retry interval after WiFi off (minutes)**: How often the device retries the client connection. Used only when the AP+Client fallback timeout has been reached. `0` = no retry.
- **Access Point Settings**:
    - **Auto AP Password**: The password for the device's own WiFi Access Point.
    - **Disable Auto AP after (minutes)**: The time in minutes after which the device's Access Point will automatically turn off to save power. `0` means it will stay on indefinitely.
    - **Disable AP+Client after (minutes)**: The time after which the AP+Client fallback mode is disabled. `0` = never disable. Useful for battery-powered stations during WiFi outages, so the device does not keep the AP running indefinitely.

### LoRa RF Settings

Configure the radio parameters for LoRa communication. The transmitter (TX) and receiver (RX) are configured independently.

➡️ The device will send status packets indicating which frequencies are in use. Learn more: [Status Packets](/lora_aprs_digi/status-packets/)

- **Transmitter (TX)**:
    - **Enable TX**: Check this to enable the transmitter module for sending beacons and digipeated packets.
    - **Frequency (MHz)**: The frequency for sending LoRa packets.
    - **Speed**: A dropdown to select the LoRa modulation parameters that determine the transmission speed:
        - `BW 125kHz CR 4:7 SF 9 (1200bps)`
        - `BW 125kHz CR 4:5 SF 12 (300bps)`
        - `Custom` — reveals the custom modulation selectors (see below).
    - **Power (dBm)**: The transmission power of the radio module.

        **Note:** The power value is passed directly (1:1) to the LoRa module without any modification or compensation for losses in the code. The actual output power depends on your hardware (antenna, connectors, cables, quality, etc.).

- **Receiver (RX)**:
    - **Enable RX**: Check this to enable the receiver module. This must be active for the digipeater function to work.
    - **Frequency (MHz)**: The frequency for listening for LoRa packets.
    - **Speed**: The LoRa speed setting for reception, with the same options as TX (`1200bps`, `300bps`, `Custom`). It must match the transmitter settings of the stations you want to hear.

- **Custom modulation**: When **Speed** is set to `Custom` (independently for TX and RX), three extra selectors appear, letting you set non-standard LoRa parameters:
    - **SF (Spreading Factor)**: `SF5` to `SF12`.
    - **CR (Coding Rate)**: `4:5`, `4:6`, `4:7`, `4:8`.
    - **BW (Bandwidth)**: `62.5 kHz`, `125 kHz`, `250 kHz`, `500 kHz`.

### Tactical callsigns

<div style="border: 3px solid #c0392b; background-color: #fdecea; color: #7b1f12; padding: 1rem 1.25rem; border-radius: 6px; margin: 1rem 0; font-weight: 600;">
⚠️ <strong>LEGAL WARNING — READ BEFORE ENABLING</strong><br><br>
Tactical callsigns are <strong>NOT legal in many countries</strong>. They are accepted in the USA, but are <strong>illegal in much of Europe</strong> and elsewhere. Enabling this option replaces your own source callsign on the air, which is forbidden under many national amateur radio regulations.<br><br>
<strong>It is your responsibility to verify that tactical callsigns are permitted by your local regulations before enabling this option.</strong>
</div>

- **Use tactical callsigns**: Enables the use of a tactical callsign.
- **Tactical callsign**: The tactical callsign to use. The base may use only letters A–Z (max 6 characters), with an optional alphanumeric SSID up to 2 characters.

If stations near you use tactical callsigns, enable this option. Leaving the tactical callsign field empty keeps your own source callsign unchanged. When both the option is enabled and a tactical callsign is entered, it becomes your source callsign for beacons, telemetry, digipeating, APRS-IS and messages. Your beacon will always end with `de <main callsign>`, and the beacon interval is limited to a maximum of 10 minutes.

### Beacon Settings

Control how your station's position beacon is transmitted.

- **Beacon Interval (min)**: How often (in minutes) the device sends its position beacon.
- **Send via RF**: Check this to send the beacon over the LoRa radio.
- **Send via APRS-IS**: Check this to send the beacon over the internet to the APRS-IS network (requires APRS-IS connection to be configured and active).
- **Send Beacon**: A button to manually trigger a single beacon transmission immediately.

### Digipeater Settings

Configure the device to act as a digital repeater (digipeater).

- **Digi mode**:
    - `Disabled`: The digipeater function is off.
    - `Repeat only if own call or alias is addressed`: The device will only repeat packets specifically addressed to its callsign (or to the TEMP PATH Alias below).
    - `Act as WIDE1 (fill-in) digi`: The device will act as a WIDE1-1 fill-in digipeater, repeating packets with `WIDE1-1` in their path.
    - `Act as combined WIDE1+WIDE2 digi`: The device will repeat both `WIDE1-1` (fill-in) and `WIDE2-x` packets.
    - `Act as WIDE2 digi (first unused address only)`: The device will act as a WIDE2-x digipeater, processing only the first unused address in the path.
- **TEMP PATH Alias**: An optional callsign alias recognized in the incoming path, e.g. `MOBILE`, `EVENT`. Packets addressed to this alias will be digipeated.
- **Keep path markers (`*`)**: When checked, previous `*` markers in the path are preserved instead of being stripped.

### Voltage Monitoring

This section allows you to monitor and report the voltage of the internal battery and/or an external power source.

- **Send Internal/External Voltage**: Check these boxes to include voltage readings in your beacons.
- **Send Voltage As Telemetry**: If checked, voltage data will be sent as APRS telemetry packets.
    - ➡️ Learn more about how telemetry works: [APRS Telemetry](/lora_aprs_digi/telemetry/)
- **External Voltage Pin**: The GPIO pin number where the external voltage source is connected.
- **Voltage Divider R1 / R2 (Ω)**: The resistance values of your external voltage divider circuit.
- **Internal/External Voltage Calibration**: These fields allow you to calibrate the voltage readings by mapping raw ADC input values (`Raw Input`) to actual measured voltage values (`Mapped Output`).

### Power Configuration

Manage the device's power-saving features.

- **Cut-off Voltage (V)**: The battery voltage at which the device will power down to protect the battery (mainly for boards with an AXP power management chip).
- **Enable sleep on low voltage**: For boards without an AXP chip, checking this will put the device into a deep sleep mode at the cut-off voltage.

### TNC Settings

Configure the device to act as a Terminal Node Controller (TNC). Three independent TNC interfaces are available, each with a selectable framing mode (KISS or TNC2).

➡️ For a detailed guide on using the TNC, see: [TNC (KISS Protocol)](/lora_aprs_digi/tnc-kiss/)

- **Enable TNC Server (port 8001)**: Enables a TNC server over TCP/IP (WiFi) on port `8001`.
    - **TNC Server mode**: `KISS` or `TNC2`.
- **Enable USB Serial TNC**: Enables a TNC over the device's USB serial port.
    - **USB Serial TNC mode**: `KISS` or `TNC2`.
- **Enable Hardware Serial TNC**: Enables a TNC over a hardware (GPIO) serial port.
    - **Hardware Serial TNC mode**: `KISS` or `TNC2`.
    - **Hardware Serial RX pin** / **TX pin**: The GPIO pins used for the hardware serial connection.
    - **Serial TNC speed**: Fixed at `115200 bps` (applies to both the USB Serial TNC and the Hardware Serial TNC).
- **Accept Own Frames**: If checked, the TNC will also process packets sent by the device itself.

**KISS vs TNC2:**

- **KISS** = AX.25 strict. Addresses longer than 6 characters and SSIDs outside the numeric range `0–15` are rejected.
- **TNC2** = raw APRS text frame terminated with `\n`. Unlike KISS, it accepts alphanumeric `-XX` SSIDs (KISS only accepts numeric `0–15`).

### APRS-IS Settings

Configure the device's connection to the global APRS Internet Service network.

- **Enable APRS-IS connection**: Check this to connect the device to an APRS-IS server.
- **Server**: The address and port of the APRS-IS server (e.g., `euro.aprs2.net:14580`).
- **Passcode**: Your APRS-IS passcode. Fill this in only if your passcode is different from the standard one calculated from your callsign.
- **Connection Status**: A live indicator showing whether the device is currently connected to the APRS-IS server.
- **Filter**: An APRS-IS filter string to limit the traffic received from the internet (e.g., `r/lat/lon/dist`).
- **Allow messages from APRSIS to RF**: If checked, packets received from APRS-IS that match the filter will be transmitted over LoRa (i-Gate functionality).

### WX Telemetry Settings

Enables the device to act as a weather station by sending telemetry data from a connected sensor.

➡️ For more details on supported sensors and data format, see: [Weather (WX) Telemetry](/lora_aprs_digi/wx-telemetry/)

- **Activate Wx Telemetry**: Enables this feature. Requires a compatible sensor (BME/BMP280, BME680 or Si7021) to be connected.
- **Height Correction (m)**: A value in meters to add to the sensor's altitude reading for calibration.
- **Temperature Correction (°C)**: A value in degrees Celsius to add to the sensor's temperature reading for calibration.

### Web Settings

- **Web Password**: Set a password to protect access to this web configuration interface. Leave it blank for no password.

### Syslog Settings

Configure the device to send logs to a remote syslog server for monitoring.

➡️ Learn how to set up and use syslog: [Syslog Monitoring](/lora_aprs_digi/syslog/)

- **Enable syslog**: Turns the feature on or off.
- **Mode**: Select a preset server:
    - `log.lora-aprs.pl`
    - `lora-aprs.live` — **Deprecated.** This endpoint may be removed or lose compatibility at any time.
- **Syslog server**: Manually enter the address and port of your own syslog server.

### Display Settings

Manage the settings for the device's built-in display.

- **Enable display**: Check this box to activate the display.
- **Display timeout**: Specify the time in seconds after which the display will automatically turn off to save power. A value of `0` disables this feature.
- **Rotate display 180°**: Check this to rotate the display output by 180 degrees, useful when the device is mounted upside down.

### Advanced Settings

- **CPU frequency**: Select the operating frequency for the device's processor.
- **Reboot Interval (hrs)**: Automatically reboot the device after a set number of hours. `0` disables this.
- **Low Power Mode**: An experimental mode to reduce power consumption, primarily for solar-powered (PV) digipeaters.
- **Ignored callsigns (blacklist)**: A comma-separated list of callsigns from which packets should be ignored.
- **Don't send blacklisted packets via TNC**: If checked, packets from blacklisted callsigns will not be forwarded to the TNC interfaces.
- **Admins callsigns (station operators)**: A comma-separated list of callsigns that have administrative privileges.
    - ➡️ Find out what administrative users can do: [Query Messages](/lora_aprs_digi/query-messages/)

### Metrics

This section displays real-time packet counters. These metrics are the same data that the device sends in its telemetry.

➡️ Learn more about how telemetry works: [APRS Telemetry](/lora_aprs_digi/telemetry/)

- **RX packets count**: Total number of packets received.
- **TX packets count**: Total number of packets transmitted by this device.
- **Repeated packets (Digi)**: Number of packets that have been digipeated.

---

### System Status

This section provides a live overview of the device's operational parameters.

- **CPU Speed**: Current operating frequency of the processor.
- **RAM usage**: How much RAM is currently in use.
- **Temperature**: The internal temperature of the main chip.
- **Radio RSSI**: This value shows the current background noise level of the LoRa radio, updated every few seconds. It does **not** represent the signal strength of the last received packet. Monitoring this value is useful for diagnosing issues with a high noise floor or local radio frequency (RF) interference.
- **WiFi Strength**: The signal strength of the connection to your WiFi network.

---

### Last Received Packets

This table displays the most recent LoRa packets heard by the device.

- The **Time** column shows Coordinated Universal Time (UTC) if available, or the time since the device was last started (uptime) otherwise.
- Packets may be prefixed with indicators:
    - `CRC>`: Indicates a packet received with a CRC error.
    - `INVALID>`: Indicates an invalid frame that is not supported (e.g., does not meet AX.25 protocol requirements).
