---
layout: mobile_app
title: Main Screen
permalink: /lora_aprs_mobile_app/main_screen/
---

The Main Screen is your central hub and command center. It provides an at-a-glance overview of your connection status, recent activity, and provides quick navigation to the app's core features.

![LoRa APRS App Main Screen](/assets/images/lora_aprs_mobile_app/main-screen.jpg)

---

## 1. Top Status & Navigation Bar

This bar at the top of the screen provides core status information and navigation.

-   **Settings (Gear Icon)**: Located on the far left, this button takes you to the app's **Settings** screen.
-   **Map (Map Icon)**: Located on the far right, this button opens the **Network Map** view.
-   **Center Status Display**: This is the main status area, which shows:
    -   **Callsign**: Your device's configured callsign (e.g., `SQ2CPA-9`).
    -   **Connection Status**: Shows the current connection type (`BT`, `BLE`, `TCPIP`) or `Offline` if not connected.
    -   **Last Locator**: Displays the last known grid square locator reported by your TNC.
    -   **Battery Voltage**: If supported by your device's firmware, it displays the current battery voltage.

## 2. Info Banner

A yellow informational banner is displayed on preview or beta versions, noting that the application is still in development and not all features may work as expected.

## 3. Messages Section

This card manages all your messaging functions.

-   **Messages List (Chat Icon)**: Tapping this button opens your full conversation list. If you have unread messages, a badge will appear on this icon indicating the count.
-   **New Message (Pencil Icon)**: This button opens a new, blank message screen, allowing you to compose and send a new message.

## 4. Activity Section

This card gives you a quick summary of your RF activity.

-   **Last Activity**: Displays when you last transmitted (`Tx`) and received (`Rx`) a frame, typically shown in "seconds ago" format.
-   **Frames (Button)**: This button on the right takes you to the **Raw Frames View**, where you can see a live log of all incoming and outgoing APRS packets.

## 5. Recent Stations Section

This card shows a list of APRS stations that your device has recently heard over RF. If no stations have been heard since the app was started, it will display "No stations heard yet."

## 6. Main Control Button (Bottom)

This is the primary action button for the app, located in a floating bar at the bottom of the screen.

-   **Start**: When the app is disconnected, this button (with a "Play" icon) will initiate the connection process to your selected LoRa APRS device.
-   **Stop**: Once connected, this button will change to a "Stop" button, allowing you to manually disconnect from the device.
