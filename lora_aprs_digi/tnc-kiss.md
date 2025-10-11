---
layout: digi
title: TNC (KISS) Functionality
permalink: /lora_aprs_digi/tnc-kiss/
---

Our firmware includes a built-in Terminal Node Controller (TNC) that uses the standard KISS protocol. This feature turns your device into a modem, allowing it to act as a bridge between the LoRa radio network and APRS applications running on your computer or smartphone.

You can connect to the TNC through two primary interfaces: **TCP/IP** (over your local Wi-Fi network) or the physical **Serial/USB** port. Both interfaces allow you to send and receive APRS packets using any KISS-compatible software.

This functionality can be enabled or disabled in the "TNC Settings" section of the web configuration panel.

---

## TCP/IP KISS Server

When the device is connected to your Wi-Fi network, it can run a KISS TNC server. This allows you to connect APRS software to it wirelessly over your local network.

-   **Port**: The server runs on port `8001`.
-   **Connections**: It supports up to 4 simultaneous client connections.

This is the most convenient method for connecting modern applications without needing a physical cable.

---

## Serial KISS Interface

For a more traditional setup, the TNC can also be accessed via the device's USB serial port. When you connect the device to your computer, it will appear as a COM port that you can connect to with your APRS software. This method provides a direct, wired connection to the TNC.

---

## Compatible Software

The TNC is compatible with a wide range of APRS software that supports the KISS protocol. While classic applications like **APRSIS32** (Windows) or **APRSDroid** (Android) will work, we highly recommend using modern, web-based clients for the best experience.

### Recommended Applications

1.  **APRS TNC Web**

    -   A modern, browser-based TNC web server that runs on any device on your local network. It requires no installation—simply open the web page and connect to your device's IP address from within your local network.
    -   **Link**: [https://github.com/SQ2CPA/aprs-tnc-web](https://github.com/SQ2CPA/aprs-tnc-web)

2.  **LoRa APRS Mobile App**
    -   A dedicated Android App designed for a seamless mobile experience. It allows you to easily send and receive LoRa APRS messages, view packets on a map, and interact with the network directly from your smartphone.
    -   **Link**: [https://app.lora-aprs.pl](https://app.lora-aprs.pl)
