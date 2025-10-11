There are several ways to update your device to the latest firmware. The recommended methods are **Manual OTA** or **Remote OTA**, as they preserve your device's settings.

---

## Method 1: Via Web Flasher (Erases Settings)

This method is identical to a first-time installation and will **erase all your current settings**. It is generally not recommended for a simple update unless you are trying to resolve a problem or perform a factory reset.

**⚠️ Important:** If you choose this method, you must first create a backup of your settings via the device's web interface. After flashing, you will need to restore this backup file to recover your configuration.

1.  Go to [**flasher.sq2cpa.pl**](https://flasher.sq2cpa.pl).
2.  Follow the same steps as for the initial installation.
3.  After the flash is complete, connect to the device, access the web interface, and use the "Restore" function to upload your backed-up settings file.

---

## Method 2: Manual OTA Update (Offline)

This is a recommended method for updating as it keeps all your settings intact. It does not require the device to be connected to the internet, but you will need to download the update file to your computer first.

1.  **Download the update file.**

    -   Go to the firmware repository: [**https://firmware.sq2cpa.pl/LoRa_APRS_Tracker/latest/**](https://firmware.sq2cpa.pl/LoRa_APRS_Tracker/latest/)
    -   Download the `ota_update.bin` file.

2.  **Upload the file to the device.**
    -   Connect to your device's web interface.
    -   Navigate to the **"Update"** section.
    -   Choose the `ota_update.bin` file you just downloaded.
    -   Start the update process and wait for it to complete. The device will reboot automatically.

---

## Method 3: Remote OTA Update (Online)

This is the easiest method if your device is connected to a WiFi network with internet access. It allows the device to download and install the latest firmware directly from the internet.

1.  **Ensure your device has an internet connection.**

    -   In the web interface, connect the device to a WiFi network that has internet access.

2.  **Start the remote update.**
    -   Navigate to the **"Update"** section in the web interface.
    -   You should see a list of available firmware versions.
    -   Select the version you wish to install (usually the latest one).
    -   Click the update button to begin the remote OTA process.
    -   The device will download the firmware, install it, and reboot automatically. Do not unplug the device during this process.
