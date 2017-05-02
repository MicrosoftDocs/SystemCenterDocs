---
title: How to Enable an Instant Message Notification Channel
description: This article describes how to create an instant message notification channel for Operations Manager.  
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 01/03/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 086970a5-845c-4a67-b164-a15f0af3213d
---
# How to enable an instant message notification channel

To configure alert notifications for System Center 2016 - Operations Manager, your first task is to enable a notification channel. This topic describes how to configure a channel that will send alert notifications to subscribers by using an instant message.  
  
Before you begin, gather the following information from your instant message server:  
  
-   Fully qualified domain name (FQDN).  
  
-   Protocol used to send messages. You have two choices: TCP or Transport Layer Security (TLS).  
  
-   Port used for instant messages. The default is 5061.  
  
-   Encoding used by the instant message server and notification subscribers. The default is UTF-8.  
  
-   Return address to be used for the instant messages.  
  
## To enable an instant message notification channel  
  
1.  Log on to the computer with a user account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Administration**.  
  
3.  In the navigation pane, under **Notifications**, right-click **Channels**. Click **New channel**, and then click **Instant Message (IM)**.  
  
4.  Type a name for the channel, such as **IM channel** and optionally provide a description. Click **Next**.  
  
5.  In the **IM server** box, type the FQDN of an instant messaging server.  
  
6.  Type the **Return Address** that should appear on instant message notifications. Preface the address with **sip:**. In the **Protocol option** list, select either TCP or TLS as the protocol used to send the instant messages. In the **Authentication method** list, select either NTLM or Kerberos as the authentication method for users. In the **IM port** box, the default instant messaging port of 5060 is entered. Type the port number used to send instant messages.  
  
    > [!NOTE]  
    > The return address should be a dedicated address that is used only for Operations Manager notifications.  
  
7.  Click **Next**.  
  
8.  In the **Default instant messaging notification format** area, in the **IM message** box, specify the text that is sent to notification subscribers. The **IM message** box contains a default message that includes text and variables. You can edit the default message or delete it and replace it with another message. You can click the right arrow next to the **IM message** box for a full list of available variables. For more information, see [How to customize message content for notifications](manage-notificiations-customize-message.md).  
  
9. In the **Encoding** box, select the text format that your IM server and notification subscribers use for transmission. By default, Unicode (UTF-8) is used.  
  
10. Click **Finish** and then click **Close**.  
  
## Next steps

* To designate when to send notifications and the addresses to which the notifications should be sent to, review [How to create notification subscribers](manage-notifications-create-subscribers.md)

* Create a [notification subscription](manage-notifications-create-subscriptions.md) to define the criteria, notification channel, and subscribers that will receive the notification.    

* To create an email notification channel, see [How to enable an email notification channel](manage-notifications-create-email-channel.md). 

* To create a command channel notification, see [How to enable a command notification channel](manage-notifications-create-command-channel.md).

* To create a text message (SMS) notification channel, see [How to enable a text message (SMS) notification channel](manage-notifications-create-txt-channel.md).