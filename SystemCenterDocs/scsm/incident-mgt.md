---
title: Configure Incident Management in Service Manager
description: Learn about how to configure Incident Management in Service Manager.
ms.topic: how-to
author: Jeronika-MS
ms.author: v-gajeronika
ms.service: system-center
keywords:
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.subservice: service-manager
ms.assetid: 8453a3e9-56ee-4750-b111-81e241c480a4
ms.custom: UpdateFrequency3, engagement-fy23, engagement-fy24
---

# Configure Incident Management in Service Manager

This article provides an overview of how to configure Incident management in Service Manager. This article also contains procedures that cover incident management configuration scenarios, including configuring incident settings, configuring email incident support, and creating an incident template.

Several features in Service Manager let you streamline the creation of incidents. You can configure incident settings such as the following in Service Manager:

- Priority calculations that are based on impact and urgency

- Target resolution time

- Prefixes that are used for incident numbers

- Length of time a closed incident remains in the Service Manager database

You can create an incident template to populate certain fields for a specified incident type, such as email-related problems. Help desk personnel use templates when creating incidents. The template prepopulates some of the fields in the incident, such as the name of the support analyst who handles email-related problems.

You can configure incident management to automatically generate incidents based on desired configuration management for configuration items that aren't in compliance. This works only if Configuration Manager with desired configuration management baselines is installed in your environment.

The procedures in this section describe how to configure incidents. You can define incident priority based on impact and urgency, specify resolution times based on incident priority, create an incident template, and create a new incident based on desired configuration management.

## Configure incident settings

You can use the procedures in this section to configure settings for incident number prefixes, file attachment limits, incident priority calculations, resolution times, and System Center Operations Manager Web settings.

In Service Manager, all the incident numbers start with **IR**. However, you can change the prefix that is used for your incident numbers.

The policy at your organization might limit the number of files that can be attached to each incident to no more than five and to limit the maximum file size for each file at 500 kilobytes (KB).

> [!NOTE]
> The maximum number of attached files and the maximum file size settings that you configure also apply to the attached files in the **Related Items** tab for configuration items.

Incident priority calculation is rated on a scale from 1 to 9. A priority of 1 is the highest priority. It's based on a combination of impact and urgency. Impact and urgency settings are defined as High, Medium, or Low, and they're configured when the incident is created. The following table shows how to define the incident priority for each possible combination of impact and urgency.

:::image type="content" source="./media/incident-mgt/prioritycalculationtable.png" alt-text="Illustration showing the calculation table.":::

The resolution time defines how much time it should take to resolve an incident. Resolution time is based on priority. Typically, you should set resolution times for higher-priority incidents. The procedures in this section describe how to set the values for file attachments, incident priority, and resolution time.

You can create a connector to import alerts and configuration items from Operations Manager. By using the Operations Manager alert connector, Service Manager can create incidents based on alerts. When you view these incidents in Service Manager, you can select a link to obtain more information about the alert or about the health state of the configuration item. Service Manager uses the Operations Manager Web console server to provide this information. Service Manager uses the URL that you specify in the Operations Manager Web setting to connect to Operations Manager.

## Create an incident template

You can use the procedures in this section to create incident templates in Service Manager for problems that are, for example, related to email and printers.

When an analyst at the help desk receives a call, there are many pieces of information that the analyst must gather to create an incident, such as a summary of the problem; the name of the user to whom the incident will be assigned; the impact; the urgency; and whether this is a Tier 1, 2, or 3 incident. For some systems in the enterprise, this information might already be known.

For example, if a problem occurs with the email system, the incident is classified as high-impact and high-urgency, handled at a Tier 2 level, and assigned to a specific analyst. You can create an incident template that, when it's applied to a new incident form, populates many fields in the new incident. This reduces the required time to create an incident, and it ensures accuracy and consistency.

Incident templates are also used as part of the Incident Change workflow. For example, your company might have determined that if the urgency of a printer-related problem changes from Low to High, that incident should automatically be elevated to the Tier 2 level.

You can use the procedures in this section to create two incident templates: one to create email-related incidents and another to use with the Incident Change workflow for printer-related problems.

## Configure incident support for email

Instead of placing a call to the help desk, your end-users can submit incidents by sending an email message to a dedicated email address. Several email addresses can be used, one for hardware, one for software, and one for printers. For example, when a message is sent to Helpdesk@Helpdesk.Woodgrove.com, Microsoft Exchange Server copies the message to a **drop folder** on the computer that is hosting an SMTP Server service. Service Manager monitors this share and processes the message into an incident. Service Manager parses the **From** address and attempts to match the user in the Service Manager database. If Service Manager can't find the user in the Service Manager database, the message is moved into a **bad folder**, and no incident is created. An administrator monitors the **bad folder**.

The infrastructure that is required to handle incidents generated by email includes an existing server running Exchange Server or an SMTP Server and a new server that runs the SMTP service for Service Manager. For this new server, use Internet Information Services\\(IIS)\SMTP services (which is included with Windows Server) on either the computer that is hosting the Service Manager management server or on a separate remote server.

Delegate one of the existing servers that is running Exchange Server or SMTP Server in your enterprise to route all email messages addressed to the help desk, and then configure the IIS SMTP service for use with Service Manager. Providing precise instructions for various versions of Exchange Server or SMTP Service is beyond the scope of this article.

## Set file attachment limits in Service Manager

Use the following procedure to limit the number and size of files that can be attached to an incident in Service Manager. In this example, set the maximum number of files to 5 and the maximum file size to 500 kilobytes (KB).

### Set file attachment limits

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, and select **Settings**.
3. In the **Settings** pane, select **Incident Settings**.
4. In the **Tasks** pane, under **Incident Settings**, select **Properties**.
5. In the **Incident Settings** dialog, select **General**.
6. Set **Maximum number of attached files** to **5**.
7. Set **Maximum size (KB)** to **500**, and select **OK**.

### Validate file attachment limits

- When you create a new incident or edit an existing one, no more than five files can be attached, and each file can be no larger than 500 KB.

## Set parent incident options

Use the following procedure to set default options for parent and child incidents in Service Manager. The default options determine whether the child incidents automatically resolve, whether the child incidents automatically activate, or whether the child incident status automatically updates.

When choosing to automatically resolve child incidents or automatically reactivate child incidents when its parent is resolved or when its parent is reactivated, you can prompt the resolving analyst for their decision. When prompted, an analyst can choose a resolution category or activation status. Otherwise, when incidents are automatically resolved or activated, the analyst isn't prompted and the changes are effective immediately using the parent incident settings.

Select the required tab for steps to automatically resolve, activate, or update child incidents:

# [Resolve child incidents](#tab/ResolveChildIncidents)

Follow these steps to automatically resolve child incidents:

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, and select **Settings**.
3. In the **Settings** pane, select **Incident Settings**.
4. In the **Tasks** pane, under **Incident Settings**, select **Properties**.
5. In the **Incident Settings** dialog, select **Parent Incident** and then choose one of the following actions:
    - If you want to automatically resolve a child incident when its parent is resolved without any analyst interaction, set **Auto resolution of child incidents** to **Automatically resolve child incidents when parent incident is resolved**, and then choose either **Same as parent incident category** or **Choose a child incident category** and a default resolution category.
    - If you want to automatically resolve a child incident when its parent is resolved and have an analyst review and verify the incident resolution category, select **Auto resolution of child incidents** to **Let the analyst decide when resolve the parent incident** and then choose either **Same as parent incident category** or **Choose a child incident category** and a default resolution category.
    - If you don't want child incidents to automatically resolve, select **Auto resolution of child incidents** to **Do not resolve child incidents when parent incident is resolved**.
6. Select **OK**.

# [Activate child incidents](#tab/ActivateChildIncidents)

Follow these steps to automatically activate child incidents:

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, and select **Settings**.
3. In the **Settings** pane, select **Incident Settings**.
4. In the **Tasks** pane, under **Incident Settings**, select **Properties**.
5. In the **Incident Settings** dialog, select **Parent Incident**, and then choose one of the following actions:
    - If you want to automatically activate a child incident when its parent is activated without any analyst interaction, set **Auto reactivation of child incidents** to **Automatically reactivate child incidents when parent incident is reactivated**, and then choose a default reactivation status.
    - If you want to automatically resolve a child incident when its parent is resolved and have an analyst review and verify the incident reactivation status, select **Auto reactivation of child incidents** to **Automatically reactivate child incidents when parent incident is reactivated**, and then choose a default reactivation status.
    - If you don't want to automatically activate child incidents, set **Auto reactivation of child incidents** to **Do not reactivate child incidents when parent incident is reactivated**.
6. Select **OK**.

# [Update child incident status](#tab/UpdateChildIncidentStatus)

Follow these steps to automatically update child incident status:

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, and select **Settings**.
3. In the **Settings** pane, select **Incident Settings**.
4. In the **Tasks** pane, under **Incident Settings**, select **Properties**.
5. In the **Incident Settings** dialog, select **Parent Incident**, and then choose one of the following actions:
    - If you want to automatically update child incident status when it's linked to a parent incident, set **Status of active child incidents when linked to parent** to **Automatically change the status of active child incidents when linking to parent**, and then choose an available incident status.
    - If you don't want to automatically update child incident status, set **Status of active child incidents when linked to parent** to **Do not change the status of child incidents**.
6. Select **OK**.

---

## Set incident priority in Service Manager

Use the following procedure in Service Manager to define a priority calculation table based on impact and urgency settings that are defined during the creation of an incident.

### Set incident priority

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, and select **Settings**.
3. In the **Settings** pane, select **Incident Settings**.
4. In the **Tasks** pane, under **Incident Settings**, select **Properties**.
5. In the **Incident Settings** dialog, select **Priority Calculation**.
6. For each of the High, Medium, and Low settings for both impact and urgency, select an incident priority value from 1 through 9, and select **OK**.

### Validate incident priority

- When you create a new incident or edit an existing one, the resulting priority setting must match the value that is entered in the table for a specific High, Medium, and Low setting that is defined for impact and urgency.

## Set the default incident resolution time

Use the following procedure to set a resolution time based on incident priority in Service Manager.

### Set resolution time

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, and select **Settings**.
3. In the **Settings** pane, select **Incident Settings**.
4. In the **Tasks** pane, under **Incident Settings**, select **Properties**.
5. In the **Incident Settings** dialog, select **Resolution Time**.
6. For each of the priority settings of 1 through 9, specify the amount of time for incident resolution.
7. Select **OK**.

### Validate resolution time

- When you create a new incident or edit an existing one, the resulting resolution times for an incident match the values that are defined in the preceding procedures.

## Set Operations Manager web settings in Service Manager

Use the following procedures to set the web settings of System Center Operations Manager in Service Manager and validate the settings.

### Set Operations Manager web settings

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, and select **Settings**.
3. In the **Settings** pane, select **Incident Settings**.
4. In the **Tasks** pane, under **Incident Settings**, select **Properties**.
5. In the **Incident Settings** dialog, select **Operations Manager Web Settings**.
6. In the **Web Console URL** box, enter the URL of the Operations Manager 2007 web console server, and select **OK**. For example, enter `http://servername:51908`, where *servername* is the name of the computer hosting the web console server.

### Validate Operations Manager web settings

- Ensure that you can access the web console server by entering `http://servername:51908` into your browser, where *servername* is the name of the computer hosting the web console server.

## Configure email incident support for Exchange Server

Use the following procedures to configure your Microsoft Exchange Server infrastructure to support the creation of incidents through email.

### Install and configure the SMTP server

1. Sign in with administrative credentials on the server that will host the Simple Mail Transfer Protocol (SMTP) server role.

    > [!NOTE]
    > A server running Exchange Server can't be your SMTP server.

2. Select **Start**, navigate to **All Programs**, **Administrative Tools**, and select **Server Manager**.
3. In Server Manager, select **Features**, and in the **Features** pane, select **Add Features**.
4. In the **Select Feature** window, select **SMTP Server**.
5. The Add Features Wizard appears. If the dependent role services aren't already selected, you're prompted to add role services and features for the SMTP server. Select **Add Required Role Services**.
6. On the **Select Features** page, select **Next**.
7. On the **Web Server (IIS)** page, select **Next**.
8. On the **Select Role Service** page, select **Next**.
9. On the **Confirm Installation Selections** page, select **Install**.
10. When the **Installation Results** page appears, select **Close** to exit the wizard.

### Configure the IIS SMTP server service for Service Manager

1. On the server that is hosting the SMTP server service, open **Administrative Tools**, and select **Internet Information Services (IIS) Manager**.
2. Expand the SMTP server until you see **SMTP Virtual Server #1**. The SMTP server might have a different name, but it appears with an email icon.
3. Right-click **SMTP Virtual Server #1**, select **Rename**, and then enter the name of your server.
4. Expand **Domains**, and then rename the domain to the fully qualified domain name (FQDN) of the server or the domain name that you want to use.

    > [!NOTE]
    > This can't be the same domain that the server is a member of. However, it can be a child domain.

    For example, if the domain name is contoso.com, you use a server name that resembles server.contoso.com.

5. Using the server name from step 3, right-click the server name, and select **Properties**.
6. Select the **Access** tab, and select **Relay**.
7. On the **Relay Restrictions** tab, select **All except the list below**, select **Allow all computers which successfully authenticate to relay regardless of the list above**, and select **OK**.
8. Select the **Delivery** tab, and select **Advanced**.
9. In the **Advanced Delivery** window, enter the values as shown here:
    1. For **Masquerade Domain**, enter your root domain name; for example, **contoso.com**.
    2. For the FQDN, enter your Exchange server name; for example, **exchange.contoso.com**.
    3. For **Smart host**, enter your Exchange server name; for example, **exchange.contoso.com**.
    4. Select **OK**, and select **OK** again to close the **Advanced Delivery** window.
10. Close IIS Manager, open Windows Explorer, and navigate to *SystemDrive*:\Inetpub\Mailroot.
11. Create two child folders. Name the first folder **Badmail**, and name the second folder **Drop**.
12. Right-click the *SystemDrive*:\Inetpub\Mailroot folder, and select **Share**.
13. For sharing permissions, select the domain user that you specified for the Service Manager account, select **Contributor**, select **Share**, and select **Done**.
14. Restart the Simple Mail Transfer Protocol (SMTP) service, ensure that it's set to **Automatic**, and verify that it has started.

### Configure Service Manager for email

1. Open the Service Manager console, and select **Administration**.
2. In the **Administration** pane, expand **Administration**, and select **Settings**.
3. In the **Settings** pane, double-click **Incident Settings**.
4. Scroll to **Incoming E-mail**.
5. In **The SMTP Service drop folder location**, enter the path, share, and folder for the Drop folder. In this example, enter *computer_name\mailroot\Drop*, where *computer_name* is the name of the computer that is hosting the SMTP Server service, **Mailroot** is the share name, and **Drop** is the subfolder name.
6. In **SMTP Service bad folder location**, enter the path, share, and folder to the Badmail folder. In this example, enter *computer_name\Mailroot\Badmail* where *computer_name* is the name of the computer that is hosting the SMTP Server service, **Mailroot** is the share name, and **Badmail** is the subfolder name.
7. In **Maximum number of e-mails to process at a time**, enter a number for the emails that you want Service Manager to process during an email processing cycle.
8. Select **Turn on incoming e-mails processing**, and select **OK**.

### Configure email notifications

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Notifications**, and select **Channels**.
3. In the **Channels** pane, select **E-Mail Notification Channel**.
4. In the **Tasks** pane, under **E-Mail Notification Channel**, select **Properties** to open the **Configure E-Mail Notification Channel** dialog.
5. Select **Enable e-mail notifications**, and select **Add**.
6. In the **Add SMTP Server** dialog, enter the FQDN of the SMTP server that you want to use. For example, enter **Servername.domain.com**.
7. In **Port number**, enter or select the SMTP port number that you want to use. For example, select **25**.
8. Select **Add**, and in the **Add SMTP Server** dialog, enter the FQDN of the SMTP server that you want to use. For example, enter **Exchange.domain.com**, and replace the information with your Exchange domain name information.
9. In **Port number**, enter or select the SMTP port number that you want to use. For example, select **25**.
10. In **Authentication method**, select **Anonymous**, and select **OK**.
11. In **Return e-mail address**, enter the email address of the service account that was used during Setup. For example, enter **Helpdek\@Servername.domain.com**.
12. In **Retry primary after**, enter or select the number of seconds that you want Service Manager to wait before trying to resend outgoing email notifications. For example, select **25**.
13. Select **OK** to close the dialog.

### Validate email notification configuration

1. In the **Channels** pane, select **E-Mail Notification Channel**.
2. In the **Tasks** pane, under **E-Mail Notification Channel**, select **Configure** to open the **Configure E-Mail Notification Channel** dialog.
3. Confirm that the configuration you entered is correct.

### Configure Exchange Server for use with Service Manager

In the following procedures, you configure Exchange Server for use with Service Manager. You perform these procedures on the server that hosts Exchange Server.

#### Configure the Organization Hub Transport

1. In Exchange Server, select **Organization Configuration**, and select **Hub Transport**.
2. In the **Hub Transport** window, select the **Accepted Domains** tab.
3. In the **Actions** pane, select **New Accepted Domain**.
4. In the New Accepted Domain Wizard, on the **New Accepted Domain** page, in the **Name** box, enter a descriptive name. For example, enter **From SMTP Server**, and in **Accepted Domain**, enter the SMTP domain name that you created for Service Manager. For example, enter **\*.Servername.domain.com**.
5. Select **Authoritative Domain**, and select **New**.

#### Configure the Server Configuration Hub Transport

1. In Exchange Server, navigate to **Server Configuration**, and select **Hub Transport**.
2. In the **Actions** pane, select **New Receive Connector** to open the New Receive Connector Wizard.
3. In **Name**, enter a name that identifies the Service Manager SMTP server, select **Custom** for the intended use, and select **Next**.
4. On the **Local Network Settings** page, accept the default value, leave the **FQDN** box empty, and select **Next**.
5. On the **Remote Network Settings** page, remove the existing IP address, enter the IP address of your Service Manager SMTP server, and select **Next**.
6. On the **New Connector** page, select **New** to complete the wizard.
7. Double-click the newly created **Receive Connector** to open its properties, select the **Authentication** tab, and then clear any items that are selected.
8. Select the **Permissions Groups** tab, select **only Anonymous users**, and select **OK**.
9. To grant relay permission to anonymous connections on the new receive connector, open **Exchange Management Shell**, enter the following, and then press ENTER:

    ```powershell   
    Get-ReceiveConnector "Anonymous Relay" | Add-ADPermission -User "NT AUTHORITY\ANONYMOUS LOGON" -ExtendedRights "Ms-Exch-SMTP-Accept-Any-Recipient"

    ```

10. Close Windows PowerShell.

#### Configure the mail contact in Exchange

1. In Exchange Server, navigate to **Recipient Configuration**, and select **Mail Contact**.
2. In the **Action** pane, select **New Mail Contact**.
3. In the New Mail Contact Wizard, select **New contact**, and select **Next**.
4. In **Name**, enter the name that you want to use as the Service Manager return email address, without @domain.com. For example, enter **Helpdesk**.
5. In **Alias**, enter the name that you want users to use as the **Email Alias** name. For example, enter **Helpdesk**.
6. Edit the **External e-mail address**, and enter the FQDN for the email address. For example, enter **helpdesk\@server.domain.com**.
7. Select **Next**, and select **New** to complete the wizard.

#### Test email functionality between the SMTP server and the Exchange server

1. Using Windows Explorer on the SMTP server, create a new text file named **TESTEMAIL**.
2. Remove the TXT file name extension from the new file.
3. Right-click the TESTEMAIL file, and select **Open**.
4. When you're prompted to open the file with a program, select **Notepad**, and select **OK**.
5. In the file, enter the following using your own information, similar to the following example:

    ```
    to:username@domain.com
    ```

    ```
    from:Helpdesk@servername.domain.com
    ```

    ```
    Subject:This is an email test.
    ```

    ```
    This is a test
    ```

6. Save the file without a file name extension, and then close Notepad.
7. Copy the file to a location where you can use it in the future for testing.
8. Copy the file into the *SystemDrive*:\inetpub\mailroot\Pickup folder.

    > [!NOTE]
    > The file should be removed automatically. This indicates that the Exchange server is using it.

9. Using the user credentials for the **To** recipient that you entered previously, open Outlook and confirm that the email was received.

## Create Service Manager incident templates

Use the following procedures to create two incident templates in Service Manager. The first you use to create email-related incidents, and the second you use with the Incident Change workflow for printer-related problems.

Select the required tab for steps to create an email-related or a new printer-related incident template:

# [Email-related incident template](#tab/EmailRelated)

Follow these steps to create an email-related incident template:

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, expand **Library**, and select **Templates**.
3. In the **Tasks** pane, in the **Templates** area, select **Create Template**.
4. In the **Create Template** dialog, complete these steps:
    1. In the **Name** box, enter a name for the incident template. For example, enter **E-mail Incident**.
    2. In the **Description** box, enter a description for the incident template. For example, enter **Use this template to start all email-related incidents**.
    3. Select **Browse** to choose a class.
    4. In the **Choose Class** dialog, select **Incident**, and select **OK**.
    5. In the **Management Pack** list, select **Service Manager Incident Management Configuration Library**, and select **OK**.
5. In the incident template form, complete these steps:
    1. Leave the **Affected user** box empty.
    2. Leave the **Alternate contact information** box empty. Alternate contact information for the affected user is entered when the incident is created.
    3. In the **Title** box, enter a title for the template. Or, enter a preface, such as **Email:**.
    4. In the **Classification Category** box, select the category that reflects the problem to report. For example, select **E-mail Problems**.
    5. Leave the **Source** box empty. The **Source** box is automatically populated when the incident is created.
    6. In the **Impact** box, select a value. For example, select **High**.
        In the **Urgency** box, select a value. For example, select **High**.
    7. In the **Support Group** box, select a tier. For example, if you want all email-related issues to be assigned to the tier 2 support group, select **Tier 2**.
    8. Select **OK**.

# [Printer-related incident template](#tab/PrinterRelated)

Follow these steps to create a new printer-related incident template:

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, expand **Library**, and select **Templates**.
3. In the **Tasks** pane, select **Create Template**.
4. In the **Create Template** dialog, complete these steps:
    1. In the **Name** box, enter a name for the incident template. For example, enter **Escalate Printer Problems to Tier 2**.
    2. In the **Description** box, enter a description for the incident template. For example, enter **Use this template to assign high-urgency printer-related problems to tier 2**.
    3. Select **Browse** to choose a class.
    4. In the **Choose Class** dialog, select **Incident**, and select **OK**.
    5. In the **Management Pack** list, select **Service Manager Incident Management Configuration Library**, and select **OK**.
5. In the incident template form, follow these steps:
    1. In the **Support Group** box, select a tier. For example, if you want all printer-related issues to be assigned to the tier 2 support group, select **Tier 2**.
    2. Select **OK**.
    3. Press F5 to refresh the **Templates** pane.

---

### Validate that the new incident template was created

Verify that the new incident templates are listed in the **Templates** pane.

## Next steps

To measure incident and service request timeliness, see [Configure service level management](service-level-mgt.md).
