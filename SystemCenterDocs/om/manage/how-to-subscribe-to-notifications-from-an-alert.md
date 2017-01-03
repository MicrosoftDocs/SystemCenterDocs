---
title: How to Subscribe to Notifications from an Alert
description: This article describes how to subscribe to a notification from a selected alert in the Operations console.   
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 01/03/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: d7e061b0-5d6e-49de-b93f-85215f7c4b73
---

# How to subscribe to Notifications from an alert

>Applies To: System Center 2016 - Operations Manager

In System Center 2016 - Operations Manager, when an alert is generated, Operations Manager can notify designated individuals by email, instant message (IM), or text message (SMS). Notifications can also run commands automatically when an alert is raised on a monitored system. A notification requires a channel, a subscriber, and a subscription.  
  
You can create a notification subscription from an alert to ensure that you are notified if the alert is sent again. You can either create a new subscription or add the alert to an existing subscription. In the following procedure, you create a new subscription.  
  
> [!NOTE]  
> You must have configured a notification channel and notification subscriber to perform this procedure.  
  
## To create a notification subscription from an alert  
  
1.  In the **Alerts** view, right-click the alert, click **Notification subscription**, and then click **Create**.  
  
2.  The text boxes for the name and description for the subscription are pre-populated with information from the alert. Click **Next**.  
  
3.  The text boxes for the conditions and criteria for when the notification is sent are pre-populated with default values from the alert. Click **Next**.  
  
4.  Click **Add or Remove** to select the notification subscriber that the notifications should be sent to.  
  
5.  Click **Search** to display all available subscribers.  
  
6.  Double-click the subscriber you want to use, and then click **OK**.  
  
7.  Click **Next**.  
  
8.  Click **Add or Remove** to select the notification channel to use.  
  
9. Click **Search** to display all available channels.  
  
10. Double-click the channel you want to use, and then click **OK**.  
  
11. Click **Next**, and then click **Finish**.  
  
12. Click **Close**.  
  
## Next steps 

* To designate when to send notifications and the addresses to which the notifications should be sent to, review [How to Create Notification Subscribers](how-to-create-notification-subscribers.md)

* Create a [notification subscription](how-to-create-notification-subscriptions.md) to define the criteria, notification channel, and subscribers that will receive the notification.  
