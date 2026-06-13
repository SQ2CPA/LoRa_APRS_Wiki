---
layout: digi
title: WiFi Logic
permalink: /lora_aprs_digi/wifi-logic/
---

This page explains how the device decides between running its own Access Point and connecting to your WiFi network, and how it behaves over time.

> **Terminology:** `STA` mode (Station) is sometimes also called **Client** mode. Both terms describe the same role: the device joining your existing WiFi network. `AP` mode means the device runs its own WiFi Access Point that you connect to directly.

---

## WiFi States

The device can be in one of the following states:

- **`AP`** — The device runs its own Access Point. Used when no WiFi client credentials are configured.
- **`STA_CONNECTING`** — A short STA-only phase where the device tries to join your WiFi network **without** exposing its own AP.
- **`STA`** — The device is connected to your WiFi network.
- **`AP_STA`** — Fallback mode: the device runs its own Access Point **and** keeps retrying the WiFi client connection in the background.
- **`OFF`** — WiFi is fully turned off (to save power).

---

## How It Works

### Starting up

- If **no WiFi client credentials** are configured, the device starts directly in **`AP`** mode.
- If **WiFi client credentials are configured**, the device always starts with a short **`STA_CONNECTING`** phase. During this phase it tries to join your network without broadcasting its own AP.
    - If the connection **succeeds** before the initial timeout expires, the device stays in **`STA`**.
    - If the connection **does not succeed** in time, the device switches to **`AP_STA`**.

> The length of the initial STA-only window is set by **Initial WiFi client connection attempt (seconds)** in the configuration.

### Fallback (`AP_STA`)

- In **`AP_STA`**, the Access Point becomes available so you can still reach the device, while the STA side keeps trying to connect in the background.
- If STA connects while in `AP_STA`, the AP is turned off and the device returns to **`STA`**.

### Losing the connection

- If STA disconnects **after being connected**, the device does **not** go straight back to AP. It first starts a new **`STA_CONNECTING`** phase.
- This means every new connection attempt starts with a short STA-only window — including boot, retry after `OFF`, and reconnect after a lost connection.

### Turning WiFi off

- In **`AP`** mode, the AP can stay available forever, or turn off after the configured AP timeout (**Disable Auto AP after (minutes)**, `0` = stay on).
- In **`AP_STA`** mode, WiFi can turn fully **`OFF`** after the AP has been idle long enough (**Disable AP+Client after (minutes)**, `0` = never).
- If **retry after `OFF`** is enabled (**Retry interval after WiFi off (minutes)**), the device waits for the configured interval and then restarts the whole cycle from `STA_CONNECTING`.
- If retry is disabled (`0`), `OFF` becomes a **terminal** state — WiFi stays off until reboot or manual intervention.

> **Low power mode:** In paths where WiFi would normally transition to `OFF`, the device sends a status packet and **restarts** instead.

---

## State Transitions

| From             | To               | When                                                              |
| ---------------- | ---------------- | ----------------------------------------------------------------- |
| `BOOT`           | `AP`             | No WiFi client credentials are configured.                        |
| `BOOT`           | `STA_CONNECTING` | WiFi client credentials are configured.                           |
| `STA_CONNECTING` | `STA`            | Device gets an IP address before the initial timeout expires.     |
| `STA_CONNECTING` | `AP_STA`         | Initial STA-only timeout expires without a successful connection. |
| `AP_STA`         | `STA`            | STA connection succeeds; the fallback AP is no longer needed.     |
| `STA`            | `STA_CONNECTING` | An existing STA connection is lost.                               |
| `AP`             | `OFF`            | AP-only timeout is enabled and the AP stays unused long enough.   |
| `AP_STA`         | `OFF`            | AP+Client timeout is enabled and the AP stays unused long enough. |
| `OFF`            | `STA_CONNECTING` | WiFi credentials exist and retry after `OFF` is enabled.          |
| `OFF`            | `OFF` (terminal) | No WiFi credentials exist, **or** retry after `OFF` is disabled.  |

---

## Scenarios

### 1. No WiFi credentials

- The device starts its AP immediately.
- If AP timeout is disabled, the AP stays up continuously.
- If AP timeout is enabled and nobody uses the AP for long enough, WiFi turns off.

### 2. WiFi available at boot

- The device starts in `STA_CONNECTING`.
- It joins the configured network during the initial STA-only window.
- The AP never appears.

### 3. WiFi unavailable at boot, fallback AP allowed forever

- The device starts in `STA_CONNECTING`.
- After the initial timeout, it switches to `AP_STA`.
- The AP becomes available and stays available.
- STA keeps retrying in the background until WiFi comes back.
- Once STA connects, the AP disappears and the device returns to `STA`.

### 4. WiFi unavailable at boot, fallback AP has timeout

- The device starts in `STA_CONNECTING`.
- It moves to `AP_STA` after the initial timeout.
- If nobody uses the AP and the AP+Client timeout expires, WiFi turns `OFF`.
- If retry is enabled, the device waits for the retry interval and starts over from `STA_CONNECTING`.
- This cycle repeats until STA eventually connects, or until retry is disabled.

### 5. AP is actively used during fallback

- The device is in `AP_STA`.
- While at least one AP client is connected, the AP idle timer is effectively pushed forward.
- The timeout only matters after the last AP client disconnects.

### 6. STA drops after it was working

- The device leaves `STA` and enters `STA_CONNECTING`.
- It first tries to recover in STA-only mode again.
- If WiFi returns quickly, the device goes back to `STA` without broadcasting an AP.
- If WiFi does not return in time, the device falls back to `AP_STA`.

### 7. Retry after OFF disabled

- The device can still reach `OFF` after the AP+Client timeout.
- Once in `OFF`, it stays there until manual intervention or reboot.

### 8. Low power mode

- In paths where WiFi would normally transition to `OFF`, the device sends a status packet and restarts instead.
