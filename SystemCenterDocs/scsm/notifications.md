---
title: Configure Service Manager notifications
description: You can create notifications in Service Manager when incidents or changes occur.
ms.topic: how-to
author: Jeronika-MS
ms.author: v-gajeronika
ms.service: system-center
keywords:
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.subservice: service-manager
ms.assetid: a74d2677-96ac-44ac-8f45-12d2e24b0275
ms.custom:
  - UpdateFrequency3
  - engagement-fy24
  - sfi-image-nochange
---

# Configure notifications in Service Manager



Using Service Manager notifications, you can generate emails for almost any kind of change. For example, you can configure notifications to be sent to an analyst when changes occur to a work item or configuration item that pertains to email problems.

Before notifications are sent, first configure each notification channel, such as the settings for Simple Mail Transfer Protocol (SMTP). Notification messages are sent based on a notification template. Therefore, you must create a notification template. You can then use the Notification Subscription Wizard to subscribe a group of users to a notification that will be sent whenever the changes that you specify occur. Finally, you can verify that a notification is sent by manually generating the change.

> [!NOTE]
> You must add the Service Manager workflow account to the Service Manager Administrators user role for notifications to function properly.

## Substitution strings in notification templates

Substitution strings are special tokens or system variables that are used in notification templates in Service Manager. These strings retrieve properties from an instance that is related to the instance for which the template was created. The strings then display the value in the notification email. Notification templates in Service Manager include substitution strings. Although you should avoid modifying the predefined templates, you can duplicate them and then modify the duplicates.

For example, the end-user notification template includes a substitution string in the message body that represents the user's first name. If you want to add the user's last name, you can easily do so by using the **Insert** button, which is available when you edit a notification template, and then browsing the available strings that are available for the class of template that you're modifying. In this example, you would browse and then select **Affected User** and then select **Last Name** to insert the string into the template. Later, when the notification is sent to the user, their first and last name is included in the message as a salutation.

While this example is simple, Service Manager includes substitution strings for almost every property that you might need to create notifications that can inform end-users and other Service Manager users with very timely and relevant information. You can easily view the substitution strings that are available in Service Manager by opening an existing notification template and then, in the template design area, selecting the **Insert** button to view the classes and properties.

## Configure notification channels

You can use the following procedures to configure notification channels and validate the configuration. Notification channels are the method by which notification messages are sent to users. You use the **Configure E-Mail Notification Channel** dialog to configure and enable email notifications that Service Manager sends to a Simple Mail Transfer Protocol (SMTP) server.

> [!NOTE]
> Only email notification is supported.

### Configure email notifications

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Notifications**, and select **Channels**.
3. In the **Channels** pane, select **E-Mail Notification Channel**.
4. In the **Tasks** pane, under **E-Mail Notification Channel**, select **Properties** to open the **Configure E-Mail Notification Channel** dialog.
5. Select the **Enable e-mail notifications** checkbox.
6. Select **Add**. In the **Add SMTP Server** dialog, enter the fully qualified domain name (FQDN) of the SMTP server that you want to use. For example, enter **Exchange01.Woodgrove.Com**.
7. In the **Port number** box, enter or select the SMTP port number that you want to use. For example, select **25**.
8. In the **Authentication method** box, select either **Anonymous** or **Windows Integrated**. For example, select **Anonymous**. Then, select **OK**.
9. In the **Return e-mail address** box, enter the email address of the service account that is used during setup. For example, enter **smadmin\@woodgrove.com**.
10. In the **Retry primary after** box, enter or select the number of seconds that you want Service Manager to wait before it tries to resend outgoing email notifications. For example, select **25**.
11. Select **OK** to close the dialog.

### Validate email notification configuration

1. In the **Channels** pane, select **E-Mail Notification Channel**.
2. In the **Tasks** pane, under **E-Mail Notification Channel**, select **Properties** to open the **Configure E-Mail Notification Channel** dialog.
3. Verify that the configuration you entered is correct.

![Screenshot of PowerShell symbol.](./media/notifications/pssymbol.png)You can use a Windows PowerShell command to complete these tasks, as follows:

- For information about how to use Windows PowerShell to set the properties of an email notification channel in Service Manager, see [Set-SCSMChannel](/previous-versions/system-center/powershell/system-center-2012-r2/hh316236(v=sc.20)).
- For information about how to use Windows PowerShell to retrieve the Email Notification channels that are defined in Service Manager, see [Get-SCSMChannel](/previous-versions/system-center/powershell/system-center-2012-r2/hh316246(v=sc.20)).

::: moniker range=">=sc-sm-2022"

## Send notifications using external email authentication

Microsoft Entra ID implements OAuth protocol for secure authentication of its users and applications. Here's how the connection establishes when the activity runs:

1. Obtains user credentials from IP configuration.

2. Uses the credentials to authenticate with Azure AD using OAuth.

3. After authentication, you will receive an OAuth token from Azure AD.

4. Activity performs operations on the EWS endpoint using the OAuth token.

### Create an Azure AD app

To create an Azure AD app, do the following:

1. Sign in to the [Azure portal](https://go.microsoft.com/fwlink/?linkid=2083908) and search for [Microsoft Entra ID admin center](https://aad.portal.azure.com/).

2. On the **Microsoft Entra ID admin center** dashboard, select **Microsoft Entra ID**.

3. On the **Overview** page, under **Manage** > **App registrations**, select **New registration**.
     
      :::image type="App registrations page" source="media/notifications/app-registrations.png" alt-text="screenshot of app registrations page.":::

4. On the Register an application page, do the following:

     - **Name**: Enter the desired name.

     - **Supported account types**: Select the supported account type based on your scenario.

     - **Redirect URI (optional)**: From the **Select a platform** dropdown, select **Public client/native (mobile & desktop)**, and set the URI to https://login.microsoftonline.com/common/oauth2/nativeclient.
          
      :::image type="Register application page" source="media/notifications/register-application-inline.png" alt-text="screenshot of register an application page." lightbox="media/notifications/register-application-expanded.png":::

5. Select **Register**.

6. After successful registration, under **Overview** > **Essentials**, ensure to note the **Application (client) ID** and **Directory (tenant) ID**.

      :::image type="Overview essentials" source="media/notifications/overview-essentials.png" alt-text="screenshot of overview essentials page." lightbox="media/notifications/overview-essentials.png":::

7. On the **Overview** page, under **Manage**, select **Authentication**, and do the following:

     - Ensure that the **Platform configurations** is set to **Mobile and desktop applications** with at least https://login.microsoftonline.com/common/oauth2/nativeclient as one of the Redirect URIs. Shape screenshot of authentication page.

     - Under **Advanced settings**, ensure **Allow public client flows** is set to **Yes**.
     
          :::image type="Advanced settings" source="media/notifications/advanced-settings.png" alt-text="screenshot of advanced settings page.":::

8. Select **Save**.

9. On the **Overview** page, under **Manage**, select **API Permissions**.

10. On the **API permissions** page, select **Add a permission** > **APIs my organization uses**.

11. Enter **Office** in the search bar and select **Office 365 Exchange Online**, and then select **Delegated permissions** > **EWS** > **EWS.AccessAsUser.All** permission.
     
      :::image type="APIs used by organization" source="media/notifications/apis-used-by-my-organization.png" alt-text="screenshot of APIs used by organization."::: 

12. Remove redundant permissions and select **Grant admin consent**.
     
      :::image type="API permissions" source="media/notifications/api-permissions.png" alt-text="screenshot of API permissions.":::

### Enable TLS 1.2

To enable TLS 1.2, do the following:

1. Open Windows PowerShell in Administrator mode in Service Manager Console machine.

2. Run the following script to enable TLS 1.2 version.

     ```powershell
     New-Item 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319' -Force | Out-Null
     New-ItemProperty -path 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319' -name 'SystemDefaultTlsVersions' -value '1' -PropertyType 'DWord' -Force | Out-Null
     New-ItemProperty -path 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value '1' -PropertyType 'DWord' -Force | Out-Null
     New-Item 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -Force | Out-Null
     New-ItemProperty -path 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -name 'SystemDefaultTlsVersions' -value '1' -PropertyType 'DWord' -Force | Out-Null
     New-ItemProperty -path 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value '1' -PropertyType 'DWord' -Force | Out-Null
     New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Force | Out-Null
     New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'Enabled' -value '1' -PropertyType 'DWord' -Force | Out-Null
     New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'DisabledByDefault' -value 0 -PropertyType 'DWord' -Force | Out-Null
     New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Force | Out-Null
     New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'Enabled' -value '1' -PropertyType 'DWord' -Force | Out-Null
     New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'DisabledByDefault' -value 0 -PropertyType 'DWord' -Force | Out-Null
     Write-Host 'TLS 1.2 has been enabled. You must restart the Windows Server for the changes to take effect.' -ForegroundColor Cyan 
     ```

### Use OAuth for Notifications

To use OAuth for notifications, do the following:

1. Open the Service Manager Console and navigate to **Notifications** > **Channels** > **Properties**.

2. On the **Configure E-mail Notification Channel** pop-up, select **Enable e-mail notifications** checkbox, and select **Add**.

      :::image type="Email notification channel" source="media/notifications/email-notification-channel-inline.png" alt-text="screenshot of Email notification channel." lightbox="media/notifications/email-notification-channel-expanded.png":::

3. On the Add SMTP Server page, do the following:

     - **Authentication method**: Select **External E-mail Authentication** from the dropdown.

     - **Client Id**: Enter the client ID created in the previous steps.

     - **Tenant Id**: Enter the tenant ID created in the previous steps.

     - **Mail Id**: Enter the mail ID that acts as a sender for notifications.

     - **Password**: Enter the corresponding password.

      :::image type="Add SMTP server" source="media/notifications/add-smtp-server-inline.png" alt-text="screenshot of add SMTP server." lightbox="media/notifications/add-smtp-server-expanded.png":::

4. Select **OK** to save the changes.

5. Enter **Return e-mail address** and set **Retry primary after** as required and select **OK**.

Use this channel for sending notifications/outgoing e-mails.

An additional setup of connector/SMTP relay and SMTP details such as FQDN and port number are not required while you use External E-mail Authentication mode for sending notifications. Therefore, FQDN and port number values are set to random values as NA and 65534 when a channel is created using this authentication method.

### Troubleshooting

Each time Notification part runs, it logs events into the event viewer. In case of unexpected behavior, check events to troubleshoot. For more information or for debugging purposes, refer EWS Traces in events. To display trace and logs in the event viewer, open command prompt in administrator mode in the Service Manager Console machine and set the env var EXTERNALEWSLogs value to 1 (setx /m EXTERNALEWSLogs 1).

Setting EXTERNALEWSLogs to 1 enables trace and logs to be shown in event viewer as follows:

:::image type="Troubleshooting" source="media/notifications/troubleshooting-inline.png" alt-text="screenshot of troubleshooting." lightbox="media/notifications/troubleshooting-expanded.png":::

::: moniker-end

## Create notification templates

You can use the following procedures to create notification templates for many types of information records or work items that Service Manager records or keeps track of, such as incidents, change requests, activities, release records, and configuration items. After you create the notification templates, you can use a notification subscription to send email messages based on the templates. The notification template determines the type and format of the messages to send.

> [!NOTE]
> Manually copying and pasting substitution strings from other notification templates won't generally work. Therefore, you should avoid copying them to prevent errors. Instead, you can easily browse for and insert available substitution strings into any notification template that you're creating or updating.

The following two templates are prerequisites for other procedures:

- The New Activity Assigned Received Template.
- The New Standard Change Request Received Template.

> [!NOTE]
> Notifications are sent only by email.

### Create a notification template for incidents

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Notifications**, and select **Templates**.
3. In the **Tasks** pane, under **Templates**, select **Create E-mail Template**.
4. On the **General** page of the Create E-mail Notification Template Wizard, in the **Notification template name** box, enter a name. For example, enter **New E-mail Incident Template**. Optionally, in the **Description** box, you can enter a description for the template that you're creating.
5. Next to the **Targeted class** box, select **Browse**.
6. In the **Choose Class** dialog, select **Incident**, and select **OK**.
7. Ensure that an unsealed management pack of your choice is selected, and select **Next**. For example, select the **Sample Management Pack**.
8. On the **Template Design** page, in the **Message subject** box, enter a subject for the email template. For example, enter **New Incident created with ID#**. Then, select **Insert**.
9. In the **Select Property** dialog, select **ID**, and select **Add**.
10. In the **Message body** box, enter a description to indicate that a new incident was opened for an email problem.
11. Use the other default values on this page, and select **Next**.
12. On the **Summary** page, review the settings that you've selected for the template. Then, select **Create**.
13. On the **Completion** page, select **Close**.

### Create a notification template for change requests

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Notifications**, and select **Templates**.
3. In the **Tasks** pane, under **Templates**, select **Create E-mail Template**.
4. On the **General** page of the Create E-mail Notification Template Wizard, in the **Notification template name** box, enter a name. For example, enter **New Standard Change Request Received Template**. Optionally, in the **Description** box, you can enter a description for the template that you're creating.
5. Next to the **Targeted class** box, select **Browse**.
6. In the **Choose Class** dialog, select **Change Request**, and select **OK**.
7. Ensure that an unsealed management pack of your choice is selected, and select **Next**. For example, select the **Sample Management Pack**.
8. On the **Template Design** page, in the **Message subject** box, enter a subject for the email template. For example, enter **New Standard Change Request with ID#**. Then, select **Insert**.
9. In the **Select Property** dialog, select **ID**, and select **Add**.
10. In the **Message body** box, enter a description to indicate that a new standard change request was opened.
11. Use the other default values on this page, and select **Next**.
12. On the **Summary** page, review the settings that you've selected for the template. Then, select **Create**.
13. On the **Completion** page, select **Close**.

### Create a notification template for a newly assigned activity

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Notifications**, and select **Templates**.
3. In the **Tasks** pane, under **Templates**, select **Create E-mail Template**.
4. On the **General** page of the Create E-mail Notification Template Wizard, in the **Notification template name** box, enter a name. For example, enter **New Activity Assigned Received Template**. Optionally, in the **Description** box, you can enter a description for the template that you're creating.
5. Next to the **Targeted class** box, select **Browse**.
6. In the **Select a Class** dialog, select **Manual Activity**, and select **OK**.
7. Ensure that an unsealed management pack of your choice is selected, and select **Next**. For example, select the **Sample Management Pack**.
8. On the **Template Design** page, in the **Message subject** box, enter a subject for the email template. For example, enter **New Activity Assigned with ID#**. Then, select **Insert**.
9. In the **Select Property** dialog, select **ID**, and select **Add**.
10. In the **Message body** box, enter a description to indicate that an activity has been assigned.
11. Use the other default values on this page, and select **Next**.
12. On the **Summary** page, review the settings that you've selected for the template. Then, select **Create**.
13. On the **Completion** page, select **Close**.

### Validate template creation

- Verify that the new template you created appears in the list of notification templates.

![Screenshot of the PowerShell symbol.](./media/notifications/pssymbol.png)You can use Windows PowerShell commands to complete these and other related tasks, as follows:

- For information about how to use Windows PowerShell to create a new Email template in Service Manager, see [New-SCSMEmailTemplate](/previous-versions/system-center/powershell/system-center-2012-r2/hh316229(v=sc.20)).
- For information about how to use Windows PowerShell to retrieve Email templates that are defined in Service Manager, see [Get-SCSMEmailTemplate](/previous-versions/system-center/powershell/system-center-2012-r2/hh316234(v=sc.20)).
- For information about how to use Windows PowerShell to retrieve the content of a Service Manager Email template, see [Get-SCSMEmailTemplateContent](/previous-versions/system-center/powershell/system-center-2012-r2/hh316219(v=sc.20)).
- For information about how to use Windows PowerShell to update properties of an Email template, see [Update-SCSMEmailtemplate](/previous-versions/system-center/powershell/system-center-2012-r2/hh316235(v=sc.20)).
- For information about how to use Windows PowerShell to remove an Email template from Service Manager, see [Remove-SCSMEmailTemplate](/previous-versions/system-center/powershell/system-center-2012-r2/hh316216(v=sc.20)).

## Subscribe to notifications

After you create a notification template, and after you've enabled at least one notification channel, you can use the following procedure to subscribe to notifications by using the Notification Subscription Wizard. Then, notifications will be sent when an object is created or updated or periodically when other criteria that you specify are met.

The scenarios in this article center on the Create E-Mail Notification Subscription Wizard. The condition that you choose to notify will dynamically change the wizard pages that are available.

In the first procedure, you set up a subscription so that a messaging analyst is notified when a new incident that pertains to an email problem is opened. In the second procedure, you set up a subscription so that daily status updates are sent to the release manager while the HR web application is in development, testing, and deployment.

> [!NOTE]
> Some notification criteria values might not change. If you want to receive a notification when a change occurs, ensure that you choose a value for an object that is likely to change. For example, the **Incident ID** for an incident doesn't change.

### Create a notification subscription for an incident

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Notification**, and select **Subscriptions**.
3. In the **Tasks** pane, select **Create Subscription**.
4. On the **Before You Begin** page of the Create E-mail Notification Subscription Wizard, select **Next**.
5. On the **General** page, in the **Notification subscription name** box, enter a name. For example, enter **New Incident for E-mail Problem Notification Subscription**. Optionally, in the **Description** box, you can enter a description for the subscription that you're creating.
6. Next to the **Targeted class** box, select **Browse**.
7. In the **When to notify** box, select **When an object of the selected class is created**.
8. In the **Choose Class** dialog, choose a class. For example, select **Incident**. Then, select **OK**.
9. Ensure that an unsealed management pack of your choice is selected, and select **Next**. For example, select the **Sample Management Pack**.
10. On the **Additional Criteria** page, select **Incident**. In the **Available Properties** list, select **Classification Category**, and select **Add**.
11. On the **Additional Criteria** page, select the **Criteria** tab. In the **Criteria** area, next to **[Incident] Classification Category**, select **equals**. In the list, select **E-mail Problems**, and select **Next**.
12. On the **Template** page, next to the **E-mail template** box, select **Select**.
13. In the **Select Objects** dialog, in the **Templates** list, select a notification template. For example, select **New E-mail Incident Template**, select **OK**, and select **Next**.
14. On the **Recipient** page, select **Add**.
15. In the **Select Objects** dialog, search for the appropriate user, and then select the user. Select **Add**, select **OK**, and select **Next**. For example, select the user account for a messaging analyst or messaging administrator.

    > [!NOTE]
    > The notification address must be configured for the user account of the messaging analyst or messaging administrator.

16. On the **Related Recipients** page, select **Add**.
17. In the **Select Related Recipient** dialog, search for the appropriate class, and then select the appropriate substitution string that represents the user. Select **Add**, select **OK**, and select **Next**. For example, select additional user accounts that you want to send the notification to.
18. On the **Summary** page, review the settings that you selected for the notification subscription, and select **Create**.
19. On the **Completion** page, select **Close**.

### Create a periodic notification subscription for a release record

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Notifications**, and select **Subscriptions**.
3. In the **Tasks** pane, select **Create Subscription**.
4. On the **Before You Begin** page of the Create E-mail Notification Subscription Wizard, select **Next**.
5. On the **General** page, in the **Notification subscription name** box, enter a name. For example, enter **Daily Notification for Deploy HR Web 2.0 Release Record**. Optionally, in the **Description** box, you can enter a description for the subscription that you're creating. For example, enter **This subscription sends a daily notification of the status for the HR Web 2.0 release record**.
6. In the **When to notify** box, select **Periodically notify when objects meet a criteria**.
7. Next to the **Targeted class** box, select **Browse**.
8. In the **Choose Class** dialog, choose a class, and select **OK**. For example, select **Release Record**.
9. Ensure that an unsealed management pack of your choice is selected, and select **Next**. For example, select the **Sample Management Pack**.
10. On the **Additional Criteria** page, select **Release Record**. In the **Available Properties** list, select **Status**, and select **Add**.
11. In the **Criteria** area, next to **[Release Record] Status**, select **does not equal**. In the list, select **Closed**, and select **Next**.
12. On the **Recurring Notification** page under **Recurrence pattern**, select **Notify every *TimeInterval*** and then choose an interval. For example, set the recurrence pattern to every one day.
13. On the **Recurring Notification** page under **Range of recurrence**, select a range of recurrence or choose no end date. For example, select **No end date**.
14. On the **Template** page, next to the **E-mail template** box, select **Select**.
15. In the **Select Template** dialog, in the **Templates** list, select a notification template that you've created for release record notifications.
16. On the **Recipient** page, select **Add**.
17. In the **Select Objects** dialog, search for the appropriate user, and then select the user. Select **Add**, select **OK**, and select **Next**. For example, select the user account for the release manager.

    > [!NOTE]
    > The notification address must be configured for the user account of the messaging analyst or messaging administrator.

18. On the **Related Recipients** page, select **Add**.
19. In the **Select Related Recipient** dialog, search for the appropriate class, and then select the appropriate substitution string that represents the user. Select **Add**, select **OK**, and select **Next**. For example, select additional user accounts that you want to send the notification to.
20. On the **Summary** page, review the settings that you selected for the notification subscription, and select **Create**.
21. On the **Completion** page, select **Close**.

### Validate a notification subscription

- Locate the notification subscription that you created in the list of subscriptions.

![Screenshot of the PowerShell symbol.](./media/notifications/pssymbol.png)You can use a Windows PowerShell command to complete these tasks and other related tasks, as follows:

- For information about how to use Windows PowerShell to create a new subscription in Service Manager, see [New-SCSMSubscription](/previous-versions/system-center/powershell/system-center-2012-r2/hh316196(v=sc.20)).
- For information about how to use Windows PowerShell to retrieve subscriptions that are configured in Service Manager, see [Get-SCSMSubscription](/previous-versions/system-center/powershell/system-center-2012-r2/hh316211(v=sc.20)).
- For information about how to use Windows PowerShell to update subscription properties in Service Manager, see [Update-SCSMSubscription](/previous-versions/system-center/powershell/system-center-2012-r2/hh316242(v=sc.20)).
- For information about how to use Windows PowerShell to remove a subscription from Service Manager, see [Remove-SCSMSubscription](/previous-versions/system-center/powershell/system-center-2012-r2/hh316257(v=sc.20)).

## Verify a notification configuration

You can use the following procedure to verify that you've correctly configured notifications. Generate the type of change that activates the notification subscription that was previously created. When you do this, the subscription generates and then sends a notification. Receipt of the notification verifies success. For example, create a test incident that generates an email notification. The notification informs the recipient that an incident was opened.

If you're verifying a recurring notification subscription, you must wait for the time interval that you set previously to elapse until the notification is sent. When the notification is received, the configuration of the notification is verified.

To verify a notification configuration, follow these steps:

1. In the Service Manager console, select **Work Items**.
2. In the **Work Items** pane, expand **Work Items**, expand **Incident Management**, and select **All Open Incidents**.
3. In the **Tasks** pane, under **Incident Management**, select **Create Incident**.
4. In the **Incident *Number* New** form, enter the required information in the **Affected user**, **Title**, **Classification Category**, **Impact**, and **Urgency** boxes.
5. In the **Classification Category** list, select **E-mail Problems**, and select **OK**.
6. Verify that an email notification that contains the information you entered in the template is received. The email title should contain the incident ID number.

## Automatically notify groups of Service Manager users

In some situations, you may want to use a group rather than an individual user in Service Manager as a work item stakeholder. For example, you might want to assign an incident to a team of people, such as an initial response team that routes incidents, and then notify everyone in the initial response team that an incident has been assigned to their team.

Messaging-enabled universal security groups in Microsoft Exchange Server are the key to this task. This article describes how to accomplish this using the Exchange Server Exchange Management console for incidents. You can use the following procedures to create a messaging-enabled universal security group, create a workflow to notify stakeholders when an incident is created, and then test for success.

In Exchange Server, the **Require that all senders are authenticated** setting is enabled by default for mail-enabled universal security groups. You can modify the setting in the distribution group properties, in Mail-Flow settings, in the **Message Delivery Restrictions** dialog. If your outgoing Simple Mail Transfer Protocol (SMTP) server specified in the Service Manager settings (Under **Administration** > **Notifications Channels** > **Edit**) is using Anonymous as the Authentication Method (either in  Service Manager or the SMTP settings), then given the above default setting in exchange, the email wouldn't be sent out. If you've Anonymous Access configured on the SMTP side, it's necessary either to clear the **Require that all senders are authenticated** setting in exchange for the Mail Enabled Universal Security Group, or change the SMTP authentication settings (in Service Manager or the outgoing SMTP Server settings) from anonymous to Windows Integrated, so that the user is authenticated, allowing the email to be sent.

As an alternative, you can avoid using **Assigned to** and instead use **Support Group** changing as a triggering field. To set this up, create a new email notification subscription, and under additional criteria, use the following:

- Changed from: [incident] Support Group Does not equal Tier 1
- Changed to: [incident] Support Group equals Tier 1

Use whatever template you want, and add the recipient of the mailing distribution list for Tier 1. Now Tier 1 is notified whenever a ticket is sent to them, even if it's done by means of a template at portal ticket creation.

Setting up one of these for each support group will ensure that all your groups are informed of incoming incidents that require their attention.

### Create a messaging-enabled universal security group

1. In the Exchange Management Console, navigate to **Recipient Configuration**, right-click **Distribution Group**, and select **New Distribution Group**.
2. On the **Introduction** page, either choose an existing universal group or create a new group.
3. On the **Group Information** page, select the **Security** group type.
4. Complete the creation of the group.
5. Add members to the group by right-clicking them, selecting **Properties**, and accessing the **Members** tab.
6. Wait for Service Manager to sync with Active Directory Domain Services (AD DS), or perform a manual Synchronization from **Administration** > **Connectors**. (Select **AD Connector**, and then select the **Synchronize Now** task on the right-hand side).
7. Once the Active Directory synchronization has completed, the newly created group will be available as a configuration item in Service Manager, and it can be selected in the user picker fields, such as **Affected User** and **Assigned To**.

### Create a workflow to notify stakeholders when an incident is created

1. Navigate to **Administration** > **Workflows** > **Configuration**.
2. Double-click **Incident Event Workflow Configuration**.
3. Select **Add**, and select **Next** on the **Before you Begin** page.
4. Give the workflow a name, such as *Incident Created Email Stakeholders*.
5. Leave the default of **When an incident is created** in the **Check for Events** dropdown list.
6. Select one of your custom management packs (or create one) to store the workflow in, and select **Next**.
7. Select **Next** on the **Specify Incident Criteria** page. (We want this workflow to run when any new incident is created.)
8. Optionally, apply a template. (In this case, we're creating the workflow for notification only, so we choose **Do not apply a template**.)
9. In the **Select People to Notify** dialog, select the **Enable notification** checkbox. Add the appropriate users you want to notify with the appropriate templates.
10. Select Next, and select **Create** to complete creation of the workflow.

### Test the workflow and mail the enabled universal security group

- Create an incident and assign it to the messaging-enabled universal security group that you created earlier.

## Next steps

- [Use the service catalog to offer services](service-catalog.md).
