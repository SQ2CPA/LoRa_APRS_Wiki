---
layout: digi
title: Weather (WX) Telemetry
permalink: /lora_aprs_digi/wx-telemetry/
---

Our firmware can function as a simple APRS weather station (WX) by connecting a compatible external sensor via the I2C interface. When this feature is enabled, the device will periodically transmit weather data that can be viewed on APRS mapping services like `aprs.fi`.

The firmware automatically detects the connected sensor upon startup.

---

## Supported Sensors

The device is compatible with a range of popular environmental sensors. Depending on the sensor used, different types of data can be transmitted.

-   **BME280**: Measures Temperature, Humidity, and Barometric Pressure.
-   **BMP280**: Measures Temperature and Barometric Pressure.
-   **BME680**: Measures Temperature, Humidity, Barometric Pressure, and Gas Resistance (VOC).
-   **Si7021**: Measures Temperature and Humidity.

---

## Data Transmission

To ensure compatibility with the APRS network, weather data is handled in a specific way.

### Alternating Packets

The device does not send weather data with every single beacon. Instead, it alternates between sending a standard beacon (containing telemetry like voltage in the comment) and a weather beacon. For example, the first beacon will be a standard position packet, the next will be a position packet with weather data, the third will be a standard one again, and so on.

### APRS Symbol Change

This is a critical requirement for the APRS network. For weather data to be correctly parsed and displayed by APRS-IS servers, the station's icon **must** be the official weather station symbol.

Our firmware handles this automatically. When a weather packet is due to be sent, the device temporarily changes its APRS symbol to the weather symbol (`_`, often displayed as a blue circle). Once the packet is sent, the symbol reverts to the one you configured for all subsequent non-weather beacons. **Without this symbol change, most platforms will ignore the weather data.**

### Data Format

All weather data is encoded into the standard APRS format:

-   **Temperature**: Sent in degrees Fahrenheit.
-   **Humidity**: Sent as a percentage.
-   **Pressure**: Sent in tenths of a millibar.
-   **Gas Resistance** (BME680 only): Sent as a comment in the packet (e.g., `Gas: 50.12 Kohms`).

You can configure a temperature offset and an altitude correction in the web interface to ensure the most accurate readings.
