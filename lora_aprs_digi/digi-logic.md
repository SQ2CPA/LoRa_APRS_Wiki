---
layout: digi
title: Digipeater Logic
permalink: /lora_aprs_digi/digi-logic/
---

This page describes the digipeater behavior from an operator and user perspective, including all processing rules, path handling, compatibility with legacy formats, and the TEMP PATH feature.

The digipeater settings referenced here are configured in the **Digipeater Settings** section of the web interface - see [Configuration](/lora_aprs_digi/configuration/).

---

## Modes

The digipeater operates in one of five modes:

| Mode | Name                 | Relays                                    |
| ---- | -------------------- | ----------------------------------------- |
| 0    | Disabled             | Nothing                                   |
| 1    | Callsign only        | Own callsign or alias in path + TEMP PATH |
| 2    | WIDE1 (fill-in)      | WIDE1-N paths                             |
| 3    | WIDE1+WIDE2 combined | Both WIDE1-N and WIDE2-N, greedy          |
| 4    | WIDE2 (wide-area)    | WIDE2-N paths + WIDE1-1                   |

All modes above 0 also handle own callsign and alias in path (TEMP PATH) at all times.

---

## How Path Processing Works

### The "first unused address" rule

An APRS path is a comma-separated list of addresses. An address marked with `*` has already been processed by a digipeater ("used"). An address without `*` has not been processed yet ("unused").

**Finding the first unused address:**

1. Find the position of the last address that has `*` in the path.
2. The first unused address is the one immediately after it.
3. If no address has `*`, the entire path is unused - start from the beginning.
4. If there are no more addresses after the last `*`, there is nothing to relay → ignore.

**Processing the first unused address:**

- Check whether the digi is capable of handling that address type (see mode table).
- If not → ignore the packet entirely, even if there are processable addresses further right.
- If yes → relay the packet with the updated path:
    - The first unused address is replaced by `<digi_callsign>*`.
    - If the address was `WIDEn-N` with N > 1, insert `WIDEn-(N-1)` after the digi callsign.
    - All addresses after the first unused address are kept unchanged.
    - All addresses **before** the first unused address: depends on the **Path Marker Mode** setting (see section below). By default, their `*` markers are preserved (keep mode). In standard mode they are removed - only the current digi's callsign carries `*` in the relayed path.

---

## Mode 2 - WIDE1 Fill-In Digipeater

Handles `WIDE1-N` addresses only. Ignores any path where the first unused address is not WIDE1.

| Incoming path     | Relayed path      |
| ----------------- | ----------------- |
| `WIDE1-1`         | `<call>*`         |
| `WIDE1-1,WIDE2-1` | `<call>*,WIDE2-1` |
| `WIDE1-1,WIDE2-2` | `<call>*,WIDE2-2` |
| `WIDE2-1`         | **ignored**       |
| `F1*,WIDE1-1`     | `F1,<call>*`      |

> With "Keep path markers" enabled: `F1*,WIDE1-1` → `F1*,<call>*`

A packet with `WIDE2-1` as first unused is ignored even if `WIDE1-1` appears later.

---

## Mode 4 - WIDE2 Wide-Area Digipeater

Handles `WIDE2-N` addresses and `WIDE1-1` (N=1 only, per New N-N paradigm). Ignores `WIDE1-2` and higher.

| Incoming path     | Relayed path                          |
| ----------------- | ------------------------------------- |
| `WIDE2-1`         | `<call>*`                             |
| `WIDE2-2`         | `<call>*,WIDE2-1`                     |
| `F1*,WIDE2-1`     | `F1,<call>*`                          |
| `F1*,WIDE2-2`     | `F1,<call>*,WIDE2-1`                  |
| `WIDE1-1`         | `<call>*`                             |
| `WIDE1-1,WIDE2-1` | `<call>*,WIDE2-1`                     |
| `WIDE1-2`         | **ignored** (N > 1)                   |
| `WIDE1-2,WIDE2-1` | **ignored** (first unused is WIDE1-2) |

> With "Keep path markers" enabled: `F1*,WIDE2-1` → `F1*,<call>*` and `F1*,WIDE2-2` → `F1*,<call>*,WIDE2-1`

### Sequential example - `WIDE2-2`

1. Source sends: `WIDE2-2`
2. First wide-area digi (H1) relays: `H1*,WIDE2-1`
3. Second wide-area digi (H2) relays: `H1,H2*`

With "Keep path markers" enabled: step 3 produces `H1*,H2*` instead.

---

## Mode 3 - Combined WIDE1+WIDE2 Digipeater (Greedy)

Mode 3 processes all `WIDE1-N` and `WIDE2-N` addresses in the unused portion of the path in a single pass.

- All `WIDE1-N` are consumed completely.
- `WIDE2-N` with N=1 is consumed; with N>1 it is decremented to `WIDE2-(N-1)`.
- The digi inserts its callsign once, at the position of the first consumed WIDE address.
- Addresses before the unused portion follow the Path Marker Mode setting.

| Incoming path     | Relayed path              |
| ----------------- | ------------------------- |
| `WIDE1-1`         | `<call>*`                 |
| `WIDE2-1`         | `<call>*`                 |
| `WIDE2-2`         | `<call>*,WIDE2-1`         |
| `WIDE1-1,WIDE2-1` | `<call>*` (both consumed) |
| `WIDE1-1,WIDE2-2` | `<call>*,WIDE2-1`         |
| `F1*,WIDE2-1`     | `F1,<call>*`              |
| `F1*,WIDE2-2`     | `F1,<call>*,WIDE2-1`      |

> With "Keep path markers" enabled: `F1*,WIDE2-1` → `F1*,<call>*` and `F1*,WIDE2-2` → `F1*,<call>*,WIDE2-1`

---

## Path Order Matters

Processing always goes left to right. If the first unused address is a type the digi cannot handle, the packet is ignored - even if a handleable address appears further right.

**Example:** path `WIDE2-1,WIDE1-1` arriving at a mode 2 (WIDE1) digi.

- First unused = `WIDE2-1` → mode 2 does not handle WIDE2 → **ignored**.
- `WIDE1-1` at position 2 is never reached.

This is correct APRS behavior. Paths like `WIDE2-1,WIDE1-1` are malformed and will not be efficiently relayed.

---

## Compatibility with Legacy Path Formats

Older digipeater software (pre-New N-N) inserts its callsign **without** `*` directly before the WIDE element it processed. For example:

- A legacy combined digi receives `WIDE1-1,WIDE2-2` and produces: `WIDE1*,SQ2-1,WIDE2-1`

Here `SQ2-1` already relayed the packet but has no `*`. The `WIDE1*` is the position marker.

### How the new logic handles this

When the last `*` in the path belongs to a WIDE-type address (e.g. `WIDE1*`), the digi applies **legacy normalization**: it skips over any callsigns without `*` that appear between the WIDE marker and the next processable address (own callsign, alias, or another WIDE address).

| Legacy incoming path         | First unused found        | Mode 4 relay (default)      |
| ---------------------------- | ------------------------- | --------------------------- |
| `WIDE1*,SQ2-1,WIDE2-1`       | `WIDE2-1` (SQ2-1 skipped) | `WIDE1,SQ2-1,<call>*`       |
| `WIDE1*,SQ2-1,SQ2-2,WIDE2-1` | `WIDE2-1` (both skipped)  | `WIDE1,SQ2-1,SQ2-2,<call>*` |
| `SQ2-1,WIDE1*,WIDE2-1`       | `WIDE2-1`                 | `SQ2-1,WIDE1,<call>*`       |
| `SQ2-1,WIDE1*,SQ2-2,WIDE2*`  | none                      | **ignored** ✓               |
| `WIDE1*,SQ2-1,WIDE2*`        | none                      | **ignored** ✓               |
| `SQ2-1,SQ2-2,WIDE2*`         | none                      | **ignored** ✓               |

> With "Keep path markers" enabled: `WIDE1*` and other `*` markers in the pre-relay portion are preserved - e.g. `WIDE1*,SQ2-1,WIDE2-1` → `WIDE1*,SQ2-1,<call>*`

Exhausted paths (last `*` on a WIDE element with no remaining addresses) are always ignored correctly.

---

## Path Optimization

When the digi's own callsign or configured alias is the first unused address **and** the path contains legacy WIDE `*` markers before it, the digi performs path optimization: it converts the legacy format to the new clean format in a single relay.

**Optimization rules applied to all addresses before own callsign:**

- WIDE-type addresses with `*` (e.g. `WIDE1*`) → **always removed** (they were position markers, not real digis)
- Other callsign addresses → follow the Path Marker Mode setting

Then own callsign is appended with `*`. Everything after remains unchanged.

### Examples

`sourceCallsign = SQ2CPA-1`

| Incoming path                      | Relayed path (default)       | Relayed path (keep markers)   |
| ---------------------------------- | ---------------------------- | ----------------------------- |
| `SQ2CPA-2,WIDE1*,SQ2CPA-1`         | `SQ2CPA-2,SQ2CPA-1*`         | `SQ2CPA-2*,SQ2CPA-1*`         |
| `SQ2CPA-2,WIDE1*,SQ2CPA-1,WIDE2-1` | `SQ2CPA-2,SQ2CPA-1*,WIDE2-1` | `SQ2CPA-2*,SQ2CPA-1*,WIDE2-1` |
| `WIDE1*,SQ2-1,SQ2CPA-1`            | `SQ2-1,SQ2CPA-1*`            | `SQ2-1*,SQ2CPA-1*`            |
| `F1*,SQ2CPA-1,WIDE2-1`             | `F1,SQ2CPA-1*,WIDE2-1`       | `F1*,SQ2CPA-1*,WIDE2-1`       |

> Note: `F1*` in the last row - F1 is a callsign address (not WIDE-type), so path optimization is not triggered. `*` on F1 is removed or kept based on the Path Marker Mode setting, not by optimization logic.

**Why this matters:** In both modes, the relayed path contains no unused addresses after `SQ2CPA-1*` - so any digi receiving the packet will find no further work to do and correctly ignores it. Loop prevention relies on the 30-second deduplication cache, not on the presence of `*` on previous addresses.

---

## TEMP PATH

TEMP PATH allows a tracker or portable station to act as a relay digi for another station that cannot reach the main APRS network directly. Active in all modes above 0.

### Configuration

One optional alias callsign can be configured (`dgi_temp_call`, max 9 characters; the **TEMP PATH Alias** field in the web interface). When a packet arrives with this alias or the digi's own callsign as the first unused address, the digi relays it - replacing the alias or callsign with its own callsign marked `*`.

### Use case

A handheld radio (HH) is operated in an area with no direct WIDE1 digipeater coverage, but a car tracker (SQ2CPA-10) is nearby with good coverage.

**Option A - HH puts the car's callsign in the path explicitly:**

HH sends: `SQ2CPA-10,WIDE1-1,WIDE2-1`

Car tracker receives, sees `SQ2CPA-10` as first unused (matches own callsign) → relays:
`SQ2CPA-10*,WIDE1-1,WIDE2-1`

A WIDE1 digi then relays: `SQ2CPA-10,<W1>*,WIDE2-1`
A WIDE2 digi then relays: `SQ2CPA-10,<W1>,<W2>*`

> With "Keep path markers": `SQ2CPA-10*,<W1>*,WIDE2-1` and `SQ2CPA-10*,<W1>*,<W2>*`

**Option B - Car configured with `dgi_temp_call = MOBILE`:**

HH sends: `MOBILE,WIDE1-1,WIDE2-1`

Car receives, sees `MOBILE` as first unused (matches alias) → relays using own callsign:
`SQ2CPA-10*,WIDE1-1,WIDE2-1`

The path continues normally from there.

**Option C - Car configured with `dgi_temp_call = SQ2CPA-9` (HH's callsign):**

HH sends: `SQ2CPA-9,WIDE1-1,WIDE2-1`

Car receives, sees `SQ2CPA-9` (matches alias) → relays as:
`SQ2CPA-10*,WIDE1-1,WIDE2-1`

HH does not need to know the car's callsign - just puts its own callsign in the path.

### Loop prevention

If the car receives its own relay back (`SQ2CPA-10*,WIDE1-1,WIDE2-1`):

- Last `*` = `SQ2CPA-10*` (a callsign, not WIDE) → no legacy normalization
- First unused = `WIDE1-1`
- Mode 1: WIDE1-1 is not handled → **ignored** ✓
- Mode 2+: same payload hash was already seen within 30 seconds → **ignored** ✓

---

## Path Validation - Duplicate Address Detection

Before processing, the path is validated. A packet is rejected if any address appears more than once in the path (case-insensitive, ignoring `*`).

| Path                      | Result                                |
| ------------------------- | ------------------------------------- |
| `WIDE1-1,WIDE2-1,WIDE1-1` | **rejected** - WIDE1-1 appears twice  |
| `WIDE2-1,WIDE2-1`         | **rejected** - WIDE2-1 appears twice  |
| `wide2-1,WIDE2-1`         | **rejected** - case-insensitive match |
| `F1*,WIDE2-1,F1`          | **rejected** - F1 appears twice       |
| `WIDE1-1,WIDE2-1`         | accepted                              |

---

## Frame Deduplication

The digi maintains a cache of recently seen frames (identified by a hash of the source and payload, excluding the path). If the same frame is received again within **30 seconds**, it is not retransmitted.

This prevents duplicate transmissions when the same packet arrives via multiple paths, and provides a safety net against relay loops.

---

## Path Marker Mode

This setting controls whether previous `*` markers in the relayed path are preserved or stripped.

| Setting                         | Behavior                                                                                              |
| ------------------------------- | ----------------------------------------------------------------------------------------------------- |
| **Standard**                    | Only the current digi's callsign carries `*`. All `*` from previous hops are removed from the output. |
| **Keep path markers** (default) | All previous `*` markers are preserved. Each hop in the chain retains its `*`.                        |

### Why this matters

In standard mode, the relayed path is clean and shows only who relayed last:

- `F1*,WIDE2-1` received by H1 → relayed as `F1,H1*`

In "keep" mode, the full relay history is visible:

- `F1*,WIDE2-1` received by H1 → relayed as `F1*,H1*`

Most APRS software and iGate displays show only the last `*` entry regardless, so for end users the practical difference is minimal. Standard mode produces shorter, cleaner paths. Keep mode is useful if you want the full relay chain visible in raw packet logs.

Loop prevention works identically in both modes - it is always based on the 30-second frame deduplication cache, not on the presence of `*` markers.

### Configuration

The setting is available in the web interface under the Digipeater configuration section as "Keep path markers (`*`)". It is checked by default (keep mode).

---

## Cross-Digi (RX/TX on Different Frequencies)

When the receive and transmit frequencies are different (cross-digi mode), the digi applies a simpler rule: it strips all WIDE markers from the path and inserts its own callsign with `*`. The first-unused-address algorithm, legacy normalization, path optimization, and TEMP PATH do not apply in this mode.

---

## Complete Path Examples

### Standard WIDE2-2 traversal (new format, two wide-area digis)

1. Source transmits: `WIDE2-2`
2. H1 (first W2 digi, mode 4) relays: `H1*,WIDE2-1`
3. H2 (second W2 digi, mode 4) relays: `H1,H2*`
4. IGate receives `H1,H2*` - both hops consumed, no further relay.

> With "Keep path markers": step 3 produces `H1*,H2*`

### Mixed WIDE1+WIDE2 traversal (fill-in then wide-area)

1. Source transmits: `WIDE1-1,WIDE2-1`
2. F1 (fill-in digi, mode 2) relays: `F1*,WIDE2-1`
3. H1 (wide-area digi, mode 4) relays: `F1,H1*`

> With "Keep path markers": step 3 produces `F1*,H1*`

### TEMP PATH with path optimization (legacy W1 in network)

Car callsign = `SQ2CPA-10`, `dgi_temp_call = SQ2CPA-9`.

1. HH transmits: `SQ2CPA-9,WIDE1-1,WIDE2-1`
2. Car (SQ2CPA-10) receives, `SQ2CPA-9` is first unused → matches alias → relays:
   `SQ2CPA-10*,WIDE1-1,WIDE2-1`
3. Fill-in digi (mode 2) receives → relays: `SQ2CPA-10,F1*,WIDE2-1`
4. Wide-area digi (mode 4) receives → relays: `SQ2CPA-10,F1,H1*`

> With "Keep path markers": step 3 = `SQ2CPA-10*,F1*,WIDE2-1`, step 4 = `SQ2CPA-10*,F1*,H1*`

### Old-format path arriving at own callsign digi

1. Legacy combined digi processed `WIDE1-1,WIDE2-2` and produced:
   `SQ2CPA-2,WIDE1*,SQ2CPA-1,WIDE2-1`
2. SQ2CPA-1 digi (mode 1+) receives this, detects `WIDE1*` before own callsign → path optimization:
    - `WIDE1*` → **removed** (always)
    - `SQ2CPA-2` → kept as-is (default) or marked `SQ2CPA-2*` (keep markers mode)
    - `SQ2CPA-1` → own callsign → `SQ2CPA-1*`
    - `WIDE2-1` → unchanged
3. Relayed path (default): `SQ2CPA-2,SQ2CPA-1*,WIDE2-1`
   (with "Keep path markers": `SQ2CPA-2*,SQ2CPA-1*,WIDE2-1`)
4. SQ2CPA-2 hears this - last `*` = `SQ2CPA-1*`, no addresses after it (for the no-WIDE2-1 case) → **ignored** ✓. For the WIDE2-1 case, the 30-second deduplication prevents re-relay.
5. Wide-area digi (mode 4) receives → relays: `SQ2CPA-2,SQ2CPA-1,H1*`
   (with "Keep path markers": `SQ2CPA-2*,SQ2CPA-1*,H1*`)
