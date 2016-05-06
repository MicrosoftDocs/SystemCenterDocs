---
title: Sending Notifications for Specific Computers and Specific Alerts to Specific Teams
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d84efd2b-be10-431e-9862-70ddccd2a940
---
# Sending Notifications for Specific Computers and Specific Alerts to Specific Teams
In [!INCLUDE[om12long](../Token/om12long_md.md)], when an alert is generated, Operations Manager can notify designated individuals. These notifications have three parts:

-   A channel, which can be email, instant message \(IM\), or text message \(SMS\). Notifications can also run commands automatically when an alert is raised on a monitored system.

-   A subscriber, which defines the recipients and the schedule for sending notifications to the subscriber.

-   A subscription, which defines the criteria for sending a notification, the channel to be used, and the subscribers to receive the notification.

You can use the combination of subscriber and subscription to tailor which alerts are sent to individuals or teams.

For example, suppose you have a team that wants to be notified of any problems on specific test lab servers that the team owns. To configure notifications for this situation, you would:

1.  Create a notification subscriber that uses the addresses for the individual team members or the address of a distribution list that contains the team members.

2.  Create a group that contains the test lab servers that the team wants to monitor.

3.  Create a subscription that sends notifications of alerts to the notification subscriber from step 1 for alerts raised by any member of the group from step 2.

## See Also
[How to Enable an Instant Message Notification Channel](../Topic/How-to-Enable-an-Instant-Message-Notification-Channel.md)
[How to Enable a Text Message &#40;SMS&#41; Notification Channel](../Topic/How-to-Enable-a-Text-Message--SMS--Notification-Channel.md)
[How to Enable a Command Notification Channel](../Topic/How-to-Enable-a-Command-Notification-Channel.md)
[How to Create Notification Subscribers](../Topic/How-to-Create-Notification-Subscribers.md)
[How to Create Notification Subscriptions](../Topic/How-to-Create-Notification-Subscriptions.md)
[Subscribing to Alert Notifications](../Topic/Subscribing-to-Alert-Notifications.md)
[How to Create and Configure the Notification Action Account](../Topic/How-to-Create-and-Configure-the-Notification-Action-Account.md)
[How to Customize Message Content for Notifications](../Topic/How-to-Customize-Message-Content-for-Notifications.md)
[How to Subscribe to Notifications from an Alert](../Topic/How-to-Subscribe-to-Notifications-from-an-Alert.md)
[How to Create Subscriptions Using Classes and Groups](../Topic/How-to-Create-Subscriptions-Using-Classes-and-Groups.md)
[How to Specify Which Alerts Generate Notifications &#40;Conditions&#41;](../Topic/How-to-Specify-Which-Alerts-Generate-Notifications--Conditions-.md)
[How to Enable an Email Notification Channel](../Topic/How-to-Enable-an-Email-Notification-Channel.md)

