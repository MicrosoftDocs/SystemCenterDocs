---
title: Configure Service Manager notifications
description: You can create notifications in Service Manager when incidents or changes occur.
manager: carmonm
ms.topic: article
author: bandersmsft
ms.author: banders
ms.prod: system-center-2016
keywords:  
ms.date: 02/15/2016
ms.technology: service-manager
ms.assetid: a74d2677-96ac-44ac-8f45-12d2e24b0275
---

# Configure notifications in Service Manager

>Applies To: System Center 2016 - Service Manager

Using Service Manager notifications, you can generate emails for almost any kind of change. For example, you can configure notifications to be sent to an analyst when changes occur to a work item or configuration item that pertains to email problems.

Before notifications are sent, first configure each notification channel, such as the settings for Simple Mail Transfer Protocol (SMTP). Notification messages are sent based on a notification template. Therefore, you must create a notification template. You can then use the Notification Subscription Wizard to subscribe a group of users to a notification that will be sent whenever the changes that you specify occur. Finally, you can verify that a notification is sent by manually generating the change.

> [!NOTE]
> You must add the Service Manager workflow account to the Service Manager Administrators user role for notifications to function properly.

## Substitution strings in notification templates

Substitution strings are special tokens or system variables that are used in notification templates in Service Manager. These strings retrieve properties from an instance that is related to the instance for which the template was created. The strings then display the value in the notification email. Notification templates in Service Manager include substitution strings. Although you should avoid modifying the predefined templates, you can duplicate them and then modify the duplicates.

For example, the end user notification template includes a substitution string in the message body that represents the user's first name. If you want to add the user's last name, you can easily do so by using the **Insert** button, which is available when you edit a notification template, and then browsing the available strings that are available for the class of template that you are modifying. In this example, you would browse and then select **Affected User** and then select **Last Name** to insert the string into the template. Later, when the notification is sent to the user, his or her first and last name is included in the message as a salutation.

While this example is very simple, Service Manager includes substitution strings for almost every property that you might need to create notifications that can inform end users and other Service Manager users with very timely and relevant information. You can easily view the substitution strings that are available in Service Manager by opening an existing notification template and then, in the template design area, clicking the **Insert** button to view the classes and properties.


## Configure notification channels

You can use the following procedures to configure notification channels and validate the configuration. Notification channels are the method by which notification messages are sent to users. You use the **Configure E-Mail Notification Channel** dialog box to configure and enable email notifications that Service Manager sends to a Simple Mail Transfer Protocol (SMTP) server.

> [!NOTE]
> Only email notification is supported.

### To configure email notifications

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Notifications**, and then click **Channels**.
3.  In the **Channels** pane, click **E-Mail Notification Channel**.
4.  In the **Tasks** pane, under **E-Mail Notification Channel**, click **Properties** to open the **Configure E-Mail Notification Channel** dialog box.
5.  Select the **Enable e-mail notifications** check box.
6.  Click **Add**. In the **Add SMTP Server** dialog box, type the fully qualified domain name (FQDN) of the SMTP server that you want to use. For example, type **Exchange01.Woodgrove.Com**.
7.  In the **Port number** box, type or select the SMTP port number that you want to use. For example, select **25**.
8.  In the **Authentication method** box, select either **Anonymous** or **Windows Integrated**. For example, select **Anonymous**. Then, click **OK**.
9. In the **Return e-mail address** box, type the email address of the service account that is used during setup. For example, type **smadmin@woodgrove.com**.
10. In the **Retry primary after** box, type or select the number of seconds that you want Service Manager to wait before it tries to resend outgoing email notifications. For example, select **25**.
11. Click **OK** to close the dialog box.

### To validate email notification configuration

1.  In the **Channels** pane, click **E-Mail Notification Channel**.
2.  In the **Tasks** pane, under **E-Mail Notification Channel**, click **Properties** to open the **Configure E-Mail Notification Channel** dialog box.
3.  Verify that the configuration you entered is correct.

![PowerShell symbol](./media/notifications/pssymbol.png)You can use a Windows PowerShell command to complete these tasks, as follows:

-   For information about how to use Windows PowerShell to set the properties of an email notification channel in Service Manager, see [Set-SCSMChannel](http://go.microsoft.com/fwlink/p/?LinkId=225375).
-   For information about how to use Windows PowerShell to retrieve the Email Notification channels that are defined in Service Manager, see [Get-SCSMChannel](http://go.microsoft.com/fwlink/p/?LinkId=225319).

## Create notification templates

You can use the following procedures to create notification templates for many types of information records or work items that Service Manager records or keeps track of, such as incidents, change requests, activities, release records, and configuration items. After you create the notification templates, you can use a notification subscription to send email messages based on the templates. The notification template determines the type and format of the messages to send.

> [!NOTE]
> Manually copying and pasting substitution strings from other notification templates will not generally work. Therefore, you should avoid copying them to prevent errors. Instead, you can easily browse for and insert available substitution strings into any notification template that you are creating or updating. For more information about using substitution strings in notification templates, see [About Substitution Strings in Notification Templates](sub-strings.md).

The following two templates are prerequisites for other procedures:

-   The New Activity Assigned Received Template.
-   The New Standard Change Request Received Template.

> [!NOTE]
> Notifications are sent only by email.

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

![PowerShell symbol](./media/notifications/pssymbol.png)You can use Windows PowerShell commands to complete these and other related tasks, as follows:

-   For information about how to use Windows PowerShell to create a new Email template in Service Manager, see [New-SCSMEmailTemplate](http://go.microsoft.com/fwlink/p/?LinkID=225355).
-   For information about how to use Windows PowerShell to retrieve Email templates that are defined in Service Manager, see [Get-SCSMEmailTemplate](http://go.microsoft.com/fwlink/p/?LinkID=225323).
-   For information about how to use Windows PowerShell to retrieve the content of a Service Manager Email template, see [Get-SCSMEmailTemplateContent](http://go.microsoft.com/fwlink/p/?LinkID=225324).
-   For information about how to use Windows PowerShell to update properties of an Email template, see [Update-SCSMEmailtemplate](http://go.microsoft.com/fwlink/p/?LinkID=225384).
-   For information about how to use Windows PowerShell to remove an Email template from Service Manager, see [Remove-SCSMEmailTemplate](http://go.microsoft.com/fwlink/p/?LinkId=246064).

## Subscribe to notifications

After you create a notification template, and after you have enabled at least one notification channel, you can use the following procedure to subscribe to notifications by using the Notification Subscription Wizard. Then, notifications will be sent when an object is created or updated or periodically when other criteria that you specify are met.

The scenarios in this topic center on the Create E-Mail Notification Subscription Wizard. The condition that you choose to notify will dynamically change the wizard pages that are available.

In the first procedure, you set up a subscription so that a messaging analyst is notified when a new incident that pertains to an email problem is opened. In the second procedure, you set up a subscription so that daily status updates are sent to the release manager while the HR web application is in development, testing, and deployment.

> [!NOTE]
> Some notification criteria values might not change. If you want to receive a notification when a change occurs, make sure that you choose a value for an object that is likely to change. For example, the **Incident ID** for an incident does not change.

### To create a notification subscription for an incident

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Notification**, and then click **Subscriptions**.
3.  In the **Tasks** pane, click **Create Subscription**.
4.  On the **Before You Begin** page of the Create E-mail Notification Subscription Wizard, click **Next**.
5.  On the **General** page, in the **Notification subscription name** box, type a name. For example, type **New Incident for E-mail Problem Notification Subscription**. Optionally, in the **Description** box, you can type a description for the subscription that you are creating.
6.  Next to the **Targeted class** box, click **Browse**.
7.  In the **When to notify** box, select **When an object of the selected class is created**.
8.  In the **Choose Class** dialog box, choose a class. For example, click **Incident**. Then, click **OK**.
9. Make sure that an unsealed management pack of your choice is selected, and then click **Next**. For example, select the **Sample Management Pack**.
10. On the **Additional Criteria** page, select **Incident**. In the **Available Properties** list, select **Classification Category**, and then click **Add**.
11. On the **Additional Criteria** page, click the **Criteria** tab. In the **Criteria** area, next to **[Incident] Classification Category**, select **equals**. In the list, select **E-mail Problems**, and then click **Next**.
12. On the **Template** page, next to the **E-mail template** box, click **Select**.
13. In the **Select Objects** dialog box, in the **Templates** list, select a notification template. For example, select **New E-mail Incident Template**, click **OK**, and then click **Next**.
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
4.  On the **Before You Begin** page of the Create E-mail Notification Subscription Wizard, click **Next**.
5.  On the **General** page, in the **Notification subscription name** box, type a name. For example, type **Daily Notification for Deploy HR Web 2.0 Release Record**. Optionally, in the **Description** box, you can type a description for the subscription that you are creating. For example, type **This subscription sends a daily notification of the status for the HR Web 2.0 release record**.
6.  In the **When to notify** box, select **Periodically notify when objects meet a criteria**.
7.  Next to the **Targeted class** box, click **Browse**.
8.  In the **Choose Class** dialog box, choose a class, and then click **OK**. For example, click **Release Record**.
9. Make sure that an unsealed management pack of your choice is selected, and then click **Next**. For example, select the **Sample Management Pack**.
10. On the **Additional Criteria** page, select **Release Record**. In the **Available Properties** list, select **Status**, and then click **Add**.
11. In the **Criteria** area, next to **[Release Record] Status**, select **does not equal**. In the list, select **Closed**, and then click **Next**.
12. On the **Recurring Notification** page under **Recurrence pattern**, select **Notify every *TimeInterval*** and then choose an interval. For example, set the recurrence pattern to every 1 day.
13. On the **Recurring Notification** page under **Range of recurrence**, select a range of recurrence or choose no end date. For example, select **No end date**.
14. On the **Template** page, next to the **E-mail template** box, click **Select**.
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

![PowerShell symbol](./media/notifications/pssymbol.png)You can use a Windows PowerShell command to complete these tasks and other related tasks, as follows:

-   For information about how to use Windows PowerShell to create a new subscription in Service Manager, see [New-SCSMSubscription](http://go.microsoft.com/fwlink/p/?LinkID=225359).
-   For information about how to use Windows PowerShell to retrieve subscriptions that are configured in Service Manager, see [Get-SCSMSubscription](http://go.microsoft.com/fwlink/p/?LinkID=225333).
-   For information about how to use Windows PowerShell to update subscription properties in Service Manager, see [Update-SCSMSubscription](http://go.microsoft.com/fwlink/p/?LinkID=225388).
-   For information about how to use Windows PowerShell to remove a subscription from Service Manager, see [Remove-SCSMSubscription](http://go.microsoft.com/fwlink/p/?LinkID=225370).

## Verify a notification configuration

You can use the following procedure to verify that you have correctly configured notifications. Generate the type of change that activates the notification subscription that was previously created. When you do this, the subscription generates and then sends a notification. Receipt of the notification verifies success. For example, create a test incident that generates an email notification. The notification informs the recipient that an incident was opened.

If you are verifying a recurring notification subscription, you must wait for the time interval that you set previously to elapse until the notification is sent. When the notification is received, the configuration of the notification is verified.

### To verify a notification configuration

1.  In the Service Manager console, click **Work Items**.
2.  In the **Work Items** pane, expand **Work Items**, expand **Incident Management**, and then click **All Open Incidents**.
3.  In the **Tasks** pane, under **Incident Management**, click **Create Incident**.
4.  In the **Incident *Number* New** form, enter the required information in the **Affected user**, **Title**, **Classification Category**, **Impact**, and **Urgency** boxes.
5.  In the **Classification Category** list, select **E-mail Problems**, and then click **OK**.
6.  Verify that an email notification that contains the information you entered in the template is received. The email title should contain the incident ID number.

## Automatically notify groups of Service Manager users

In some situations, you may want to use a group rather than an individual user in Service Manager as a work item stakeholder. For example, you might want to assign an incident to a team of people, such as an initial response team that routes incidents, and then notify everyone in the initial response team that an incident has been assigned to their team.

Messaging-enabled universal security groups in Microsoft Exchange Server are the key to this task. This topic describes how to accomplish this using the Exchange Server Exchange Management console for incidents. You can use the following procedures to create a messaging-enabled universal security group, create a workflow to notify stakeholders when an incident is created, and then test for success.

In Exchange Server, the **Require that all senders are authenticated** setting is enabled by default for mail-enabled universal security groups. You can modify the setting in the distribution group properties, in Mail-Flow settings, in the **Message Delivery Restrictions** dialog box. If your outgoing Simple Mail Transfer Protocol (SMTP) server specified in the Service Manager settings (Under **Administration** > **Notifications Channels** > **Edit**) is using Anonymous as the Authentication Method (either in  Service Manager or the SMTP settings), then given the above default setting in exchange, the email would not be sent out. If you have Anonymous Access configured on the SMTP side, it is necessary either to clear the **Require that all senders are authenticated** setting in exchange for the Mail Enabled Universal Security Group, or change the SMTP authentication settings (in Service Manager or the outgoing SMTP Server settings) from anonymous to Windows Integrated, so that the user is authenticated, allowing the email to be sent.

As an alternative, you can avoid using **Assigned to** and instead use **Support Group** changing as a triggering field. To set this up, create a new email notification subscription, and under additional criteria, use the following:

-   Changed from: [incident] Support Group Does not equal Tier 1
-   Changed to: [incident] Support Group equals Tier 1

Use whatever template you want, and add the recipient of the mailing distribution list for Tier 1. Now Tier 1 is notified whenever a ticket is set to them, even if it is done by means of a template at portal ticket creation.

Setting up one of these for each support group will ensure that all your groups are informed of incoming incidents that require their attention.

### To create a messaging-enabled universal security group

1.  In the Exchange Management Console, navigate to **Recipient Configuration**, right-click **Distribution Group**, and then click **New Distribution Group**.
2.  On the **Introduction** page, either choose an existing universal group or create a new group.
3.  On the **Group Information** page, select the **Security** group type.
4.  Complete the creation of the group.
5.  Add members to the group by right-clicking them, clicking **Properties**, and accessing the **Members** tab.
6.  Wait for Service Manager to sync with Active Directory Domain Services (AD DS), or perform a manual Synchronization from **Administration** > **Connectors**. (Click **AD Connector**, and then click the **Synchronize Now** task on the right-hand side).
7.  Once the Active Directory synchronization has completed, the newly created group will be available as a configuration item in Service Manager, and it can be selected in the user picker fields, such as **Affected User** and **Assigned To**.

### To create a workflow to notify stakeholders when an incident is created

1.  Navigate to **Administration** > **Workflows** > **Configuration**.
2.  Double-click **Incident Event Workflow Configuration**.
3.  Click **Add**, and then click **Next** on the **Before you Begin** page.
4.  Give the workflow a name, such as *Incident Created Email Stakeholders*.
5.  Leave the default of **When an incident is created** in the **Check for Events** drop-down list.
6.  Select one of your custom management packs (or create one) to store the workflow in, and then click **Next**.
7.  Click **Next** on the **Specify Incident Criteria** page. (We want this workflow to run when any new incident is created.)
8.  Optionally, apply a template. (In this case we are creating the workflow for notification only, so we choose **Do not apply a template**.)
9. In the **Select People to Notify** dialog box, select the **Enable notification** check box. Add the appropriate users you want to notify with the appropriate templates.
10. Click Next, and then click **Create** to complete creation of the workflow.

### To test the workflow and mail the enabled universal security group

- Create an incident and assign it to the messaging-enabled universal security group that you created earlier.
