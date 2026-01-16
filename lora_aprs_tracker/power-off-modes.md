---
layout: tracker
title: Power Off Modes
permalink: /lora_aprs_tracker/power-off-modes/
---

Not all trackers power down in the same way. The method used to turn off the device depends entirely on its underlying hardware design. There are two primary methods you'll encounter: a true hardware shutdown managed by a dedicated chip, and a software-simulated "off" state using the microcontroller's deep sleep mode.

Understanding the difference is crucial for proper battery management.

---

## 1. Hardware Power Off (e.g., T-Beam)

This is the most effective and safest way to power down a device.

-   **How it works**: Devices like the **T-Beam** include a dedicated **Power Management Unit (PMU)**, such as the AXP192 chip. When you long-press the power button, this chip gets a signal to completely cut the power supply to the main components of the tracker (the main processor, LoRa chip, GPS module, etc.).
-   **Battery Drain**: The power consumption in this state is near-zero, as the circuit is physically disconnected from the battery. You can leave a device in this state for months with minimal battery loss.
-   **Battery Protection**: A major advantage of PMU chips is that they typically include **built-in battery protection circuits**. They actively monitor the battery voltage and will automatically shut down the device if the voltage drops to a critically low level, preventing permanent damage to the Li-Ion/Li-Po cell.

This is a **true "off" state**.

---

## 2. Software "Power Off" / Deep Sleep (e.g., Heltec Wireless Tracker)

This method is a clever software workaround for devices that lack a dedicated power management chip.

-   **How it works**: On devices like the **Heltec Wireless Tracker**, there is no chip to physically cut the power. Instead, when you select the power off option from the [Menu](/lora_aprs_tracker/menu/), the firmware puts the main processor into its lowest possible power mode, known as **"deep sleep."** In this state, the processor is almost entirely shut down, but it keeps just enough circuitry active to listen for a wake-up signal (in this case, a press of the reset/power-on button).
-   **Battery Drain**: While extremely low, there is still a **small but constant power draw** to maintain this wake-up capability. It's not zero. Leaving the device in this state for many weeks or months _will_ eventually drain the battery.
-   **The Critical Limitation**: This software method **does not inherently protect the battery from over-discharge**. Because the device is never truly off, it will continue to draw a tiny amount of current. If the battery is already low, leaving it in this state for an extended period can drain it below the safe voltage limit, potentially destroying the battery cell.

For this reason, it is essential that devices using the deep sleep method have a separate **Battery Management System (BMS)** circuit, either on the mainboard or built into the battery pack itself, to provide over-discharge protection.

This is a **simulated "off" state**, not a true hardware shutdown, but it works fine.
