Telemetry allows your tracker to send small pieces of data, like sensor readings, to the APRS network. In this firmware, it's primarily used to report the device's battery and external voltage.

---

## How It Works

A key feature of our telemetry implementation is its efficiency.

-   **No Extra Packets**: Telemetry data does **not** generate separate, additional radio packets. Instead, the voltage information is cleverly embedded within your standard position beacon.
-   **"Cost-Free" Data**: Because it piggybacks on your existing beacons, enabling telemetry adds valuable data to your track at no extra cost to radio channel airtime.

Enabling this feature is highly recommended. It provides an excellent way to monitor your device's power source, allowing you to see beautiful graphs of its performance on APRS websites. This helps you understand how your battery behaves under different conditions and realistically estimate how long your tracker will operate in the field.

---

## The Initial Setup Process

For telemetry values to be displayed correctly on websites like `aprs.fi`, they need to know what the data means (e.g., that "125" actually means "4.1V"). This is done by sending a few special configuration packets that define the parameters and units for your station.

-   Our firmware handles this automatically. **Approximately one minute after the device is powered on, it will transmit three configuration packets.** These packets tell the APRS network how to interpret the telemetry data from your callsign.

### A Note on Initial Display

It is possible that when you first start using your tracker, the telemetry data may not display correctly or at all on APRS mapping sites.

> **What does this mean?**
> This happens if the three initial configuration packets were not successfully received by an APRS-IS IGate. If you are in a location with poor RF propagation to the nearest gate when your device starts up, these critical packets might get lost.
>
> **What should you do?** > **You can safely ignore this.** You don't need to do anything special. Simply continue to use the tracker as intended. The device sends these setup packets every time it boots. Over time, as you use the tracker in different locations, it will eventually be heard by an IGate at the right moment. Once the configuration packets are received, the telemetry will start displaying correctly on its own.
