---
title: How to Enable a Command Notification Channel
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 230eadbd-2a79-4987-903f-4bd0c85536fd
author:mgoedtel
manager:cfreemanwa
---
# How to Enable a Command Notification Channel
To configure alert notifications for [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)], your first task is to enable a notification channel. This topic describes how to configure a channel that runs an executable program automatically in response to an alert.  
  
To create a command notification channel, you need the following information:  
  
-   Full path of the command file.  
  
-   Command line parameters.  
  
-   The startup folder for the command, which is the path of the program you want to run.  
  
> [!IMPORTANT]  
> Unlike the other notification channels, the command notification channel will run its command by using Local System, rather than the Notification Action Account.  
  
### To enable a command notification  
  
1.  Log on to the computer with a user account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Administration**.  
  
3.  In the navigation pane, under **Notifications**, right\-click **Channels**. Click **New channel** and then click **Command**.  
  
4.  Type a unique name for this command channel in the **Notification command channel name** box and a brief description in the **Description** box. Click **Next**.  
  
5.  Type the path to the executable file that you want to run in the **Full path to command file**  box. For example, “%systemroot%\\cmd.exe” or “c:\\winnt\\system32\\cscript.exe”. Type any parameters that you want to run with this command in **Command line parameters** box. Type the  directory for this command in the **Startup folder for the command line** box.  
  
6.  Click **Finish**, and then click **Close**.  
  
After you have enabled the command notification channel, do the following:  
  
-   Create a notification subscriber that has the command channel selected in the subscriber address. For more information, see [How to Create Notification Subscribers](../../om/manage/How-to-Create-Notification-Subscribers.md).  
  
-   Create a new subscription and select only the subscriber created for this command. For more information, see [How to Create Notification Subscriptions](../../om/manage/How-to-Create-Notification-Subscriptions.md).  
  
## See Also  
[How to Enable an Instant Message Notification Channel](../../om/manage/How-to-Enable-an-Instant-Message-Notification-Channel.md)  
[How to Enable a Text Message &#40;SMS&#41; Notification Channel](../../om/manage/How-to-Enable-a-Text-Message--SMS--Notification-Channel.md)  
[How to Enable an Email Notification Channel](../../om/manage/How-to-Enable-an-Email-Notification-Channel.md)  
[How to Create Notification Subscribers](../../om/manage/How-to-Create-Notification-Subscribers.md)  
[How to Create Notification Subscriptions](../../om/manage/How-to-Create-Notification-Subscriptions.md)  
[Subscribing to Alert Notifications](../../om/manage/Subscribing-to-Alert-Notifications.md)  
[How to Create and Configure the Notification Action Account](../../om/manage/How-to-Create-and-Configure-the-Notification-Action-Account.md)  
[How to Customize Message Content for Notifications](../../om/manage/How-to-Customize-Message-Content-for-Notifications.md)  
[How to Subscribe to Notifications from an Alert](../../om/manage/How-to-Subscribe-to-Notifications-from-an-Alert.md)  
[How to Create Subscriptions Using Classes and Groups](../../om/manage/How-to-Create-Subscriptions-Using-Classes-and-Groups.md)  
[How to Specify Which Alerts Generate Notifications &#40;Conditions&#41;](../../om/manage/How-to-Specify-Which-Alerts-Generate-Notifications--Conditions-.md)  
[Sending Notifications for Specific Computers and Specific Alerts to Specific Teams](../../om/manage/Sending-Notifications-for-Specific-Computers-and-Specific-Alerts-to-Specific-Teams.md)  
  
