---
title: How to Create and Configure the Notification Action Account
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4801a5a-5830-48ca-85ee-3a6095600902
---
# How to Create and Configure the Notification Action Account
In [!INCLUDE[om12long](Token/om12long_md.md)], when an alert is generated, Operations Manager can notify designated individuals by email, instant message \(IM\), or text message \(SMS\). The Notification Account Run As profile is used to send notifications. For notifications to work correctly, you must create a Run As account that provides the credentials for sending notifications and associate the Run As account to the Notification Account profile.

### To create and configure the notification action account

1.  Log on to the computer with a user account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Administration**.

3.  In the **Administration** workspace, right\-click **Security**, and then click **Create Run As Account**. Use the Create Run As Account Wizard to create an account to use as the Notification action account, which is used to send the notifications.

4.  On the **Introduction** page, click **Next**.

5.  On the **General Properties** page, select **Windows** in the **Run As Account type** list, and then in **Display name**, type **Notification action account**. Click **Next**.

6.  On the **Credentials** page, type the information for the user name, password, and domain of the user account that to be used for notifications. Click **Next**.

7.  Select the **More secure** distribution security option. For more information on this option, see [Distribution and Targeting for Run As Accounts and Profiles](Distribution-and-Targeting-for-Run-As-Accounts-and-Profiles.md).

8.  Click **Create**.

9. In the navigation pane, click **Accounts** under **Run As Configuration**.

10. In the details pane, right\-click **Notification action account**, and then click **Properties**.

11. On the **Distribution** tab, click **Add**.

12. In the **Computer Search** window, click **Search** to display a name of available computers.

13. Select the server or servers to distribute the credentials to, click **Add**, and then click **OK** to close the search window.

14. Click **OK** to close the properties window.

15. In the navigation pane, click **Profiles** under **Run As Configuration**.

16. Right\-click **Notification Account** and click **Properties**, which will open the **Run As Profile Wizard**.

17. On the **Introduction** page, click **Next**.

18. On the **General Properties** page, click **Next**.

19. On the **Run As Accounts** page, click **Add**.

20. In the **Add a Run As Account** window, in the **Run As account** dropdown menu, select the Run As account that you created earlier in this procedure. Accept the default of **All targeted objects** and then click **OK**.

21. Click **Save**. When the association is completed, click **Close** to close the wizard.

## See Also
[How to Enable an Email Notification Channel](How-to-Enable-an-Email-Notification-Channel.md)
[How to Enable an Instant Message Notification Channel](How-to-Enable-an-Instant-Message-Notification-Channel.md)
[How to Enable a Text Message &#40;SMS&#41; Notification Channel](How-to-Enable-a-Text-Message--SMS--Notification-Channel.md)
[How to Enable a Command Notification Channel](How-to-Enable-a-Command-Notification-Channel.md)
[How to Create Notification Subscribers](How-to-Create-Notification-Subscribers.md)
[How to Create Notification Subscriptions](How-to-Create-Notification-Subscriptions.md)
[How to Customize Message Content for Notifications](How-to-Customize-Message-Content-for-Notifications.md)
[How to Subscribe to Notifications from an Alert](How-to-Subscribe-to-Notifications-from-an-Alert.md)
[How to Create Subscriptions Using Classes and Groups](How-to-Create-Subscriptions-Using-Classes-and-Groups.md)
[How to Specify Which Alerts Generate Notifications &#40;Conditions&#41;](How-to-Specify-Which-Alerts-Generate-Notifications--Conditions-.md)
[Sending Notifications for Specific Computers and Specific Alerts to Specific Teams](Sending-Notifications-for-Specific-Computers-and-Specific-Alerts-to-Specific-Teams.md)


