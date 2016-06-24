---
title: How to Create Notification Templates
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98af143b-a337-440a-93e6-52f6857a74ef
---
# How to Create Notification Templates
You can use the following procedures to create notification templates for many types of information records or work items that Service Manager records or keeps track of, such as incidents, change requests, activities, release records, and configuration items. After you create the notification templates, you can use a notification subscription to send email messages based on the templates. The notification template determines the type and format of the messages to send.

> [!NOTE]
> Manually copying and pasting substitution strings from other notification templates will not generally work. Therefore, you should avoid copying them to prevent errors. Instead, you can easily browse for and insert available substitution strings into any notification template that you are creating or updating. For more information about using substitution strings in notification templates, see [About Substitution Strings in Notification Templates](About-Substitution-Strings-in-Notification-Templates.md).

The following two templates are prerequisites for other procedures:

-   The New Activity Assigned Received Template.

-   The New Standard Change Request Received Template.

> [!NOTE]
> In this release of Service Manager, notifications are sent only by email.

### To create a notification template for incidents

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Notifications**, and then click **Templates**.

3.  In the **Tasks** pane, under **Templates**, click **Create E-mail Template**.

4.  On the **General** page of the Create E-mail Notification Template Wizard, in the **Notification template name** box, type a name. For example, type **New E-mail Incident Template**. Optionally, in the **Description** box, you can type a description for the template that you are creating.

5.  Next to the **Targeted class** box, click **Browse**.

6.  In the **Choose Class** dialog box, click **Incident**, and then click **OK**.

7.  Make sure that an unsealed management pack of your choice is selected, and then click **Next**. For example, select the **Sample Management Pack**.

8.  On the **Template Design** page, in the **Message subject** box, type a subject for the email template. For example, type **New Incident created with ID#**. Then, click **Insert**.

9. In the **Select Property** dialog box, select **ID**, and then click **Add**.

10. In the **Message body** box, type a description to indicate that a new incident was opened for an email problem.

11. Use the other default values on this page, and then click **Next**.

12. On the **Summary** page, review the settings that you have selected for the template. Then, click **Create**.

13. On the **Completion** page, click **Close**.

### To create a notification template for change requests

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Notifications**, and then click **Templates**.

3.  In the **Tasks** pane, under **Templates**, click **Create E-mail Template**.

4.  On the **General** page of the Create E-mail Notification Template Wizard, in the **Notification template name** box, type a name. For example, type **New Standard Change Request Received Template**. Optionally, in the **Description** box, you can type a description for the template that you are creating.

5.  Next to the **Targeted class** box, click **Browse**.

6.  In the **Choose Class** dialog box, click **Change Request**, and then click **OK**.

7.  Make sure that an unsealed management pack of your choice is selected, and then click **Next**. For example, select the **Sample Management Pack**.

8.  On the **Template Design** page, in the **Message subject** box, type a subject for the email template. For example, type **New Standard Change Request with ID#**. Then, click **Insert**.

9. In the **Select Property** dialog box, select **ID**, and then click **Add**.

10. In the **Message body** box, type a description to indicate that a new standard change request was opened.

11. Use the other default values on this page, and then click **Next**.

12. On the **Summary** page, review the settings that you have selected for the template. Then, click **Create**.

13. On the **Completion** page, click **Close**.

### To create a notification template for a newly assigned activity

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Notifications**, and then click **Templates**.

3.  In the **Tasks** pane, under **Templates**, click **Create E-mail Template**.

4.  On the **General** page of the Create E-mail Notification Template Wizard, in the **Notification template name** box, type a name. For example, type **New Activity Assigned Received Template**. Optionally, in the **Description** box, you can type a description for the template that you are creating.

5.  Next to the **Targeted class** box, click **Browse**.

6.  In the **Select a Class** dialog box, click **Manual Activity**, and then click **OK**.

7.  Make sure that an unsealed management pack of your choice is selected, and then click **Next**. For example, select the **Sample Management Pack**.

8.  On the **Template Design** page, in the **Message subject** box, type a subject for the email template. For example, type **New Activity Assigned with ID#**. Then, click **Insert**.

9. In the **Select Property** dialog box, select **ID**, and then click **Add**.

10. In the **Message body** box, type a description to indicate that an activity has been assigned.

11. Use the other default values on this page, and then click **Next**.

12. On the **Summary** page, review the settings that you have selected for the template. Then, click **Create**.

13. On the **Completion** page, click **Close**.

### To validate template creation

-   Verify that the new template you created appears in the list of notification templates.

![](../../media/pssymbol.png)You can use Windows PowerShell commands to complete these and other related tasks, as follows:

-   For information about how to use Windows PowerShell to create a new Email template in Service Manager, see [New-SCSMEmailTemplate](http://go.microsoft.com/fwlink/p/?LinkID=225355).

-   For information about how to use Windows PowerShell to retrieve Email templates that are defined in Service Manager, see [Get-SCSMEmailTemplate](http://go.microsoft.com/fwlink/p/?LinkID=225323).

-   For information about how to use Windows PowerShell to retrieve the content of a Service Manager Email template, see [Get-SCSMEmailTemplateContent](http://go.microsoft.com/fwlink/p/?LinkID=225324).

-   For information about how to use Windows PowerShell to update properties of an Email template, see [Update-SCSMEmailtemplate](http://go.microsoft.com/fwlink/p/?LinkID=225384).

-   For information about how to use Windows PowerShell to remove an Email template from Service Manager, see [Remove-SCSMEmailTemplate](http://go.microsoft.com/fwlink/p/?LinkId=246064).


