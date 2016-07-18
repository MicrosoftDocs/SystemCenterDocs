---
title: How to Create Notification Subscriptions
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8361d0b2-8b6d-462c-aee0-800eda31dd21
author:mgoedtel
manager:cfreemanwa
---
# How to Create Notification Subscriptions
In [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)], when an alert is generated, Operations Manager can notify designated individuals by email, instant message \(IM\), or text message \(SMS\). Notifications can also run commands automatically when an alert is raised on a monitored system. A notification requires a channel, a subscriber, and a subscription.  
  
These procedures explain how to configure a notification subscription. A subscription defines the criteria for a notification, such as when a critical alert is generated. A subscription also defines the channel to be used for the notification and the subscribers to receive the notification.  
  
Notification channels and subscribers must be configured before you create a subscription.  
  
### To create a notification subscription as an administrator  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Administration**.  
  
3.  In the **Administration** workspace, expand **Notifications**, right\-click **Subscriptions,** and then click **New subscription**. The Notification Subscription Wizard starts.  
  
4.  On the **Description** page, in **Subscription name,** type a descriptive name for the subscription, type a short description, and then click **Next**.  
  
5.  On the **Subscription Criteria** page, you can set conditions that will determine when notifications will be sent to specified subscribers. If you do not set conditions, notifications will be sent for all alerts. Click **Next**.  
  
    > [!NOTE]  
    > You will also receive notifications when an alert is updated.  
  
6.  On the **Subscribers** page, click **Add** to add subscribers who are already defined, or click **New** to add new subscribers. For more information on defining subscribers, see [How to Create Notification Subscriptions](../../om/manage/How-to-Create-Notification-Subscriptions.md).  
  
7.  Click **Next**.  
  
8.  On the **Channels** page, click **Add** to add a channel that is already defined, or click **New** to add a new channel. For more information on defining channels, see [How to Enable an Email Notification Channel](../../om/manage/How-to-Enable-an-Email-Notification-Channel.md), [How to Enable an Instant Message Notification Channel](../../om/manage/How-to-Enable-an-Instant-Message-Notification-Channel.md), [How to Enable a Text Message &#40;SMS&#41; Notification Channel](../../om/manage/How-to-Enable-a-Text-Message--SMS--Notification-Channel.md), and [How to Enable a Command Notification Channel](../../om/manage/How-to-Enable-a-Command-Notification-Channel.md).  
  
9. In the **Alert aging** section on the **Channels** page, select to send notifications without delay or set a value in minutes that notification should be delayed unless conditions remain unchanged, and then click **Next**.  
  
10. Review the settings on the **Summary** page, click **Finish**, and then click **Close**.  
  
### To create a notification subscription as an operator  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Operators or Advanced Operators role.  
  
2.  In the Operations console, click **Tools** in the top menu bar, and then click **My Subscriptions**.  
  
3.  In the **Notification Subscriptions** window, click **New**.  
  
4.  On the **Description** page, in **Subscription name,** type a descriptive name for the subscription, type a short description, and then click **Next**.  
  
5.  On the **Subscription Criteria** page, you can set conditions that will determine when notifications will be sent to specified subscribers. If you do not set conditions, notifications will be sent for all alerts. Click **Next**.  
  
    > [!NOTE]  
    > You will also receive notifications when an alert is updated.  
  
6.  On the **Subscribers** page, click **Add** to add subscribers who are already defined, or select a subscriber in the **Selected subscribers** box and click **Edit** to change the settings for this subscription. For more information on defining subscribers, see [How to Create Notification Subscriptions](../../om/manage/How-to-Create-Notification-Subscriptions.md).  
  
7.  Click **Next**.  
  
8.  On the **Channels** page, click **Add** to add a channel that is already defined, or click **New** to create a customized copy of an existing channel. For more information on defining channels, see [How to Enable an Email Notification Channel](../../om/manage/How-to-Enable-an-Email-Notification-Channel.md), [How to Enable an Instant Message Notification Channel](../../om/manage/How-to-Enable-an-Instant-Message-Notification-Channel.md), [How to Enable a Text Message &#40;SMS&#41; Notification Channel](../../om/manage/How-to-Enable-a-Text-Message--SMS--Notification-Channel.md), and [How to Enable a Command Notification Channel](../../om/manage/How-to-Enable-a-Command-Notification-Channel.md).  
  
9. In the **Alert aging** section on the **Channels** page, select to send notifications without delay or set a value in minutes that notification should be delayed unless conditions remain unchanged, and then click **Next**.  
  
10. Review the settings on the **Summary** page, click **Finish**, and then click **Close**.  
  
## See Also  
[How to Enable an Instant Message Notification Channel](../../om/manage/How-to-Enable-an-Instant-Message-Notification-Channel.md)  
[How to Enable a Text Message &#40;SMS&#41; Notification Channel](../../om/manage/How-to-Enable-a-Text-Message--SMS--Notification-Channel.md)  
[How to Enable a Command Notification Channel](../../om/manage/How-to-Enable-a-Command-Notification-Channel.md)  
[How to Create Notification Subscribers](../../om/manage/How-to-Create-Notification-Subscribers.md)  
[How to Enable an Email Notification Channel](../../om/manage/How-to-Enable-an-Email-Notification-Channel.md)  
[Subscribing to Alert Notifications](../../om/manage/Subscribing-to-Alert-Notifications.md)  
[How to Create and Configure the Notification Action Account](../../om/manage/How-to-Create-and-Configure-the-Notification-Action-Account.md)  
[How to Customize Message Content for Notifications](../../om/manage/How-to-Customize-Message-Content-for-Notifications.md)  
[How to Subscribe to Notifications from an Alert](../../om/manage/How-to-Subscribe-to-Notifications-from-an-Alert.md)  
[How to Create Subscriptions Using Classes and Groups](../../om/manage/How-to-Create-Subscriptions-Using-Classes-and-Groups.md)  
[How to Specify Which Alerts Generate Notifications &#40;Conditions&#41;](../../om/manage/How-to-Specify-Which-Alerts-Generate-Notifications--Conditions-.md)  
[Sending Notifications for Specific Computers and Specific Alerts to Specific Teams](../../om/manage/Sending-Notifications-for-Specific-Computers-and-Specific-Alerts-to-Specific-Teams.md)  
  
