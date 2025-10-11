---
layout: tracker
title: LoRa APRS Tracker Status Packets
permalink: /lora_aprs_tracker/status-packets/
---

In the APRS network, a status packet serves a specific, functional purpose. It is not meant to be an advertising banner or a static message. Its goal is to inform other stations about the current state, activity, or configuration of your device in real-time.

Our firmware uses status packets to announce key events, which can be helpful for remote diagnostics or simply understanding what the tracker is doing.

---

## Available Status Messages

Below is a list of the status packets that your tracker can automatically transmit, along with their meanings.

1.  **`Tracker started 434.855MHz 1200bps`**

    -   **When it's sent**: Transmitted shortly after the device boots up.
    -   **Meaning**: This is an announcement that the tracker is online and operational. It conveniently includes the LoRa frequency and speed (e.g., 1200bps) it is currently configured to use, which is very useful for other users in the area.

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
    -   **When it's sent**: Transmitted when the device is being turned off by the user. This applies only to devices without an AXP chip (i.e., other than T-Beams). See [Button Functions](/LoRa_APRS_Wiki/lora_aprs_tracker/button-functions/) for more information.
    -   **Meaning**: A notification that the device has been intentionally powered down by the user.
