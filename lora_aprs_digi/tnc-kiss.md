---
layout: digi
title: TNC (KISS / TNC2) Functionality
permalink: /lora_aprs_digi/tnc-kiss/
---

Our firmware includes a built-in Terminal Node Controller (TNC) that bridges the LoRa radio network with APRS applications running on your computer or smartphone. It turns your device into a modem that can send and receive APRS packets.

The TNC is available over **three independent interfaces**, and each interface can use one of **two framing modes**: **KISS** or **TNC2**. You enable the interfaces and choose their modes in the **"TNC Settings"** section of the web configuration panel.

➡️ For the configuration fields, see: [Configuration → TNC Settings](/lora_aprs_digi/configuration/#tnc-settings)

---

## Framing modes: KISS vs TNC2

Each interface can run in one of two modes. The mode determines how packets are encoded on the wire — it does **not** change which interface you connect to.

| | **KISS** | **TNC2** |
| --- | --- | --- |
| Frame format | AX.25 binary, SLIP-framed | Raw APRS text, terminated with `\n` |
| Callsign length | Max 6 characters (AX.25 strict) | Longer callsigns accepted |
| SSID | Numeric `0–15` only | Alphanumeric `-XX` SSIDs accepted |
| Validation | Strict — frames violating AX.25 are rejected | Lenient — passes raw text through |
| Best for | Standard KISS apps (APRSIS32, APRSDroid, etc.) | Tools that need long/alphanumeric callsigns or simple text framing |

**Key difference:** KISS follows AX.25 strictly, so any address longer than 6 characters or an SSID outside the numeric range `0–15` is rejected. TNC2 sends the raw APRS text frame and therefore accepts alphanumeric `-XX` SSIDs that KISS cannot represent.

> If you use **tactical callsigns** or any callsign with an alphanumeric SSID, you must use **TNC2** — KISS will reject those frames.

---

## Interfaces: which one, when

| Interface | Transport | Connection | Modes | Notes |
| --- | --- | --- | --- | --- |
| **TNC Server** | TCP/IP (Wi-Fi) | Port `8001`, up to 4 simultaneous clients | KISS / TNC2 | Most convenient; no cable needed |
| **USB Serial TNC** | USB serial | COM port @ `115200 bps` | KISS / TNC2 | Direct wired connection to your computer |
| **Hardware Serial TNC** | GPIO serial | Configurable RX/TX pins @ `115200 bps` | KISS / TNC2 | For wiring to external hardware/microcontrollers |

All three interfaces can be enabled at the same time, each with its own independent mode.

### TCP/IP TNC Server

When the device is connected to your Wi-Fi network, it can run a TNC server over TCP/IP. This lets you connect APRS software wirelessly over your local network.

-   **Port**: `8001`.
-   **Connections**: Up to 4 simultaneous clients.
-   **Mode**: KISS or TNC2.

This is the most convenient method for connecting modern applications without a physical cable.

### USB Serial TNC

The TNC can also be accessed via the device's USB serial port. When connected to your computer, the device appears as a COM port that your APRS software can open. This provides a direct, wired connection.

-   **Speed**: `115200 bps`.
-   **Mode**: KISS or TNC2.

### Hardware Serial TNC

A separate hardware (GPIO) serial port can also act as a TNC, intended for wiring the device directly to external hardware or another microcontroller.

-   **RX / TX pins**: Configurable in the TNC Settings.
-   **Speed**: `115200 bps`.
-   **Mode**: KISS or TNC2.

---

## Accept Own Frames

The **Accept Own Frames** option (in TNC Settings) makes the TNC also process packets sent by the device itself, instead of ignoring them. Useful when you want your APRS software to see everything the device transmits.

---

## Compatible Software

The TNC is compatible with a wide range of APRS software. Classic KISS applications like **APRSIS32** (Windows) or **APRSDroid** (Android) work with the **KISS** mode, but we highly recommend modern, web-based clients for the best experience.

### Recommended Applications

1.  **APRS TNC Web**

    -   A modern, browser-based TNC web server that runs on any device on your local network. It requires no installation—simply open the web page and connect to your device's IP address from within your local network.
    -   **Link**: [https://github.com/SQ2CPA/aprs-tnc-web](https://github.com/SQ2CPA/aprs-tnc-web)

2.  **LoRa APRS Mobile App**
    -   A dedicated Android App designed for a seamless mobile experience. It allows you to easily send and receive LoRa APRS messages, view packets on a map, and interact with the network directly from your smartphone.
    -   **Link**: [https://app.lora-aprs.pl](https://app.lora-aprs.pl)
