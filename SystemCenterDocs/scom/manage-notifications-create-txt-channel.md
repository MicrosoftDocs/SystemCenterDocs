---
title: How to Enable a Text Message (SMS) Notification Channel
description: This article describes how to create a text message notification channel in Operations Manager.
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 04/29/2019
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
ms.assetid: 93f9a932-d99d-41b2-ad0c-f5e179f1cccf
---

# How to enable a text message (SMS) notification channel

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

To configure alert notifications for System Center - Operations Manager, your first task is to enable a notification channel. This topic describes how to configure a channel that will send alert notifications to subscribers by using a Short Message Service (SMS) or text message.  

## Prerequisites
To enable an SMS Notification Channel, ensure the following:
1. Modem(s) for SMS with support for SMS Protocol Data Unit (PDU) mode is/are set.

2. The Modem(s) is/are attached via the **COM Port** on **all** the management servers present in the **Notifications Resource Pool**.

3. The Baud Rate of the COM port is set to: **9600**

### How to set COM Port Baud Rate from the Command Line
1. Open Administrator Command Prompt

2. List all modes: `Mode`

3. Set the COM Port to use a Bits Per Second (Baud) rate of 9600: `Mode Com1: Baud=9600`

## To enable a text message notification channel

1.  Log on to the computer with a user account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Administration**.  

3.  In the navigation pane, under **Notifications**, right-click **Channels**. Click **New channel** and then click **Text message (SMS)**.  

4.  Type a name for the channel, such as **SMS channel** and optionally provide a description. Click **Next**.  

5.  In the **Text message** box, specify the text that is sent to SMS notification subscribers. The **Text message** box contains a default message that includes text and variables. You can edit the default message or delete it and replace it with another message. You can click the right arrow next to the **Text message** box for a full list of available variables. For more information, see [How to Customize Message Content for Notifications](manage-notificiations-customize-message.md).  

6.  In the **Encoding**  box, select the text format for the SMS messages.  

7.  Click **Finish**, and then click **Close**.  

> [!NOTE]
> When customizing the text message, ensure that SMS has a **160 character limit**. Operations Manager cannot send longer messages (over 160 characters) using Multimedia Messaging Service (MMS). 

## Next steps

* To designate when to send notifications and the addresses to which the notifications should be sent to, review [How to create notification subscribers](manage-notifications-create-subscribers.md)

* Create a [notification subscription](manage-notifications-create-subscriptions.md) to define the criteria, notification channel, and subscribers that will receive the notification.  

* To create an email notification channel, see [How to enable an email notification channel](manage-notifications-create-email-channel.md).

* To create a command channel notification, see [How to enable a command notification channel](manage-notifications-create-command-channel.md).

* To create an instant message notification channel see, [How to enable an instant message notification channel](manage-notifications-create-im-channel.md).
