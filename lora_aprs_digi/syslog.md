---
layout: default
title: Syslog for Packet Analysis
permalink: /lora_aprs_digi/syslog/
---

## What is Syslog and Why Use It?

The Syslog feature allows your device to send detailed information about every LoRa packet it receives to a remote server over your WiFi connection. This is an incredibly powerful tool for network analysis and monitoring your station's performance.

A key feature of the APRS-IS network is **deduplication**. When multiple i-gates hear the same packet from a tracker and forward it to APRS-IS, the network ensures that only one copy is distributed globally. While this is excellent for the network's health, it means that as a station operator, you don't see every single packet your device hears on websites like `aprs.fi`.

Syslog solves this problem. It sends a log entry for **every single frame**, including those with errors (bad CRC) and duplicates, directly from your device to a logging server. This gives you a complete, unfiltered view of what your station is actually receiving over the air.

---

## How It Works

When enabled, the device sends small data packets using the UDP protocol to a specified server. Each packet contains the raw APRS frame along with valuable metadata like signal strength (RSSI), signal-to-noise ratio (SNR), and frequency error. This allows for in-depth analysis of link quality and station performance.

---

## Supported Syslog Modes

The firmware supports two primary public logging services, as well as the option to use your own custom server.

### 1. `log.lora-aprs.pl` (Recommended)

This is the **highly recommended** mode for logging.

-   **Method**: This service accepts raw log data. The device simply bundles the APRS packet with signal information and sends it. All the heavy lifting—parsing, interpreting, and displaying the data—is handled by the powerful server.
-   **Format**: The data is sent in a simple, efficient, comma-separated format:
    `TYPE,RSSI,SNR,FREQ_ERR,RAW_PACKET`
-   **Advantages**:
    -   ✅ **Extremely Lightweight**: This method uses very few ESP32 resources (CPU and memory), ensuring the device's main functions (digipeating, i-gating) are not impacted.
    -   ✅ **Raw Data Integrity**: The server receives the complete, unaltered APRS frame, which is perfect for debugging and detailed analysis.
    -   ✅ **Efficient**: It follows the best practice of offloading complex tasks from a constrained embedded device to a capable server.

### 2. `lora-aprs.live`

This mode is also available but is **not recommended** due to its architecture.

-   **Method**: This service requires the data to be pre-processed and formatted into a human-readable string _before_ it is sent. This means the ESP32 must parse every single packet, determine its type (Position, Message, Telemetry, etc.), and build a complex string.
-   **Disadvantages**:
    -   ❌ **High CPU Load on ESP32**: Parsing APRS packets is a resource-intensive task. Offloading this to every digipeater in the network is inefficient and can impact the performance and stability of the device.
    -   ❌ **Loss of Raw Data**: The server does not receive the original, raw APRS frame. It only gets the ESP32's interpretation of it. This prevents any deeper analysis or debugging of potentially malformed packets that the server could otherwise handle.

### 3. Custom Syslog Server

You can also provide the IP address and port for your own private Syslog server (e.g., a local Raspberry Pi running a Syslog daemon) for full control over your data.
