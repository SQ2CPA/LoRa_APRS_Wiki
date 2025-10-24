---
layout: tracker
title: Menu
permalink: /lora_aprs_tracker/menu/
---

The tracker is equipped with a simple menu system that allows quick access to basic functions without needing to connect via the web interface. The menu is fully operated using the single button on the device.

---

## Navigation and Button Usage

The button's behavior depends on whether the menu is currently active.

### On the Main Screen (Menu is OFF)

-   **Double Press:** Enters the Menu.

### Inside the Menu (Menu is ON)

-   **Single Press:** Navigates to the next menu item (moves down the list).
-   **Long Press:** Selects (activates) the currently highlighted option and automatically exits the menu.
-   **Double Press:** Immediately exits the menu without selecting any option.

---

_For a general description of button functions (e.g., differences between devices), please see the [Button Functions](https://wiki.lora-aprs.pl/lora_aprs_tracker/button-functions/) page._

---

## Available Menu Options

Below is a list of the options available in the device menu.

1.  **`Send Beacon`**

    -   **Action:** Immediately transmits an APRS packet with the current position. This is the same function as a single press on the main screen.

2.  **`Turn OFF`**

    -   **Action:** Safely powers down the tracker. This is the same function as a long press on the main screen.

3.  **`WiFi AP ON`**

    -   **Action:** Starts the WiFi "Access Point" (AP) mode. This allows you to connect to the tracker (e.g., from your phone) and access the web configuration interface. If WiFi is already active, a message will be shown on the display.

4.  **`Bluetooth ON` / `Bluetooth OFF`**

    -   **Action:** Toggles the Bluetooth module (Classic or BLE, depending on the hardware) on or off. The label dynamically shows the action that will be performed (e.g., if Bluetooth is currently ON, the menu will show `Bluetooth OFF`). This setting is saved to the configuration and persists after a reboot.

5.  **`Exit Menu`**
    -   **Action:** Closes the menu and returns to the main screen without performing any action.
