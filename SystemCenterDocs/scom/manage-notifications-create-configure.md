---
ms.assetid: ab2991fd-8228-4afc-89c3-a380129d4a84
title:  Notification Action Account
description: This article provides information on how to create and configure the notification action account.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 02/27/2025
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
---

# How to create and configure the Notification action account


In System Center - Operations Manager, when an alert is generated, Operations Manager can notify designated individuals by email, instant message (IM), text message (SMS), or Microsoft Teams (applicable for 2022 and later). The Notification Account Run As profile is used to send notifications. For notifications to work correctly, you must create a Run As account that provides the credentials for sending notifications, and associate the Run As account to the Notification Account profile.  

## To create and configure the Notification action account  

1.  Sign in to the computer with a user account that's a member of the Operations Manager Administrators role.  

2.  In the Operations console, select **Administration**.  

3.  In the **Administration** workspace, right-click **Security**, and select **Create Run As Account**. Use the Create Run As Account Wizard to create an account to use as the Notification action account, which is used to send the notifications.  

4.  On the **Introduction** page, select **Next**.  

5.  On the **General Properties** page, select **Windows** in the **Run As Account type** list for setting up authentication with an email server in the same organization or domain or select **Simple Authentication** for setting up authentication with Microsoft Teams/external mail server, and then in **Display name**, enter **Notification action account**. Select **Next**.  

6.  On the **Credentials** page, enter the information for the user name, password, and domain (if required) of the user account that is to be used for notifications. Select **Next**.  

7.  Select the **More secure** distribution security option. For more information on this option, see [Distribution and Targeting for Run As Accounts and Profiles](manage-security-dist-target-runas-profiles.md).  

8.  Select **Create**.  

9. In the navigation pane, select **Accounts** under **Run As Configuration**.  

10. In the details pane, right-click **Notification action account**, and select **Properties**.  

11. On the **Distribution** tab, select **Add**.  

12. In the **Computer Search** window, select **Search** to display a name of available computers.  

13. Select the server(s) or resource pool(s) to distribute the credentials to, select **Add**, and then select **OK** to close the search window.  
> [!NOTE]
> The **Notifications Resource Pool** is normally used to allow all servers in the resource pool to access the credential.

14. Select **OK** to close the properties window.  

15. In the navigation pane, select **Profiles** under **Run As Configuration**.  

16. Right-click **Notification Account** and select **Properties**, which will open the **Run As Profile Wizard**.  

17. On the **Introduction** page, select **Next**.  

1. If you're configuring an internal email, then on the **General Properties** page, select **Next**. If you're configuring an external email, then right-click on **Profiles** and select **Create Run As Profile**. On the **General Properties** page, enter a suitable **Display name** and for **Select destination management pack**, choose **Notifications Internal Library** from the dropdown list.
> [!NOTE]
> The **Notifications Internal Library** Management Pack is required for External Email Authentication Run as profiles to be populated so you can select the profile you want to authenticate with in the SMTP Channel.

19. On the **Run As Accounts** page, select **Add**.  

20. In the **Add a Run As Account** window, in the **Run As account** dropdown list,  select the Run As account that you created earlier in this procedure. If you're configuring an internal email, accept the default **All targeted objects** and select **OK**. If you're configuring an external email, choose **A selected class, group, or object**, select **Select**, and choose **Class**. On the **Class Search** page, search and select **Alert Notification Subscription server**, and select **OK**.

21. Select **Save**. When the association is completed, select **Close** to close the wizard.  

## Next steps

* To designate when to send notifications and the addresses to which the notifications should be sent, review [How to Create Notification Subscribers](manage-notifications-create-subscribers.md).
* To define the criteria, notification channel, and subscribers that will receive the notification, create a [notification subscription](manage-notifications-create-subscriptions.md).


