---
title: How to Enable an Instant Message Notification Channel
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 086970a5-845c-4a67-b164-a15f0af3213d
---
# How to Enable an Instant Message Notification Channel
To configure alert notifications for [!INCLUDE[om12long](../Token/om12long_md.md)], your first task is to enable a notification channel. This topic describes how to configure a channel that will send alert notifications to subscribers by using an instant message.

Before you begin, gather the following information from your instant message server \(Live Communications Server\):

-   Fully qualified domain name \(FQDN\).

-   Protocol used to send messages. You have two choices: TCP or Transport Layer Security \(TLS\).

-   Port used for instant messages. The default is 5060.

-   Encoding used by the instant message server and notification subscribers. The default is UTF\-8.

-   Return address to be used for the instant messages.

### To enable an instant message notification channel

1.  Log on to the computer with a user account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Administration**.

3.  In the navigation pane, under **Notifications**, right\-click **Channels**. Click **New channel**, and then click **Instant Message \(IM\)**.

4.  Type a name for the channel, such as **IM channel** and optionally provide a description. Click **Next**.

5.  In the **IM server** box, type the FQDN of an instant messaging server.

6.  Type the **Return Address** that should appear on instant message notifications. Preface the address with **sip:**. In the **Protocol option** list, select either TCP or TLS as the protocol used to send the instant messages. In the **Authentication method** list, select either NTLM or Kerberos as the authentication method for users. In the **IM port** box, the default instant messaging port of 5060 is entered. Type the port number used to send instant messages.

    > [!NOTE]
    > The return address should be a dedicated address that is used only for Operations Manager notifications.

7.  Click **Next**.

8.  In the **Default instant messaging notification format** area, in the **IM message** box, specify the text that is sent to notification subscribers. The **IM message** box contains a default message that includes text and variables. You can edit the default message or delete it and replace it with another message. You can click the right arrow next to the **IM message** box for a full list of available variables. For more information, see [How to Customize Message Content for Notifications](../Topic/How-to-Customize-Message-Content-for-Notifications.md).

9. In the **Encoding** box, select the text format that your IM server and notification subscribers use for transmission. By default, Unicode \(UTF\-8\) is used.

10. Click **Finish** and then click **Close**.

Next task: [How to Create and Configure the Notification Action Account](../Topic/How-to-Create-and-Configure-the-Notification-Action-Account.md)

## See Also
[How to Enable an Email Notification Channel](../Topic/How-to-Enable-an-Email-Notification-Channel.md)
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
[Sending Notifications for Specific Computers and Specific Alerts to Specific Teams](../Topic/Sending-Notifications-for-Specific-Computers-and-Specific-Alerts-to-Specific-Teams.md)

