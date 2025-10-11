There are two methods to install the firmware on your device. The recommended method is using our web flasher, as it is the easiest and most straightforward way. WiFi AP default password after flashing: `0123456789`. After flashing check `Configuration` page on wiki.

---

## Method 1: Web Flasher (Recommended)

This method allows you to flash the firmware directly from your web browser.

**Website:** [**flasher.sq2cpa.pl**](https://flasher.sq2cpa.pl)

### How to flash your device correctly?

1.  **Select your device type**.
2.  **Select your board**.
3.  **Select your firmware version** (if you want a version other than the latest).
4.  **Flash type** is only available as `First flash / Factory reset`. If you want to update your software, please check `Updating` page on wiki.
5.  Click **"Flash firmware"**.
6.  **Select your COM port**. Please double-check that you have selected the correct one.
7.  You can optionally wipe your device first, but this is not required for a standard flash.
8.  **Important:** Do not close the browser tab, switch to another tab, or move your device during the flashing process.
9.  After a successful flash, the device will create a WiFi Access Point with the SSID `N0CALL` and password `0123456789`.

> **Note:** You can't "brick" your device with this process. If flashing fails for any reason, simply verify your port selection and try again.

---

## Method 2: Manual Flashing with a .bin file

This method is for more advanced users who prefer to use their own flashing tool (e.g., ESPHome-Flasher). You will need to download the firmware binary file first.

1.  **Download the firmware file.**
    Go to the firmware repository: [**https://firmware.sq2cpa.pl/LoRa_APRS_Tracker/latest/**](https://firmware.sq2cpa.pl/LoRa_APRS_Tracker/latest/)
    Download the `web_factory.bin` file for your device.

2.  **Flash the file.**
    Use your preferred flashing tool to upload the downloaded `web_factory.bin` file to your device. Please consult the documentation for your specific flashing tool for instructions on how to do this.
