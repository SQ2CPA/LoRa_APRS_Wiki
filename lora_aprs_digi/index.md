---
layout: digi
title: Home
permalink: /lora_aprs_digi/index/
---

> This documentation was last updated on 11 October 2025, and applies to firmware version **v1.0.4**.

**LoRa APRS Digi/iGate** is a software solution designed with a strong focus on RF-based APRS network infrastructure at **434.855 MHz\*** at **1200 bps**. This project prioritizes reliable radio-frequency (RF) communication and its functionality as a high-performance **Digipeater** and **IGate**, rather than acting as a tracker sending its own position. If you're looking for a fast and efficient solution to build out the LoRa APRS network that respects APRS, this is the software for you.

-   It's not just the different frequency that is significant here. The key distinction is the use of a 1200 bps data rate—emulating traditional packet radio speeds—on a frequency that operates outside the heavily regulated and often congested ISM band. This specific combination is what enables more robust and reliable RF performance, which is the core focus of this project.

---

## How to Start

Getting your LoRa APRS Digi/IGate running is easy. Follow these steps in order:

1.  **Installation**: First, you need to flash the firmware onto your device. Follow the detailed instructions on the installation page.

-   **➡️ [Go to Installation Guide](/lora_aprs_digi/installation/)**

2.  **Configuration**: Once the firmware is installed, you'll need to configure your station's parameters, such as your callsign, WiFi, and LoRa settings.

-   **➡️ [Go to Configuration Guide](/lora_aprs_digi/configuration/)**

3.  **Learn More**: After completing the basic setup, you can explore the rest of the wiki to understand advanced features like updating the firmware and more.

---

## Key Features

-   **RF-Centric Design**: Dedicated to reliable APRS communication over radio.
-   **Digipeater Priority**: Repeating RF packets is always prioritized over sending them to the internet (IGate).
-   **Ultra-Fast**: No packet drops due to unnecessary delays. Speed is more important than showing info on a display.
-   **Clean RF Channel**: Status and telemetry frames are sent directly to APRS-IS to keep the radio frequency clear.
-   **Optimized for 434.855 MHz**: Specifically tailored for operation outside the noisy 70cm ISM band.
-   **Lightweight and Efficient**: Minimal resource usage for deployment on low-power systems.

---

## Design Philosophy: Speed and RF Reliability

While many APRS solutions focus on features, this project takes a different approach. The core philosophy is simple: **a fast station that doesn't drop packets is more valuable than a station with many features that can introduce delays.**

-   **RF is Priority**: If the station operates in Digi & IGate mode, repeating packets (Digipeating) is the absolute priority. Sending packets to APRS-IS is done afterward.
-   **No Compromise on Speed**: Operations that could slow down packet reception, like complex screen refreshes, are intentionally avoided. This ensures no packets are missed.
-   **No Dual Receive Support**: The software does not support receiving on two frequencies at once. Attempting to monitor multiple bands (especially with slow 300 bps frames) inevitably leads to packet loss. This design focuses on doing one thing perfectly.

The goal is to build and extend RF network coverage, making LoRa APRS accessible and reliable without dependence on internet infrastructure.
