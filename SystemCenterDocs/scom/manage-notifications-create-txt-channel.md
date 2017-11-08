---
title: How to Enable a Text Message (SMS) Notification Channel
description: This article describes how to create a text message notification channel in Operations Manager.
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 01/03/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 93f9a932-d99d-41b2-ad0c-f5e179f1cccf
---

# How to enable a text message (SMS) notification channel

To configure alert notifications for System Center 2016 - Operations Manager, your first task is to enable a notification channel. This topic describes how to configure a channel that will send alert notifications to subscribers by using a Short Message Service (SMS) or text message.  
  
> [!NOTE]  
> The modem used for SMS must support SMS Protocol Data Unit (PDU) mode.  
  
## To enable a text message notification channel  
  
1.  Log on to the computer with a user account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Administration**.  
  
3.  In the navigation pane, under **Notifications**, right-click **Channels**. Click **New channel** and then click **Text message (SMS)**.  
  
4.  Type a name for the channel, such as **SMS channel** and optionally provide a description. Click **Next**.  
  
5.  In the **Text message** box, specify the text that is sent to SMS notification subscribers. The **Text message** box contains a default message that includes text and variables. You can edit the default message or delete it and replace it with another message. You can click the right arrow next to the **Text message** box for a full list of available variables. For more information, see [How to Customize Message Content for Notifications](manage-notificiations-customize-message.md).  
  
6.  In the **Encoding**  box, select the text format for the SMS messages.  
  
7.  Click **Finish**, and then click **Close**.  
  
## Next steps

* To designate when to send notifications and the addresses to which the notifications should be sent to, review [How to create notification subscribers](manage-notifications-create-subscribers.md)

* Create a [notification subscription](manage-notifications-create-subscriptions.md) to define the criteria, notification channel, and subscribers that will receive the notification.  

* To create an email notification channel, see [How to enable an email notification channel](manage-notifications-create-email-channel.md). 

* To create a command channel notification, see [How to enable a command notification channel](manage-notifications-create-command-channel.md).

* To create an instant message notification channel see, [How to enable an instant message notification channel](manage-notifications-create-im-channel.md).