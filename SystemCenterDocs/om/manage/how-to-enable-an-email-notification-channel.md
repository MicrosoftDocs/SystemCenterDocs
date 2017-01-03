---
title: How to Enable an Email Notification Channel
description: This article highlights the section titles contained within this section of the Operations Manager 2016 documentation.  
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 01/03/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: eb68582d-fe83-4d79-9017-55673f7f65b9
---

# How to Enable an Email Notification Channel

To configure alert notifications for System Center 2016 - Operations Manager, your first task is to enable a notification channel. This topic describes how to configure a channel that will send alert notifications to subscribers from an email server either within the domain of the organization or external email authentication.  
  
Before you begin, gather the following information:  
  
-   SMTP server information  
  
    -   Fully qualified domain name (FQDN).  
  
    -   Port number for the SMTP server.  
  
    -   Authentication method for the SMTP server. You have three choices: 
       -  Anonymous
       -  Windows Integrated
       -  External Email Authentication  
  
   > [!NOTE]
   > Operations Manager supports configuration of any external email account to send the notifications through External Email Authentication.  You now have the flexibility in terms of which email account is to be used for sending out the notification emails.  


-   Return email address. This address is used for all email notifications on this channel and will receive any replies to notifications.  
  - For internal email server, any return address that is within the domain can be specified.  Multiple internal servers can be added to the subscription channel.
  - For an external email server, the email account used for creating the Run As profile must match the return address.  To avoid coexistence issues with other email servers, a subscription channel with an external email account must contain only that email server.  
  
-   Email subject and body text that you want subscribers to receive. For more information, see [How to Customize Message Content for Notifications](how-to-customize-message-content-for-notifications.md).  
  
## To enable an email notification channel  
  
1.  Log on to the computer with a user account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Administration**.  
  
3.  In the navigation pane, under **Notifications**, right-click **Channels**. Click **New channel** and then click **E-mail (SMTP)**.  
  
4.  Type a name for the channel, such as **SMTP channel** and optionally provide a description. Click **Next**.  
  
5.  In the **SMTP servers** area, click **Add**.  
  
6.  In the **Add SMTP Server** dialog box, type the fully qualified domain name (FQDN) of a Simple Mail Transfer Protocol (SMTP) server, type the port number, select the authentication method used by the SMTP server, and then click **OK**.  
  
    > [!NOTE]  
    > You can add one or more additional servers to act as backup servers. If the primary SMTP server is unavailable, notifications are sent through the secondary server.  
  
7.  Type the **Return Address** that should appear on email notifications, and then in the **Retry interval** list, select the number of minutes to wait before trying to resend a notification to the primary SMTP server. Click **Next**.  
  
    > [!NOTE]  
    > If you have only one SMTP server and it's unavailable, the Retry interval has no effect. The Retry interval is used when you have a secondary server and mail sending to the primary server fails. When this happens, Operations Manager switches to the secondary server and checks the Retry interval time. If the Retry interval time has passed, Operations Manager tries to use the primary server.  
  
8.  In the **Default e-mail notification format** area, specify the **E-mail subject** and **E-mail message** text or leave the default selections, select the **Importance** level that you want the emails sent with, and then specify the **Encoding** type. You can click the right arrow next to the **E-mail subject** and **E-mail message** boxes for a full list of available variables. For more information, see [How to Customize Message Content for Notifications](how-to-customize-message-content-for-notifications.md).  
  
9. Click **Finish**, and then click **Close**.  
  

## Next steps

* To designate when to send notifications and the addresses to which the notifications should be sent to, review [How to Create Notification Subscribers](how-to-create-notification-subscribers.md)

* Create a [notification subscription](how-to-create-notification-subscriptions.md) to define the criteria, notification channel, and subscribers that will receive the notification.  
