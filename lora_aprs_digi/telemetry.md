---
layout: digi
title: How Telemetry works
permalink: /lora_aprs_digi/telemetry/
---

Telemetry allows your station to send small pieces of diagnostic data to the APRS network. This data is crucial for monitoring the health and performance of your station and the network as a whole.

The firmware reports the following values:

-   **Received Frames**: Total packets heard by the station.
-   **Transmitted Frames**: Total packets sent by the station (including its own beacons).
-   **Digipeated Frames**: Packets that were successfully repeated by the station.
-   **Internal Voltage**: The voltage of the device's internal power source.
-   **External Voltage**: The voltage of an external power source, if connected.

---

## Mandatory for a Healthy Network

A key principle of this firmware is that **telemetry cannot be disabled**. This is a deliberate design choice made to benefit the entire network.

-   **Network Analysis**: The collected data (like the number of received vs. digipeated packets) is invaluable for analyzing network performance, identifying "deaf" stations, and understanding packet flow.
-   **Future Development**: This anonymous, non-personal data helps developers improve the firmware and the LoRa APRS network protocol itself.
-   **No Harm to the Network**: Telemetry does **not** send extra packets. The data is efficiently embedded within your station's standard position beacon. Because it doesn't consume any additional airtime, there is no technical reason for a user to disable it.

---

## How It Works

A core feature of our telemetry implementation is its efficiency.

-   **No Extra Packets**: Telemetry data does **not** generate separate, additional radio packets. Instead, all five diagnostic values are cleverly embedded within your standard position beacon.
-   **"Cost-Free" Data**: Because it piggybacks on your existing beacons, telemetry adds valuable diagnostic data to your station's track at no extra cost to radio channel airtime.

Enabling this feature provides an excellent way to monitor your station's operational status and power source, allowing you to see useful graphs of its performance on APRS websites.

---

## The Initial Setup Process

For telemetry values to be displayed correctly on websites like `aprs.fi`, the network needs to know what the data means (e.g., that a value represents "Digipeated Frames" or "Volts"). This is done by sending a few special configuration packets that define the parameters and units for your station.

-   Our firmware handles this automatically. **Approximately one minute after the device is powered on, it will transmit a series of configuration packets.** These packets tell the APRS network how to interpret the telemetry data from your callsign.

### A Note on Initial Display

It is possible that when you first start using your station, the telemetry data may not display correctly or at all on APRS mapping sites.

> **What does this mean?**
> This happens if the initial configuration packets were not successfully received by an APRS-IS IGate. If you are in a location with poor RF propagation to the nearest gate when your device starts up, these critical packets might get lost.
>
> **What should you do?** > **You can safely ignore this.** You don't need to do anything special. Simply continue to use the station as intended. The device sends these setup packets every time it boots. Over time, as you use the device, it will eventually be heard by an IGate at the right moment. Once the configuration packets are received, the telemetry will start displaying correctly on its own.
