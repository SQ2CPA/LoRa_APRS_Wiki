---
layout: general
title: Flashing Firmware
permalink: /general/flashing/
---

# Flashing Firmware

This page covers flashing LoRa APRS firmware on Digi/iGate/Tracker devices. The process is unified and looks the same for all software types.

For information about updating existing firmware, please refer to:

-   Tracker updates: [/lora_aprs_tracker/updating/](/lora_aprs_tracker/updating/)
-   Digi/iGate updates: [/lora_aprs_digi/updating/](/lora_aprs_digi/updating/)

## Flashing from Scratch (First Time)

When flashing a device for the first time or when you want to install firmware on a clean device, you have two options:

### 1. Flash via Web Browser (USB) - Preffered option

You can flash firmware directly from your browser using [https://flasher.lora-aprs.pl/](https://flasher.lora-aprs.pl/).

**⚠️ Important**: Flashing via the web page **always erases all settings**, so we recommend using this method only once - during initial flashing or when you want to reset the device to factory settings.

**Requirements**:

-   Good quality USB cable connected to the device
-   Browser with Web Serial API support (e.g., Chrome, Edge)

### 2. Flash from Binary File Using External Software - for Advanced Users

You can download the `.bin` file directly from the repository page: [https://firmware.sq2cpa.pl/](https://firmware.sq2cpa.pl/) and flash it using external tools (e.g., esptool, Flash Download Tool).

This method provides more control over the flashing process and is useful for advanced users.

---

## FAQ - Common Issues

### ❓ Flashing Gets Stuck at Some Step (e.g., "Preparing Installation")

**Solution**: Change the USB cable.

Unfortunately, poor quality cables may not work properly and can cause problems during flashing. Use a good quality cable with data transfer support (not just charging).

### ❓ No Communication with Device During Flashing

**Problem**: When flashing from [https://flasher.lora-aprs.pl/](https://flasher.lora-aprs.pl/), you get a message like "no communication with device" or the device is not detected.

**Solution**: The device is probably not in flashing mode (boot mode).

Some devices, such as **Heltec Wireless Tracker**, must be manually put into flashing mode:

1. **Press and hold** the **USER** button
2. **Press** the **RESET** button (while still holding USER)
3. **Release** the RESET button
4. **Release** the USER button

The device should now be in flashing mode. Try again.

---

**Happy flashing!**
