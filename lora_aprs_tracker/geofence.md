---
layout: tracker
title: Geofence
permalink: /lora_aprs_tracker/geofence/
---

Geofence is an automatic frequency management feature that changes the tracker's operating frequency based on your geographical location. This ensures compliance with regional frequency regulations as you travel across different countries or regions.

---

## How Geofence Works

When geofence is enabled (AUTO mode), the tracker continuously monitors your GPS position and compares it against predefined geographical boundaries. When you cross from one region to another, the tracker automatically switches to the appropriate frequency (and speed) for that area.

The status change is always relative to the **current state**. This means the tracker remembers which region it was operating in and only triggers a change when it detects movement to a different region. For detailed information about status packets and their meanings, see [Status Packets](/lora_aprs_tracker/status-packets/).

---

## QSY Notification on Region Change

When the tracker detects a region change, it performs the following sequence:

1. **Transmits on the OLD frequency** - The tracker first sends a status packet on the current (old) frequency to inform stations in that area that it is leaving.

2. **Transmits on the NEW frequency** - After switching, the tracker sends a status packet on the new frequency to announce its arrival in the new region.

**Status messages sent:**

- **`Geofence QSY`** - Announces that a frequency change is occurring
- **`PL->EU`** - Indicates the direction of the change (e.g., from Poland region to Europe region)

For example, if you drive from Poland into Germany, the tracker will:

1. Send `Geofence QSY PL->EU` on 434.855 MHz (Polish frequency)
2. Switch to the new frequency
3. Send `Geofence QSY PL->EU` on 433.775 MHz (European frequency)

This way, stations monitoring both frequencies are informed about your transition.

---

## Supported Frequencies

The geofence feature supports the following regional frequency presets:

| Region                  | Frequency    | Speed    |
| ----------------------- | ------------ | -------- |
| **PL** (Poland)         | 434.855 MHz  | 1200 bps |
| **EU** (Europe)         | 433.775 MHz  | 1200 bps |
| **UK** (United Kingdom) | 439.9125 MHz | 1200 bps |

---

## Geofence Status Indicators

When geofence is active, the tracker startup status will show:

- **`Tracker started AUTO NOFIX`** - Geofence is enabled, but GPS hasn't determined the region yet
- **`Tracker started AUTO PL`** - Operating in Poland region
- **`Tracker started AUTO EU`** - Operating in Europe region
- **`Tracker started AUTO UK`** - Operating in UK region
