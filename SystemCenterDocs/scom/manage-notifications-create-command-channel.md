---
title: How to Enable a Command Notification Channel
description: This article describes how to create a command notification channel in Operations Manager.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 01/03/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 230eadbd-2a79-4987-903f-4bd0c85536fd
---

# How to enable a command notification channel

>Applies To: System Center 2016 - Operations Manager

To configure alert notifications for System Center 2016 - Operations Manager, your first task is to enable a notification channel. This topic describes how to configure a channel that runs an executable program automatically in response to an alert.  
  
To create a command notification channel, you need the following information:  
  
-   Full path of the command file.  
  
-   Command line parameters.  
  
-   The startup folder for the command, which is the path of the program you want to run.  
  
> [!IMPORTANT]  
> Unlike the other notification channels, the command notification channel will run its command by using Local System, rather than the Notification Action Account.  
  
## To enable a command notification  
  
1.  Log on to the computer with a user account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Administration**.  
  
3.  In the navigation pane, under **Notifications**, right-click **Channels**. Click **New channel** and then click **Command**.  
  
4.  Type a unique name for this command channel in the **Notification command channel name** box and a brief description in the **Description** box. Click **Next**.  
  
5.  Type the path to the executable file that you want to run in the **Full path to command file**  box. For example, "%systemroot%\cmd.exe" or "c:\windows\system32\cscript.exe". Type any parameters that you want to run with this command in **Command line parameters** box. Type the  directory for this command in the **Startup folder for the command line** box.  
  
6.  Click **Finish**, and then click **Close**.  
  
## Next steps

* To designate when to send notifications and the addresses to which the notifications should be sent to, review [How to create notification subscribers](manage-notifications-create-subscribers.md)

* Create a [notification subscription](../om/manage/how-to-create-notification-subscriptions.md) to define the criteria, notification channel, and subscribers that will receive the notification.  

* To create a text message (SMS) notification channel, see [How to enable a text message (SMS) notification channel](manage-notifications-create-txt-channel.md).

* To create an email notification channel, see [How to enable an email notification channel](manage-notifications-create-email-channel.md). 

* To create an instant message notification channel see, [How to enable an instant message notification channel](manage-notifications-create-im-channel.md).
