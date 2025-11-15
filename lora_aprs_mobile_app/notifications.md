---
layout: mobile_app
title: Notifications
permalink: /lora_aprs_mobile_app/notifications/
---

The app uses Android's notification system to provide status updates and alert you to new messages.

---

## Background Service Notification

When the app is running in the background, it displays a persistent notification (also known as a "silent notification").

This notification **cannot be disabled**, as it is required by the Android system to keep the app's connection service running.

The notification shows key status information at a glance:

-   Your connected device's callsign.
-   The current connection type (Classic, BLE, TCPIP).
-   The callsign of the last received packet.
-   The type of the last received packet (e.g., beacon, message, ack, etc.).

<img src="/assets/images/lora_aprs_mobile_app/notifications/silent-notification.jpg" alt="Background Service Notification" style="max-width: 300px; width: 100%;">

---

## New Message Notifications

In addition to the service notification, you will receive a standard, high-priority, clickable notification whenever you receive a new APRS message.

This notification will show the sender's **callsign** and the **content of the message**, allowing you to quickly see what you've received.

<img src="/assets/images/lora_aprs_mobile_app/notifications/message-notification.jpg" alt="New Message Notification" style="max-width: 300px; width: 100%;">

---

## Future Enhancements

We plan to add more notification types in the future to provide more useful, at-a-glance information. An example of a planned notification is an alert for a **low battery level** on your connected LoRa APRS device.
