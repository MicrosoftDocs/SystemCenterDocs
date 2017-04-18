---
title: How to Create Notification Subscribers
description: This article describes how to create notification subscribers that will be added to notification subscriptions in Operations Manager.  
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 01/03/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 94fe3ff6-c9d9-46c9-8dde-288d8361ccc0
---

# How to create notification subscribers

>Applies To: System Center 2016 - Operations Manager

In System Center 2016 - Operations Manager, when an alert is generated, Operations Manager can notify designated individuals by email, instant message (IM), or text message (SMS). Notifications can also run commands automatically when an alert is raised on a monitored system. A notification requires a channel, a subscriber, and a subscription.  
  
These procedures explain how to create subscribers for notifications. A notification subscriber defines when to send notifications and the addresses to which the notifications should be sent. A subscriber can be an individual user account or a distribution list.  
  
Notification channels must be enabled before you create subscribers. After a subscriber is created, you create a notification subscription that defines the format of the notification message and any filters such as age or severity of the alert.  
  
## To create a notification subscriber as an administrator  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Administration**.  
  
3.  Under **Notifications**, right-click **Subscribers,** and click **New subscriber**.  
  
4.  On the **Description** page, type a display name for this subscriber.  
  
5.  On the **Schedule Notifications** page, click **Always send notifications**, or **Notify only during the specified times** and specify when notifications should be sent to this subscriber. The options available allow you to:  
  
    -   Limit notifications to a specific range of dates.  
  
    -   Specify that notifications are sent only during certain hours or except for certain hours.  
  
    -   Specify that notifications will be sent only on certain days of the week.  
  
    -   Set a time zone to be used for the subscriber.  
  
    > [!NOTE]  
    > The settings on the **Schedule Notifications** page apply globally to the subscriber. You can also specify unique schedule settings for each address that you add to the subscriber, in the following steps. For example, you can add one email address that receives the notifications during business hours and add a second email address that receives the notifications outside of business hours.  
  
6.  On the **Subscriber Addresses** page, click **Add** to add subscriber addresses to the notification.  
  
7.  On the **Describe the Subscriber Address** page, enter a name to identify the subscriber address, and then click **Next**.  
  
8.  On the **Provide the Channel and Delivery Address** page, perform the following steps:  
  
    1.  In **Channel Type**, select between email, instant message, text message, or command for the method of notification.  
  
    2.  If you select command for channel type, in **Command Channel**, select the name of a command channel. The command channel must be created before you create the subscriber. Skip the next step, because no delivery address is specified for a command channel.  
  
    3.  In **Delivery address for the selected channel**, enter the address to which the notification should be sent.  
  
    4.  Click **Next**.  
  
9. On the **Schedule Notifications** page, click **Always send notifications**, or **Notify only during the specified times** and click **Add** to create a date range, and then click **Next**.  
  
10. Click **Add** to define another subscriber address. Otherwise, click **Finish**, and then click **Close**.  
  
11. The new subscriber displays in the **Subscribers** pane.  
  
## Next steps

* Create a [notification subscription](../om/manage/how-to-create-notification-subscriptions.md) to define the criteria, notification channel, and subscribers that will receive the notification.  