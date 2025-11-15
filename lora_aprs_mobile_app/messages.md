---
layout: mobile_app
title: Messages
permalink: /lora_aprs_mobile_app/messages/
---

The app includes a full-featured APRS messaging system. You can manage all your conversations from the main screen.

---

## Accessing Messages

On the **Main Screen**, you will find the **Messages Section**.

<img src="/assets/images/lora_aprs_mobile_app/messages/messages-section.jpg" alt="Messages Section on Main Screen" style="max-width: 300px; width: 100%;">

-   **Messages List (Chat Icon)**: Tapping this button opens your full conversation list. If you have unread messages, a badge will appear on this icon indicating the count.
-   **New Message (Pencil Icon)**: This button, located next to the chat icon, opens a new, blank message screen.

---

## New Message Screen

When you tap the "New Message" button, you are taken to the compose screen.

<img src="/assets/images/lora_aprs_mobile_app/messages/new-message.jpg" alt="New Message Screen" style="max-width: 300px; width: 100%;">

Here, you can enter the recipient's **Callsign** (with optional **SSID**) and your **Message** content. After pressing the send button, you will be automatically redirected to the conversation screen for that recipient.

---

## Conversation List Screen

This screen shows all your separate conversations.

<img src="/assets/images/lora_aprs_mobile_app/messages/conversation-list.jpg" alt="Conversation List Screen" style="max-width: 300px; width: 100%;">

-   It's a standard conversation list. Unread conversations are highlighted.
-   At the bottom, there is a floating button to create a new conversation (which takes you to the New Message Screen).
-   **To delete a conversation**, long-press any conversation in the list, and a delete option will appear.

---

## Conversation View

This is a standard chat screen showing the history with a specific station.

<img src="/assets/images/lora_aprs_mobile_app/messages/conversation-view.jpg" alt="Conversation View Screen" style="max-width: 300px; width: 100%;">

-   **Received Messages**:
    -   Displays information about whether an `ACK` (acknowledgment) was successfully sent back from your device.
    -   Messages received via **TCPIP** (from the internet, not RF) are marked with a "network" symbol.
-   **Sent Messages**:
    -   Displays information about whether an `ACK` was received from the recipient.
    -   A **person icon** next to a sent message indicates that the `ACK` was received from a compatible app (like another LoRa APRS App user), meaning it was likely a manually confirmed reply, not an automatic one.
-   **Message Actions**: If you **long-press one of your own sent messages**, a menu will appear allowing you to:
    -   **Cancel Sending**: If the message is still in the queue to be sent.
    -   **Resend**: To try sending the message again (e.g., if it failed or received no ACK).
