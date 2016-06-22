---
title: How to Subscribe to Notifications
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a52f6f49-795a-43d1-a6d6-d86140c7d9d6
---
# How to Subscribe to Notifications
After you create a notification template, and after you have enabled at least one notification channel, you can use the following procedure to subscribe to notifications by using the Notification Subscription Wizard. Then, notifications will be sent when an object is created or updated or periodically when other criteria that you specify are met.

The scenarios in this topic center on the Create E\-Mail Notification Subscription Wizard. The condition that you choose to notify will dynamically change the wizard pages that are available.

In the first procedure, you set up a subscription so that a messaging analyst is notified when a new incident that pertains to an email problem is opened. In the second procedure, you set up a subscription so that daily status updates are sent to the release manager while the HR web application is in development, testing, and deployment.

> [!NOTE]
> Some notification criteria values might not change. If you want to receive a notification when a change occurs, make sure that you choose a value for an object that is likely to change. For example, the **Incident ID** for an incident does not change.

### To create a notification subscription for an incident

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Notification**, and then click **Subscriptions**.

3.  In the **Tasks** pane, click **Create Subscription**.

4.  On the **Before You Begin** page of the Create E\-mail Notification Subscription Wizard, click **Next**.

5.  On the **General** page, in the **Notification subscription name** box, type a name. For example, type **New Incident for E\-mail Problem Notification Subscription**. Optionally, in the **Description** box, you can type a description for the subscription that you are creating.

6.  Next to the **Targeted class** box, click **Browse**.

7.  In the **When to notify** box, select **When an object of the selected class is created**.

8.  In the **Choose Class** dialog box, choose a class. For example, click **Incident**. Then, click **OK**.

9. Make sure that an unsealed management pack of your choice is selected, and then click **Next**. For example, select the **Sample Management Pack**.

10. On the **Additional Criteria** page, select **Incident**. In the **Available Properties** list, select **Classification Category**, and then click **Add**.

11. On the **Additional Criteria** page, click the **Criteria** tab. In the **Criteria** area, next to **\[Incident\] Classification Category**, select **equals**. In the list, select **E\-mail Problems**, and then click **Next**.

12. On the **Template** page, next to the **E\-mail template** box, click **Select**.

13. In the **Select Objects** dialog box, in the **Templates** list, select a notification template. For example, select **New E\-mail Incident Template**, click **OK**, and then click **Next**.

14. On the **Recipient** page, click **Add**.

15. In the **Select Objects** dialog box, search for the appropriate user, and then select the user. Click **Add**, click **OK**, and then click **Next**. For example, select the user account for a messaging analyst or messaging administrator.

    > [!NOTE]
    > The notification address must be configured for the user account of the messaging analyst or messaging administrator.

16. On the **Related Recipients** page, click **Add**.

17. In the **Select Related Recipient** dialog box, search for the appropriate class, and then select the appropriate substitution string that represents the user. Click **Add**, click **OK**, and then click **Next**. For example, select additional user accounts that you want to send the notification to.

18. On the **Summary** page, review the settings that you selected for the notification subscription, and then click **Create**.

19. On the **Completion** page, click **Close**.

### To create a periodic notification subscription for a release record

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Notifications**, and then click **Subscriptions**.

3.  In the **Tasks** pane, click **Create Subscription**.

4.  On the **Before You Begin** page of the Create E\-mail Notification Subscription Wizard, click **Next**.

5.  On the **General** page, in the **Notification subscription name** box, type a name. For example, type **Daily Notification for Deploy HR Web 2.0 Release Record**. Optionally, in the **Description** box, you can type a description for the subscription that you are creating. For example, type **This subscription sends a daily notification of the status for the HR Web 2.0 release record**.

6.  In the **When to notify** box, select **Periodically notify when objects meet a criteria**.

7.  Next to the **Targeted class** box, click **Browse**.

8.  In the **Choose Class** dialog box, choose a class, and then click **OK**. For example, click **Release Record**.

9. Make sure that an unsealed management pack of your choice is selected, and then click **Next**. For example, select the **Sample Management Pack**.

10. On the **Additional Criteria** page, select **Release Record**. In the **Available Properties** list, select **Status**, and then click **Add**.

11. In the **Criteria** area, next to **\[Release Record\] Status**, select **does not equal**. In the list, select **Closed**, and then click **Next**.

12. On the **Recurring Notification** page under **Recurrence pattern**, select **Notify every \<TimeInterval\>** and then choose an interval. For example, set the recurrence pattern to every 1 day.

13. On the **Recurring Notification** page under **Range of recurrence**, select a range of recurrence or choose no end date. For example, select **No end date**.

14. On the **Template** page, next to the **E\-mail template** box, click **Select**.

15. In the **Select Template** dialog box, in the **Templates** list, select a notification template that you have created for release record notifications.

16. On the **Recipient** page, click **Add**.

17. In the **Select Objects** dialog box, search for the appropriate user, and then select the user. Click **Add**, click **OK**, and then click **Next**. For example, select the user account for the release manager.

    > [!NOTE]
    > The notification address must be configured for the user account of the messaging analyst or messaging administrator.

18. On the **Related Recipients** page, click **Add**.

19. In the **Select Related Recipient** dialog box, search for the appropriate class, and then select the appropriate substitution string that represents the user. Click **Add**, click **OK**, and then click **Next**. For example, select additional user accounts that you want to send the notification to.

20. On the **Summary** page, review the settings that you selected for the notification subscription, and then click **Create**.

21. On the **Completion** page, click **Close**.

### To validate a notification subscription

-   Locate the notification subscription that you created in the list of subscriptions.

![](../../media/pssymbol.png)You can use a Windows PowerShell command to complete these tasks and other related tasks, as follows:

-   For information about how to use Windows PowerShell to create a new subscription in Service Manager, see [New\-SCSMSubscription](http://go.microsoft.com/fwlink/p/?LinkID=225359).

-   For information about how to use Windows PowerShell to retrieve subscriptions that are configured in Service Manager, see [Get\-SCSMSubscription](http://go.microsoft.com/fwlink/p/?LinkID=225333).

-   For information about how to use Windows PowerShell to update subscription properties in Service Manager, see [Update\-SCSMSubscription](http://go.microsoft.com/fwlink/p/?LinkID=225388).

-   For information about how to use Windows PowerShell to remove a subscription from Service Manager, see [Remove\-SCSMSubscription](http://go.microsoft.com/fwlink/p/?LinkID=225370).


