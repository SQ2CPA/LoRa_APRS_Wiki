---
layout: mobile_app
title: Recent Stations
permalink: /lora_aprs_mobile_app/recent-stations/
---

The Recent Stations feature allows you to see and interact with the stations you have recently heard over RF.

---

## Interaction from the Main Screen

The Main Screen provides a quick-glance card of the last 3 stations heard. You can perform quick actions from this card.

<img src="/assets/images/lora_aprs_mobile_app/recent-stations/main-screen-section.jpg" alt="Recent Stations section on Main Screen" style="max-width: 300px; width: 100%;">

-   **Short Tap**: Tapping a station in this list has two functions:
    -   If the station is message-capable (indicated by a **message icon**), it will immediately open a new message screen. This is a useful way to know if another user is actively running the LoRa APRS App.
    -   If the station is _not_ message-capable, it will open the **Station Details** page (see section 3).
-   **Long Press**: If you **long-press** any station in this list, it will _always_ open the **Station Details** page, bypassing the new message shortcut.

_(Note: Tapping the "Recent Stations" card title will navigate you to the full list described below.)_

---

## Recent Stations List

This screen shows a complete list of all stations you have recently heard. Unlike the Main Screen, this list is not limited to 3 stations.

This list provides more information at a glance, including:

-   Description
-   Telemetry
-   Weather Data

At the bottom of the screen, there is a button that allows you to **Clear** this entire list.

<img src="/assets/images/lora_aprs_mobile_app/recent-stations/recent-stations-list.jpg" alt="Full Recent Stations List" style="max-width: 300px; width: 100%;">

---

## Station Details

When you select a specific station from the Recent Stations List (or via the interaction on the Main Screen), you will be taken to its dedicated Details page.

<img src="/assets/images/lora_aprs_mobile_app/recent-stations/station-details.jpg" alt="Station Details Screen" style="max-width: 300px; width: 100%;">

This page contains all the information from the list (description, telemetry, weather) but also adds a detailed log of:

-   **Raw Frames**: A list of all raw packets received from this specific station, complete with their reception timestamps.
