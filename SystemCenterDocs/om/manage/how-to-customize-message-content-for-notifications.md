---
title: How to Customize Message Content for Notifications
authors:mgoedtel
manager:cfreemanwa
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0f6934ea-1998-4bd5-987a-41cf4e24d408
---

# How to Customize Message Content for Notifications

In System Center 2016 - Operations Manager, you can customize the format that will be used for messages that notify you of alerts. The format of an alert notification is determined by the channel by which the notification is sent. Each channel type has a default format, as shown in the following examples.  
  
> [!NOTE]  
> The command channel type is not mentioned because it generates a command rather than a notification message.  
  
|Channel type|Default notification format|  
|----------------|-------------------------------|  
|Email|**Subject**: Alert: *alert name* Resolution state: *new or closed*<br /><br />Alert:<br /><br />Source:<br /><br />Path:<br /><br />Last modified by:<br /><br />Last modified time:<br /><br />Alert description:<br /><br />Alert view link:<br /><br />Notification subscription ID generating this message:|  
|Instant message \(IM\)|Alert: *alert name* Path: *path to managed entity* Resolution state: *new or closed* Last modified by:|  
|SMS \(text message\)|Alert: *alert name* Resolution state: *new or closed*|  
  
You can change the format on the **Format** page of the channel type wizard when you create the channel or after the channel is created. The procedure is the same for all three channel types.  
  
## To configure notification format  
  
1.  On the **Format** page of the channel type wizard, in the message box for the channel type \(or subject box for the email channel\), delete any information from the default format that you do not want to include.  
  
2.  Position your cursor in the location of the box where you want to add information.  
  
3.  Type any non\-variable text that you want in the message.  
  
4.  Click the button to the right of the box to display the information you can add to the subject or message for notifications, as shown in the following illustration.  
  
    ![Options for notification messages](../media/om2016-notification-format-options.png)  
  
5.  Click any item in that list to add the corresponding variable to the notification message. For example, if you click **Alert Severity**, the following variable will be added to the box:  
  
    $Data\[Default\='Not Present'\]\/Context\/DataItem\/Severity$  
  
    > [!NOTE]  
    > When a default value for a parameter is included, such as \[Default\='Not Present'\] in the preceding example, it indicates the text to provide when the alert does not contain data for that parameter.  
  
6.  When you are done, click **Finish**. All notification messages that use the same channel will be formatted the same way.  
  
## Customizing a Channel for a Subscription  

When you create a subscription, you can copy an existing channel that you can customize for that subscription.  
  
### To customize a channel for a subscription  
  
1.  In the **Notification Subscription Wizard**, on the **Channels** page, click **New**, and then click **Create Customized Copy**.  
  
2.  In the **Channel Search** window, use **Filter by** and **Search** to locate the channel you want to copy. Select the channel in **Available channels**, click **Add**, and then click **OK**.  
  
3.  The notification channel wizard for the selected channel opens. You can change the name, description, settings, and message format on the corresponding wizard pages. As a best practice, change the name of the channel to distinguish it from the original channel. Click **Finish** when you are done making changes.  
  
