---
title: Subscribing to Alert Notifications
description: This article highlights the section titles contained within this section of the Operations Manager documentation.
author: JYOTHIRMAISURI
ms.author: magoedte
manager: cfreemanwa
ms.date: 04/29/2019
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
ms.assetid: 4b0d664b-f806-4c3f-896b-aa0160ee4fb8
---

# Subscribing to alert notifications

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

In System Center - Operations Manager, when an alert is generated, Operations Manager can notify designated individuals by email, instant message (IM), or text message (SMS). Notifications can also run commands automatically when an alert is raised on a monitored system.  

A notification requires the following elements:  

-   A Run As account that provides credentials to the Notification Account Run As profile.  

-   A notification channel which defines the format for the notification and the method by which the notification is sent.  

-   A notification subscriber which defines the recipients and the schedule for sending notifications to the subscriber.  

-   A notification subscription which defines the criteria for sending a notification, the channel to be used, and the subscribers to receive the notification.  

An Operations Manager administrator must define the notification channels and if authentication is required, configure the Run As account for notifications. An Operations Manager administrator, advanced operator, or operator can create a subscriber and a subscription.  

## Subscribing to alert notifications topics  

-   [How to create and configure the Notification Action account](manage-notifications-create-configure.md)  

-   [How to enable an email notification channel](manage-notifications-create-email-channel.md)  

-   [How to enable an instant message notification channel](manage-notifications-create-im-channel.md)  

-   [How to enable a text message (SMS) notification channel](manage-notifications-create-txt-channel.md)  

-   [How to enable a command notification channel](manage-notifications-create-command-channel.md)  

-   [How to create notification subscribers](manage-notifications-create-subscribers.md)  

-   [How to create notification subscriptions](manage-notifications-create-subscriptions.md)  

-   [How to customize message content for Notifications](manage-notificiations-customize-message.md)  

-   [How to subscribe to notifications from an alert](manage-notifications-subscribe-from-alert.md)  
