---
title: How to Enable a Text Message (SMS) Notification Channel
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 93f9a932-d99d-41b2-ad0c-f5e179f1cccf
author:mgoedtel
manager:cfreemanwa
---
# How to Enable a Text Message (SMS) Notification Channel
To configure alert notifications for [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)], your first task is to enable a notification channel. This topic describes how to configure a channel that will send alert notifications to subscribers by using a Short Message Service \(SMS\) or text message.  
  
> [!NOTE]  
> The modem used for SMS must support SMS Protocol Data Unit \(PDU\) mode.  
  
### To enable an SMS notification channel  
  
1.  Log on to the computer with a user account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Administration**.  
  
3.  In the navigation pane, under **Notifications**, right\-click **Channels**. Click **New channel** and then click **Text message \(SMS\)**.  
  
4.  Type a name for the channel, such as **SMS channel** and optionally provide a description. Click **Next**.  
  
5.  In the **Text message** box, specify the text that is sent to SMS notification subscribers. The **Text message** box contains a default message that includes text and variables. You can edit the default message or delete it and replace it with another message. You can click the right arrow next to the **Text message** box for a full list of available variables. For more information, see [How to Customize Message Content for Notifications](../../om/manage/How-to-Customize-Message-Content-for-Notifications.md).  
  
6.  In the **Encoding**  box, select the text format for the SMS messages.  
  
7.  Click **Finish**, and then click **Close**.  
  
Next task: [How to Create and Configure the Notification Action Account](../../om/manage/How-to-Create-and-Configure-the-Notification-Action-Account.md)  
  
## See Also  
[How to Enable an Instant Message Notification Channel](../../om/manage/How-to-Enable-an-Instant-Message-Notification-Channel.md)  
[How to Enable an Email Notification Channel](../../om/manage/How-to-Enable-an-Email-Notification-Channel.md)  
[How to Enable a Command Notification Channel](../../om/manage/How-to-Enable-a-Command-Notification-Channel.md)  
[How to Create Notification Subscribers](../../om/manage/How-to-Create-Notification-Subscribers.md)  
[How to Create Notification Subscriptions](../../om/manage/How-to-Create-Notification-Subscriptions.md)  
[Subscribing to Alert Notifications](../../om/manage/Subscribing-to-Alert-Notifications.md)  
[How to Create and Configure the Notification Action Account](../../om/manage/How-to-Create-and-Configure-the-Notification-Action-Account.md)  
[How to Customize Message Content for Notifications](../../om/manage/How-to-Customize-Message-Content-for-Notifications.md)  
[How to Subscribe to Notifications from an Alert](../../om/manage/How-to-Subscribe-to-Notifications-from-an-Alert.md)  
[How to Create Subscriptions Using Classes and Groups](../../om/manage/How-to-Create-Subscriptions-Using-Classes-and-Groups.md)  
[How to Specify Which Alerts Generate Notifications &#40;Conditions&#41;](../../om/manage/How-to-Specify-Which-Alerts-Generate-Notifications--Conditions-.md)  
[Sending Notifications for Specific Computers and Specific Alerts to Specific Teams](../../om/manage/Sending-Notifications-for-Specific-Computers-and-Specific-Alerts-to-Specific-Teams.md)  
  
