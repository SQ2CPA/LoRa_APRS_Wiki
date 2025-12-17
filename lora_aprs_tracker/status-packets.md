---
layout: tracker
title: Status Packets
permalink: /lora_aprs_tracker/status-packets/
---

In the APRS network, a status packet serves a specific, functional purpose. It is not meant to be an advertising banner or a static message. Its goal is to inform other stations about the current state, activity, or configuration of your device in real-time.

Our firmware uses status packets to announce key events, which can be helpful for remote diagnostics or simply understanding what the tracker is doing.

---

## Available Status Messages

Below is a list of the status packets that your tracker can automatically transmit, along with their meanings.

1.  **`Tracker started`** (with additional information)

    -   **When it's sent**: Transmitted shortly after the device boots up.
    -   **Meaning**: This is an announcement that the tracker is online and operational. The message includes additional information about the current configuration, which is very useful for other users in the area.

    **Understanding the status suffix:**

    The tracker appends configuration details after "Tracker started" to inform others about its operating mode:

    **Geofence Mode (AUTO):**
    -   **`Tracker started AUTO NOFIX`** - Geofence is enabled, but GPS hasn't determined the region yet
    -   **`Tracker started AUTO PL`** - Geofence detected Poland region (uses 434.855 MHz)
    -   **`Tracker started AUTO EU`** - Geofence detected Europe region (uses 433.775 MHz)
    -   **`Tracker started AUTO UK`** - Geofence detected UK region (uses 439.9125 MHz)

    **Manual Mode:**

    When geofence is disabled, the status shows which frequency presets are enabled for **transmission (TX)**:
    -   **PL** - Polish preset (434.855 MHz, 1200 bps)
    -   **EU** - European preset (433.775 MHz, 1200 bps)
    -   **UK** - UK preset (439.9125 MHz, 1200 bps)

    Multiple presets can be active simultaneously, e.g., **`Tracker started PL EU`**

    If you've configured a custom TX frequency/speed that doesn't match any preset, it will be shown explicitly:
    -   **`Tracker started 432.500MHz 300bps`** - Custom TX frequency and speed

    **Receive (RX) Configuration:**

    If your receiver (RX) uses different settings than the transmitter (TX), the status will additionally show **`RX`** followed by the receive frequency and speed:
    -   **`Tracker started PL RX 433.775MHz 1200bps`** - Transmitting on PL preset, but listening on EU frequency
    -   **`Tracker started 434.855MHz 1200bps RX 433.775MHz 300bps`** - Custom TX and different RX settings

    This is particularly useful when you want to transmit on one frequency but monitor traffic on another.

2.  **`Remote update / Remote update (query)`**

    -   **When it's sent**: At the beginning of a remote firmware update process initiated via the web interface.
    -   **Meaning**: Informs the network that the device is attempting to download and install a new firmware version from the internet.

3.  **`Remote update failed`**

    -   **When it's sent**: If the remote OTA update process fails for any reason (e.g., download error, invalid file).
    -   **Meaning**: Indicates that the firmware update was not successful.

4.  **`Local update started`**

    -   **When it's sent**: When you start a manual update by uploading a `.bin` file through the web interface.
    -   **Meaning**: The device has begun the process of a local firmware update.

5.  **`Local update finished`**

    -   **When it's sent**: After a local firmware update has been successfully completed and the device is about to reboot.
    -   **Meaning**: Confirms that the manual update was successful.

6.  **`User reboot`**

    -   **When it's sent**: When the "Device Reboot" button is clicked in the web interface.
    -   **Meaning**: A simple notification that the device was intentionally rebooted by the user.

7.  **`Low battery - sleeping`**

    -   **When it's sent**: Only on devices that do **not** have an AXP power management chip. It's transmitted just before the device enters deep sleep due to low voltage.
    -   **Meaning**: This status serves as a "last gasp" message, informing the network that the device is shutting down temporarily to protect its battery until the voltage recovers (e.g., through solar charging).

8.  **`Turned off`**
    -   **When it's sent**: Transmitted when the device is being turned off by the user. This applies only to devices without an AXP chip (i.e., other than T-Beams). See [Button Functions](/lora_aprs_tracker/button-functions/) for more information.
    -   **Meaning**: A notification that the device has been intentionally powered down by the user.
