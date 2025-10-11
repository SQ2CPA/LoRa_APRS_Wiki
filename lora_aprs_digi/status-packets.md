---
layout: digi
title: Status Packets
permalink: /lora_aprs_digi/status-packets/
---

In the APRS network, a status packet serves a specific, functional purpose. It is not meant to be an advertising banner or a static message. Its goal is to inform other stations about the current state, activity, or configuration of your device in real-time.

Our firmware uses status packets to announce key events, which can be helpful for remote diagnostics or simply understanding what the tracker is doing.

---

## Available Status Messages

Below is a list of the status packets that your station can automatically transmit, along with their meanings.

1.  **`System booted at 10:45:57Z Ws TX&RX 434.855MHz 1200bps`**

    -   **When it's sent**: Transmitted shortly after the device boots up.
    -   **Meaning**: This is an announcement that the tracker is online and operational. The packet is composed of several dynamic parts that provide useful information:
        -   **`at 10:45:57Z`**: The UTC time when the device booted. This is only included if the device has an active internet connection to synchronize its clock.
        -   **`Ws`**: A short code indicating the device's operational mode.
            -   **`W`** flags indicate the digipeater mode: `Ws` (self-digi, only repeats its own packets), `W1` (WIDE1 digi), `W2` (WIDE2 digi).
            -   **`WX`** flags indicate the weather station status: `WX` (WX module is enabled), `WX+` (WX sensor is connected and working), `WX-` (WX sensor was not detected).
        -   **`TX&RX`**: The radio state. This can be `TX&RX` (both transmitting and receiving are active), `TX` (transmit-only), or `RX` (receive-only).
        -   **`434.855MHz 1200bps`**: The current LoRa frequency and speed, which is very useful for other users in the area.

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

7.  **`Scheduled Reboot`**

    -   **When it's sent**: When the device performs an automatic, scheduled reboot (e.g., a daily restart configured by the user).
    -   **Meaning**: Notifies the network that the reboot was part of a routine maintenance schedule, distinguishing it from a manual reboot or an unexpected crash.

8.  **`Low battery - sleeping`**

    -   **When it's sent**: Only on devices that do **not** have an AXP power management chip. It's transmitted just before the device enters deep sleep due to low voltage.
    -   **Meaning**: This status serves as a "last gasp" message, informing the network that the device is shutting down temporarily to protect its battery until the voltage recovers (e.g., through solar charging).
