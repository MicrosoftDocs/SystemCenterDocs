---
title: Subscribe to alert notifications in Operations Manager
description: This article describes the alerts that Operations Manager can generate and notify individuals through email, instant message, text message, and Microsoft Teams.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 02/27/2025
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
ms.assetid: 4b0d664b-f806-4c3f-896b-aa0160ee4fb8
ms.update-cycle: 1095-days
---

# Subscribe to alert notifications in Operations Manager




In System Center - Operations Manager, when an alert is generated, Operations Manager can notify the designated individuals in the following modes:
- Email
- Instant message (IM)
- Text message (SMS)
- Microsoft Teams (applicable for 2022 and later)

Notifications can also run commands automatically when an alert is raised on a monitored system.  

A notification requires the following elements:  

-   A Run As account that provides credentials to the Notification Account Run As profile.  

-   A notification channel that defines the format for the notification and the method by which the notification is sent.  

-   A notification subscriber that defines the recipients and the schedule for sending notifications to the subscriber.  

-   A notification subscription that defines the criteria for sending a notification, the channel to be used, and the subscribers to receive the notification.  

An Operations Manager administrator must define the notification channels and if authentication is required, configure the Run As account for notifications. An Operations Manager administrator, advanced operator, or operator can create a subscriber and a subscription.  

## Subscribing to alert notifications articles  

-   [How to create and configure the Notification Action account](manage-notifications-create-configure.md)  

-   [How to enable an email notification channel](manage-notifications-create-email-channel.md)  

-   [How to enable Microsoft Teams notification channel](manage-notifications-create-teams-channel.md)

-   [How to enable an instant message notification channel](manage-notifications-create-im-channel.md)  

-   [How to enable a text message (SMS) notification channel](manage-notifications-create-txt-channel.md)  

-   [How to enable a command notification channel](manage-notifications-create-command-channel.md)  

-   [How to create notification subscribers](manage-notifications-create-subscribers.md)  

-   [How to create notification subscriptions](manage-notifications-create-subscriptions.md)  

-   [How to customize message content for Notifications](manage-notificiations-customize-message.md)  

-   [How to subscribe to notifications from an alert](manage-notifications-subscribe-from-alert.md)  

## Next steps

* To designate when to send notifications and the addresses to which the notifications should be sent, review [How to Create Notification Subscribers](manage-notifications-create-subscribers.md).

* To define the criteria, notification channel, and subscribers that will receive the notification, create a [notification subscription](manage-notifications-create-subscriptions.md).
