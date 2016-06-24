---
title: How to Send SLA Notification Information to the Assigned-To User
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 72980e7a-58c2-44d3-8a99-db3776c8abfb
---
# How to Send SLA Notification Information to the Assigned-To User
In Service Manager, you can send notifications to analysts who are responsible for incidents when each incident is within the warning period of its service level objective. Because periodic notifications require a large amount of system resources, the following example notifies the analyst once when the service level objective goes to a warning state.

### To send an SLA notification to the assigned-to user

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Notifications**, and then click **Subscriptions**.

3.  In the **Tasks** pane, click **Create Subscription** to open the Create E-Mail Notification Subscription Wizard.

4.  On the **Before You Begin** page, read the instructions, and then click **Next**.

5.  On the **General** page, complete these steps:

    1.  In the **Notification subscription name** box, type a name for the subscription for the service level objective.

    2.  In the **Description** box, type a description of the subscription for the service level objective.

    3.  In the **When to notify** list, select **When an object of the selected class is updated**.

    4.  Next to **Targeted class** click **Browse** and then in then in the **Frequently used basic classes** list, select **All basic classes**. In the **Select a Class** dialog box, click **Service Level Instance Time Information**, and then click **OK** to close the dialog box.

    5.  Keep the default management pack information, and then click **Next**.

6.  On the **Group/Queue Selection** page, click **Next**.

7.  On the **Additional Criteria** page, complete these steps:

    1.  In the **Changed From** tab, set **[Service Level Instance Time Information] Status Does Not Equal Warning**.

    2.  On the **Changed To** tab, set **[Service Level Instance Time Information] Status Equals Warning**, and then click **Next**.

8.  On the **Template** page, select an email template or create a new one targeted at the Service Level Instance Time Information class. For more information about creating email notification templates, see [How to Create Notification Templates](How-to-Create-Notification-Templates.md). Click **Next**.

9. On the **Recipient** page, click **Add** and select the groups and users to send the notification to, and then click **Next**.

10. On the **Related Recipient** page, click **Add**, select **[WorkItem]WorkItem has Service Level Instance Information** in the left box, and then select **Primary Owner** and **Assigned To User** in the right box, and then click **Next**.

11. On the **Summary** page, review the information, and then click **Create**.

12. On the **Completion** page, click **OK** to close the wizard.


