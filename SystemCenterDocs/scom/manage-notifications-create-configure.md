---
ms.assetid: ab2991fd-8228-4afc-89c3-a380129d4a84
title: How to Create and Configure the Notification Action Account
description:  
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 01/03/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to create and configure the Notification action account

>Applies To: System Center 2016 - Operations Manager

In System Center 2016 - Operations Manager, when an alert is generated, Operations Manager can notify designated individuals by email, instant message (IM), or text message (SMS). The Notification Account Run As profile is used to send notifications. For notifications to work correctly, you must create a Run As account that provides the credentials for sending notifications and associate the Run As account to the Notification Account profile.  
  
## To create and configure the Notification action account  
  
1.  Sign in to the computer with a user account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Administration**.  
  
3.  In the **Administration** workspace, right-click **Security**, and then click **Create Run As Account**. Use the Create Run As Account Wizard to create an account to use as the Notification action account, which is used to send the notifications.  
  
4.  On the **Introduction** page, click **Next**.  
  
5.  On the **General Properties** page, select **Windows** in the **Run As Account type** list for setting up authentication with an email server in the same organization or domain or select **Simple Authentication** for setting up authentication with an external mail server, and then in **Display name**, type **Notification action account**. Click **Next**.  
  
6.  On the **Credentials** page, type the information for the user name, password, and domain (if required) of the user account that to be used for notifications. Click **Next**.  
  
7.  Select the **More secure** distribution security option. For more information on this option, see [Distribution and Targeting for Run As Accounts and Profiles](../om/manage/distribution-and-targeting-for-run-as-accounts-and-profiles.md).  
  
8.  Click **Create**.  
  
9. In the navigation pane, click **Accounts** under **Run As Configuration**.  
  
10. In the details pane, right-click **Notification action account**, and then click **Properties**.  
  
11. On the **Distribution** tab, click **Add**.  
  
12. In the **Computer Search** window, click **Search** to display a name of available computers.  
  
13. Select the server or servers to distribute the credentials to, click **Add**, and then click **OK** to close the search window.  
  
14. Click **OK** to close the properties window.  
  
15. In the navigation pane, click **Profiles** under **Run As Configuration**.  
  
16. Right-click **Notification Account** and click **Properties**, which will open the **Run As Profile Wizard**.  
  
17. On the **Introduction** page, click **Next**.  
  
18. If you are configuring an internal email, then on the **General Properties** page, click **Next**. If you are configuring an external email then, right-click on **Profiles** and click **Create Run As Profile**. On the **General Properties** page enter a suitable **Display name** and for **Select destination management pack**, choose **Notification Internal Library** from the drop-down list.  
  
19. On the **Run As Accounts** page, click **Add**.  
  
20. In the **Add a Run As Account** window, in the **Run As account** drop-down list,  select the Run As account that you created earlier in this procedure. If you are configuring an internal email accept the default **All targeted objects** and then click **OK**. If you are configuring an external email, choose **A selected class, group, or object**, click **Select** and choose **Class**. On the **Class Search** page search and select **Alert Notification Subscription server**, and then click **OK**.
  
21. Click **Save**. When the association is completed, click **Close** to close the wizard.  
  
## Next steps

* To designate when to send notifications and the addresses to which the notifications should be sent to, review [How to Create Notification Subscribers](manage-notifications-create-subscribers.md)

* Create a [notification subscription](manage-notifications-create-subscriptions.md) to define the criteria, notification channel, and subscribers that will receive the notification.  
  
