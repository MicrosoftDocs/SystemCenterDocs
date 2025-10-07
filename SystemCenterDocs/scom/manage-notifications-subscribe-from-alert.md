---
title: Subscribe to Notifications from an Alert
description: This article describes how to subscribe to a notification from a selected alert in the Operations console.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 08/07/2025
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
ms.assetid: d7e061b0-5d6e-49de-b93f-85215f7c4b73
---

# Subscribe to notifications from an alert



In System Center - Operations Manager, when an alert is generated, Operations Manager can notify designated individuals by email, instant message (IM), text message (SMS), or Microsoft Teams (applicable for 2022 and later). Notifications can also run commands automatically when an alert is raised on a monitored system. A notification requires a channel, a subscriber, and a subscription.  

You can create a notification subscription from an alert to ensure that you're notified if the alert is sent again. You can either create a new subscription or add the alert to an existing subscription. You create a new subscription using the following procedure.  

> [!NOTE]  
> You must have configured a notification channel and notification subscriber to perform this procedure.  

This article describes how to subscribe to a notification from a selected alert in the Operations console.

## Create a notification subscription from an alert

To create a notification subscription from an alert, follow these steps:

1.  In the **Alerts** view, right-click the alert, select **Notification subscription**, and select **Create**.  

2.  The text boxes for the name and description for the subscription are pre-populated with information from the alert. Select **Next**.  

3.  The text boxes for the conditions and criteria for when the notification is sent are pre-populated with default values from the alert. Select **Next**.  

4.  Select **Add or Remove** to select the notification subscriber to whom the notifications should be sent.  

5.  Select **Search** to display all available subscribers.  

6.  Double-click the subscriber you want to use, and select **OK**.  

7.  Select **Next**.  

8.  Select **Add or Remove** to select the notification channel to use.  

9. Select **Search** to display all available channels.  

10. Double-click the channel you want to use, and select **OK**.  

11. Select **Next**, and select **Finish**.  

12. Select **Close**.  

## Next steps

* To designate when to send notifications and the addresses to which the notifications should be sent to, review [Create Notification Subscribers](manage-notifications-create-subscribers.md).

* To define the criteria, notification channel, and subscribers that will receive the notification, create a [notification subscription](manage-notifications-create-subscriptions.md).  
