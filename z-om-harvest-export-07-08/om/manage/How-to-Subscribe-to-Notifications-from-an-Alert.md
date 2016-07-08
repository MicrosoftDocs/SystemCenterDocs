---
title: How to Subscribe to Notifications from an Alert
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7e061b0-5d6e-49de-b93f-85215f7c4b73
author:mgoedtel
manager:cfreemanwa
---
# How to Subscribe to Notifications from an Alert
In [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)], when an alert is generated, Operations Manager can notify designated individuals by email, instant message \(IM\), or text message \(SMS\). Notifications can also run commands automatically when an alert is raised on a monitored system. A notification requires a channel, a subscriber, and a subscription.  
  
You can create a notification subscription from an alert to ensure that you are notified if the alert is sent again. You can either create a new subscription or add the alert to an existing subscription. In the following procedure, you create a new subscription.  
  
> [!NOTE]  
> You must have configured a notification channel and notification subscriber to perform this procedure.  
  
### To create a notification subscription from an alert  
  
1.  In the **Alerts** view, right\-click the alert, click **Notification subscription**, and then click **Create**.  
  
2.  The text boxes for the name and description for the subscription are pre\-populated with information from the alert. Click **Next**.  
  
3.  The text boxes for the conditions and criteria for when the notification is sent are pre\-populated with default values from the alert. Click **Next**.  
  
4.  Click **Add or Remove** to select the notification subscriber that the notifications should be sent to.  
  
5.  Click **Search** to display all available subscribers.  
  
6.  Double\-click the subscriber you want to use, and then click **OK**.  
  
7.  Click **Next**.  
  
8.  Click **Add or Remove** to select the notification channel to use.  
  
9. Click **Search** to display all available channels.  
  
10. Double\-click the channel you want to use, and then click **OK**.  
  
11. Click **Next**, and then click **Finish**.  
  
12. Click **Close**.  
  
## See Also  
[How to Enable an Instant Message Notification Channel](../../om/manage/How-to-Enable-an-Instant-Message-Notification-Channel.md)  
[How to Enable a Text Message &#40;SMS&#41; Notification Channel](../../om/manage/How-to-Enable-a-Text-Message--SMS--Notification-Channel.md)  
[How to Enable a Command Notification Channel](../../om/manage/How-to-Enable-a-Command-Notification-Channel.md)  
[How to Create Notification Subscribers](../../om/manage/How-to-Create-Notification-Subscribers.md)  
[How to Create Notification Subscriptions](../../om/manage/How-to-Create-Notification-Subscriptions.md)  
[Subscribing to Alert Notifications](../../om/manage/Subscribing-to-Alert-Notifications.md)  
[How to Create and Configure the Notification Action Account](../../om/manage/How-to-Create-and-Configure-the-Notification-Action-Account.md)  
[How to Customize Message Content for Notifications](../../om/manage/How-to-Customize-Message-Content-for-Notifications.md)  
[How to Enable an Email Notification Channel](../../om/manage/How-to-Enable-an-Email-Notification-Channel.md)  
[How to Create Subscriptions Using Classes and Groups](../../om/manage/How-to-Create-Subscriptions-Using-Classes-and-Groups.md)  
[How to Specify Which Alerts Generate Notifications &#40;Conditions&#41;](../../om/manage/How-to-Specify-Which-Alerts-Generate-Notifications--Conditions-.md)  
[Sending Notifications for Specific Computers and Specific Alerts to Specific Teams](../../om/manage/Sending-Notifications-for-Specific-Computers-and-Specific-Alerts-to-Specific-Teams.md)  
  
