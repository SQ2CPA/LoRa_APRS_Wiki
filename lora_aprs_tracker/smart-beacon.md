---
layout: tracker
title: LoRa APRS Tracker Understanding Smart Beacon
permalink: /lora_aprs_tracker/smart-beacon/
---

Smart Beacon is an intelligent algorithm designed to make your tracker transmit its position in a more efficient and relevant way. Instead of sending beacons at a fixed rate (e.g., every 2 minutes), Smart Beacon adjusts the transmission frequency based on your movement, specifically your speed and changes in direction.

The main `Beacon Interval` setting in the configuration becomes the **slowest** possible transmission rate when Smart Beacon is active.

---

## Why Use Smart Beacon? The Driving Analogy

To understand the benefit, let's compare a fixed beacon interval to the Smart Beacon logic using a driving analogy.

### The Problem: Fixed Beacon Interval

Imagine you set your `Beacon Interval` to 5 minutes.

-   **Driving in City Traffic**: You start your car, drive two blocks, turn right, wait at a red light, drive another three blocks, and then turn left into a parking lot. All of this could happen in under 5 minutes. With a fixed interval, your tracker might only send one beacon at the start and one after you've already parked. On the APRS map, it would look like you magically jumped from your starting point to the destination, completely missing the actual route you took.

-   **Driving on the Highway**: Now you're on a long, straight highway, traveling at a constant speed. Sending a beacon every 30 seconds would be excessive. Your position is highly predictable, and these frequent transmissions would unnecessarily clog the radio frequency for other users without providing much new information.

### The Solution: Smart Beacon

Smart Beacon solves both problems by adapting to the situation.

-   **In City Traffic (The "Cork")**: The algorithm detects your low speed and, more importantly, your frequent turns. Every time you make a significant turn, it triggers a beacon to accurately plot your path through the city streets. When you are stopped, it dramatically slows down the transmission rate to the maximum interval, as your position is not changing.

-   **On the Highway (The "Autostrada")**: When you are traveling at a high, constant speed in a straight line, the algorithm recognizes that your position is predictable. It reduces the number of beacons, sending them only periodically to confirm your progress. This frees up the radio frequency. If you were to exit the highway, the sharp turn would immediately trigger a new beacon.

In short, Smart Beacon sends packets when they are most needed—during changes in movement—and stays quiet when they are not, leading to a much more accurate track without congesting the APRS network.

---

## Smart Beacon Parameters

The firmware includes several pre-configured profiles for different activities. Each profile has a set of internal parameters that define its behavior, such as minimum/maximum speed thresholds and turn sensitivity.

Below are the internal values used for each mode. While you don't need to change these, they illustrate how each mode is tuned for a specific type of activity.

| Mode       | Max Time (s) | Min Speed (km/h) | Fast Time (s) | Fast Speed (km/h) | Turn Angle (deg) | Turn Slope | Min Turn Time (s) | Decay Time |
| :--------- | :----------: | :--------------: | :-----------: | :---------------: | :--------------: | :--------: | :---------------: | :--------: |
| **Car**    |     120      |        10        |      60       |        70         |       100        |     12     |        10         |     80     |
| **Bike**   |     120      |        5         |      60       |        40         |       100        |     12     |        12         |     60     |
| **Runner** |     120      |        3         |      60       |        15         |        50        |     20     |        12         |     60     |

**What these parameters generally control:**

-   **Time values**: Define the fastest and slowest beacon rates.
-   **Speed values**: Define the speed thresholds for switching between fast and slow rates.
-   **Turn values**: Define how sensitive the tracker is to changes in direction to trigger a beacon.
