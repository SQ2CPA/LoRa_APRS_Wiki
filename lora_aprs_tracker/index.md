---
layout: tracker
title: Home
permalink: /lora_aprs_tracker/index/
---

> This documentation was last updated on 16 January 2025, and applies to firmware version **v1.0.5**.

**LoRa APRS Tracker** is a software solution designed with a strong focus on RF-based APRS communication at **1200 bps**. This project prioritizes reliable radio-frequency (RF) communication and **tracker** functionality, rather than acting as only tracker to send your position. If you're looking for an RF-centric solution tailored for LoRa APRS operations, this is the software for you.

- It's not just the different frequency that is significant here. The key distinction is the use of a 1200 bps data rate - emulating traditional packet radio speeds - on a frequency that operates outside the heavily regulated and often congested ISM band. This specific combination is what enables more robust and reliable RF performance, which is the core focus of this project

---

## How to Start

Getting your LoRa APRS Tracker running is easy. Follow these steps in order:

1.  **Check Supported Hardware**: Before you begin, make sure you have a compatible device.
    - **➡️ [See Supported Boards](/lora_aprs_tracker/supported-boards/)**

2.  **Installation**: First, you need to flash the firmware onto your device. Follow the detailed instructions on the installation page.
    - **➡️ [Go to Installation Guide](/lora_aprs_tracker/installation/)**

3.  **Configuration**: Once the firmware is installed, you'll need to configure your station's parameters, such as your callsign, WiFi, and LoRa settings.
    - **➡️ [Go to Configuration Guide](/lora_aprs_tracker/configuration/)**

4.  **Using Your Tracker**: Learn how to physically interact with your device and read information from the display.
    - **➡️ [Button Functions](/lora_aprs_tracker/button-functions/)** - How to use buttons on your specific device
    - **➡️ [Display Screens](/lora_aprs_tracker/display/)** - Understanding the information shown on your tracker
    - **➡️ [Menu System](/lora_aprs_tracker/menu/)** - Access device functions via the on-screen menu

5.  **Learn More**: After completing the basic setup, you can explore the rest of the wiki to understand advanced features like updating the firmware and more.

---

## Key Features

- **RF-Centric Design**: Dedicated to reliable APRS communication over RF.
- **Digipeater Focused**: Enhanced support for digipeater operations to ensure wide RF coverage.
- **1200 bps Operation**: Specifically optimized for fast RF operations.
- **LoRa Modulation**: Utilizing the robust LoRa technology for long-range and low-power communication.
- **Lightweight and Efficient**: Minimal resource usage for deployment on low-power systems.
- **Ultra Fast**: No packet drop due to unnecessary delays.

---

## Why RF-Focused?

While many LoRa APRS softwares are designed to work primarily as IGates, this project takes a core approach. It aims to enhance APRS performance **on the radio layer**, enabling better peer-to-peer communication and extending RF network coverage. The goal is to make LoRa APRS accessible and reliable without dependence on internet infrastructure.

This software is ultra fast compared to other solutions.
