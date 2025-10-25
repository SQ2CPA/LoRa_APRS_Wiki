---
layout: mobile_app
title: Home
permalink: /lora_aprs_mobile_app/index/
---

> This documentation was last updated on 25 October 2025, and applies to app version **28.09.2025**.

**LoRa APRS App** is a mobile application for amateur radio operators, designed with a strong focus on **messaging and network monitoring**. Built by hams, for hams, this app prioritizes solid, reliable communication without the bloat. It does **not** send its own position beacons, acting as a dedicated interface for your LoRa APRS TNC but also works for AFSK VHF APRS.

If you're looking for a "set and forget" client that runs in the background, auto-connects to your devices, and just works for messaging, this is the app for you.

---

## Download & Installation

The app is currently in active development. You can download the latest version from the official download portal.

-   **Platform:** Android (Beta)
-   **Platform:** iOS (Coming Soon)

-   **➡️ [Download Latest Version at app.lora-aprs.pl/download](https://app.lora-aprs.pl/download)**

---

## How to Start

Getting your LoRa APRS App running is easy. Follow these steps in order:

1.  **Installation**: First, download and install the app from the link above.
2.  **Configuration**: Connect the app to your LoRa APRS device. The app supports Bluetooth (BLE & Classic) and TCP/IP (WiFi). Your device must support the **KISS TNC protocol**. Once connected, configure your station's parameters, such as your callsign and other preferences in the app settings.
3.  **Explore Features**: After setup, explore the app's features, like the messaging interface, station lists, and map view.

---

## Key Features

-   **Pure Messaging Focus**: No position beacons, no unnecessary features. Just solid, reliable APRS messaging.
-   **Set & Forget**: Runs in the background and automatically reconnects to your TNC.
-   **Flexible Connectivity**: Supports **Bluetooth (BLE & Classic)** and **TCP/IP over Wi-Fi** for connecting to your devices.
-   **KISS TNC Protocol**: Designed to work with any device that supports the standard KISS TNC protocol.
-   **Smart Station Lists**: Automatically filters for active, message-capable stations. Old stations are auto-cleaned from the list.
-   **Rich Station Data**: View detailed telemetry graphs, weather data, and raw packet info for any station.
-   **Network Map**: A visual map of all stations you are hearing to understand your local network coverage.

---

## Design Philosophy: A Messaging-First Client

While many APRS apps focus on tracking, this project takes a different approach. The core philosophy is simple: **a reliable messaging client that stays out of your way is more valuable than an app that tries to do everything.**

-   **Not a Tracker**: This app is **not** an APRS tracker. It will not send your phone's location. It is a client terminal for an external TNC.
-   **Clean & Simple**: The goal is to provide a clean, reliable interface for sending and receiving messages and monitoring the network. Operations are clear and easy to understand.
-   **Smart Integration**: The app is designed to work perfectly with **SQ2CPA's LoRa APRS firmware** (`flasher.sq2cpa.pl`), but it remains compatible with other standard KISS TNC devices.
-   **Background Reliability**: The app is built to run reliably in the background, ensuring you are always connected to the LoRa APRS network and ready to receive messages.
