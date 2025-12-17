---
layout: tracker
title: Display
permalink: /lora_aprs_tracker/display/
---

Almost every tracker is equipped with a display that provides real-time information about the device's status, GPS data, battery level, and network activity. The display automatically updates and can be configured to turn off after a specified period of inactivity to save power.

---

## Supported Display Types

The tracker supports two types of displays, depending on the hardware:

-   **OLED Displays (Monochrome)**

    -   **SSD1306** - 0.96" OLED display (default)
    -   **SH1106** - 1.3" OLED display

-   **TFT Display (Color)**
    -   Used in devices like the **Heltec Wireless Tracker**
    -   160x80 pixels with color support

The display type is automatically detected during initialization. For OLED displays, you must manually configure which driver to use in the settings.

---

## Display Layout

The display shows information in a structured layout with **6 lines** of text:

### **Line 0 (Header Line)**

This line is displayed with a **larger font size** and has a **colored background** (on TFT displays) or uses a bigger font (on OLED displays). It always shows:

-   **Your callsign** (e.g., `SQ2CPA`)

### **Lines 1-5 (Information Lines)**

These lines are displayed in a **smaller font** and show real-time status information:

1.  **Line 1: GPS Information**

    -   **Format:** `[Maidenhead] [Time] [Status]`
    -   **Example:** `KO02ab 12:34:56 3D`
    -   **Special case:** If GPS fails to acquire a fix, this line shows: `GPS FAILED - NO DATA!`

2.  **Line 2: Battery Status**

    -   Shows detailed battery information including voltage and charging status
    -   **Format:** `Batt > [voltage]V` and/or `Ext > [voltage]V` with optional `CHARGING` indicator
    -   **Example:** `Batt > 4.12V CHARGING` or `Batt > 3.95V Ext > 5.00V`

3.  **Line 3: WiFi Network Status**

    -   Displays the current WiFi connection status
    -   **Possible values:**
        -   `WiFi disabled` - WiFi module is turned off
        -   `WiFi connecting...` - Currently attempting to connect to a network
        -   `WiFi< [IP address]` - Connected to a WiFi network as a client (e.g., `WiFi< 192.168.1.100`)
        -   `WiFi AP > 192.168.4.1` - Operating in Access Point mode with IP 192.168.4.1
        -   `WiFi | unknown` - Status cannot be determined

4.  **Lines 4-5: Last Received Packet**

    -   Shows information about the last received APRS packet across two lines
    -   **Line 4 format:** `Last RX: [callsign]`
        -   **Default:** `Last RX: none`
        -   **Example:** `Last RX: SQ7PFS`
    -   **Line 5 format:** `RSSI [value] SNR [value]`
        -   Shows signal strength (RSSI) and Signal-to-Noise Ratio (SNR) of the received packet
        -   **Example:** `RSSI -85 SNR 8.5`

---

## Startup Animation

When the tracker boots up for the first time (not during a fast restart - like after settings save), it displays a welcome animation:

1.  **First Screen (1.5 seconds):**

    -   Shows `LoRa APRS` as the title
    -   Displays `SQ2CPA` (author's callsign)
    -   Shows the build date of the firmware

2.  **Second Screen (animated):**
    -   Shows `Welcome` message
    -   Animates your callsign character by character

After the animation, the display switches to the main information screen.

---

## Display Timeout Feature

The tracker supports an automatic display timeout to conserve power, especially useful for battery-powered operation:

-   **Configuration:** You can set a timeout period in seconds via the web interface
-   **Behavior:** After the specified period of inactivity, the display will turn off
-   **Wake-up:** Pressing the button will wake the display back up

This feature is particularly useful for devices using TFT displays, as the backlight consumes significant power.

---

## Menu System

When you enter the menu (double-press the button), the display changes to show the menu interface:

-   **Header:** Shows `MENU` in large text
-   **Menu items:** Listed with a `>` prefix for the currently selected option
-   **Navigation indicators:** `^` and `v` symbols show if there are more items above or below
-   **Maximum visible items:** Up to 4 menu items are shown at once (on most displays)

For detailed information about menu navigation, see the [Menu](/lora_aprs_tracker/menu/) page.

---

_For information about button functions and interactions with the display, see the [Button Functions](https://wiki.lora-aprs.pl/lora_aprs_tracker/button-functions/) page._
