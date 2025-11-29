---
layout: general
title: Getting Support
permalink: /general/support/
---

If you're experiencing issues with your LoRa APRS devices (Digi/iGate/Tracker), this guide will help you troubleshoot problems and get the support you need.

## Before Asking for Help

When something doesn't work as expected, it's crucial to provide detailed information to receive effective assistance. However, before reaching out for help, please verify the basics first. Many issues can be resolved by checking these fundamental aspects:

### Essential Checks

Before reporting an issue, **always verify** the following:

1. **Power Supply**

    - Ensure your device is receiving adequate power
    - Check if the power supply meets the voltage and current requirements
    - Verify all power connections are secure
    - Test with a different power source if possible

2. **Wiring and Connections**

    - Inspect all cables and connectors for damage
    - Ensure all connections are properly seated and secure
    - Check for loose pins or connectors
    - Verify correct wiring according to the device documentation

3. **Antenna**

    - Confirm the antenna is properly connected
    - Check for physical damage to the antenna
    - Verify you're using an appropriate antenna for the frequency band
    - Ensure the antenna connector is tight and making good contact
    - Check antenna placement and potential obstructions

4. **Basic Configuration**

    - Verify your callsign is correctly configured
    - Check that frequency settings match your local requirements
    - Ensure LoRa parameters (bandwidth, spreading factor) are correct
    - Confirm WiFi credentials are accurate (if applicable)

5. **Firmware Version**
    - Note which firmware version you're running
    - Check if you're using the latest stable release
    - Verify the firmware was installed correctly

## How to Report an Issue

If you've checked all the basics above and still need help, provide the following information:

### Required Information

1. **Device Type**

    - Specify which device you're using (Tracker, Digi, iGate)
    - Include hardware model/version if applicable

2. **Firmware Version**

    - State the exact firmware version number
    - Mention if you modified any code

3. **Detailed Problem Description**

    - What exactly is not working?
    - What were you trying to do?
    - What did you expect to happen?
    - What actually happened?

4. **Configuration Details**

    - Share relevant configuration settings
    - Include frequency, LoRa parameters, and any custom settings
    - **Note**: Remove or redact sensitive information (passwords, API keys)

5. **When Did It Start?**

    - Did it ever work correctly?
    - What changed before the problem started?
    - Is the problem consistent or intermittent?

6. **Troubleshooting Steps Already Taken**

    - List what you've already tried
    - Include results of the basic checks mentioned above

7. **Logs and Error Messages**
    - If available, provide relevant log entries
    - Include any error messages verbatim
    - Screenshots can be helpful but should supplement text descriptions

### Example of a Good Support Request

> **Device**: T-Beam V1.2 SX1278
>
> **Firmware**: v1.0.4
>
> **Problem**: My tracker is not transmitting position packets
>
> **Details**: The device powers on and shows GPS position on the display, but I don't see any packets on aprs.fi. I've verified:
>
> -   Power supply is 5V USB and Li-ion 18650 installed.
> -   Antenna is connected (433 MHz antenna, SMA connector tight)
> -   GPS shows 8 satellites locked
> -   Configured callsign: MYCALL-9
> -   LoRa frequency: 434.855 MHz 1200bps
>
> **What I tried**:
>
> -   Checked configuration three times
> -   Power cycled the device
> -   Moved to open area for better antenna performance
> -   Verified the digi is online and receiving packets from others
>
> The device worked fine yesterday but stopped transmitting this morning.

## Where to Get Help

### GitHub Issues

For bug reports and feature requests, please use the appropriate repository:

-   **LoRa APRS Tracker**: [GitHub Issues](https://github.com/SQ2CPA/LoRa_APRS_Tracker/issues)
-   **LoRa APRS Digi/iGate**: [GitHub Issues](https://github.com/SQ2CPA/LoRa_APRS_Digi/issues)

### Documentation

-   Check the relevant wiki sections for your device - many questions are already answered in the documentation

### Direct Contact

If you've checked the wiki and documentation but still need help, feel free to reach out:

-   **E-mail**: [sq2cpa@gmail.com](mailto:sq2cpa@gmail.com)
-   **Telegram**: [@SQ2CPA](https://t.me/SQ2CPA)

Please ensure you've reviewed the documentation first, but don't hesitate to contact directly if your issue persists.

## Common Issues

Remember that most problems stem from:

-   Power supply issues (inadequate voltage/current)
-   Poor or missing antenna connections
-   Incorrect configuration settings
-   Outdated firmware

Always start with these basics before diving into more complex troubleshooting.

---

**Good troubleshooting practices lead to faster solutions!**
