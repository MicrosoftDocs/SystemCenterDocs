---
title:  Configure Incident Management in Service Manager
description: Learn about how to configure Incident Management in Service Manager.
manager:  carmonm
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology:  service-manager
ms.assetid:  8453a3e9-56ee-4750-b111-81e241c480a4
---

# Configure Incident Management in Service Manager

>Applies To: System Center 2016 - Service Manager

This article provides an overview of how to configure Incident management in Service Manager. This article also contains procedures that cover incident management configuration scenarios, including configuring incident settings, configuring email incident support, and creating an incident template.

Several features in Service Manager let you streamline the creation of incidents. You can configure incident settings such as the following in Service Manager:

-   Priority calculations that are based on impact and urgency

-   Target resolution time

-   Prefixes that are used for incident numbers

-   Length of time a closed incident remains in the Service Manager database

You can create an incident template to populate certain fields for a specified incident type, such as email-related problems. Help desk personnel use templates when creating incidents. The template prepopulates some of the fields in the incident, such as the name of the support analyst who handles email-related problems.

You can configure incident management to automatically generate incidents based on desired configuration management for configuration items that are not in compliance. This works only if Configuration Manager with desired configuration management baselines is installed in your environment.

The procedures in this section describe how to configure incidents. You can define incident priority based on impact and urgency, specify resolution times based on incident priority, create an incident template, and create a new incident based on desired configuration management.

## Configure incident settings
You can use the procedures in this section to configure settings for incident number prefixes, file attachment limits, incident priority calculations, resolution times, and System Center Operations Manager Web settings.

In Service Manager, all incident numbers start with "IR". However, you can change the prefix that is used for your incident numbers.

The policy at your organization might limit the number of files that can be attached to each incident to no more than five and to limit the maximum file size for each file at 500 kilobytes (KB).

> [!NOTE]
> The maximum number of attached files and maximum file size settings that you configure also apply to the attached files in the **Related Items** tab for configuration items.

Incident priority calculation is rated on a scale from 1 to 9. A priority of 1 is the highest priority. It is based on a combination of impact and urgency. Impact and urgency settings are defined as High, Medium, or Low, and they are configured when the incident is created. The following table shows how to define the incident priority for each possible combination of impact and urgency.

![calculation table](../media/prioritycalculationtable.png)

The resolution time defines how much time it should take to resolve an incident. Resolution time is based on priority. Typically, you should set resolution times for higher-priority incidents. The procedures in this section describe how to set the values for file attachments, incident priority, and resolution time.

You can create a connector to import alerts and configuration items from Operations Manager. By using the Operations Manager alert connector, Service Manager can create incidents based on alerts. When you view these incidents in Service Manager, you can click a link to obtain more information about the alert or about the health state of the configuration item. Service Manager uses the Operations Manager Web console server to provide this information. Service Manager uses the URL that you specify in the Operations Manager Web setting to connect to Operations Manager.

## Create an incident template
You can use the procedures in this section to create incident templates in Service Manager for problems that are, for example, related to email and printers.

When an analyst at the help desk receives a call, there are many pieces of information that the analyst must gather to create an incident, such as a summary of the problem; the name of the user to whom the incident will be assigned; the impact; the urgency; and whether this is a Tier 1, 2, or 3 incident. For some systems in the enterprise, this information might already be known.

For example, if a problem occurs with the e-mail system, the incident is classified as high-impact and high-urgency, handled at a Tier 2 level, and assigned to a specific analyst. You can create an incident template that, when it is applied to a new incident form, populates many fields in the new incident. This reduces the required time to create an incident, and it ensures accuracy and consistency.

Incident templates are also used as part of the Incident Change workflow. For example, your company might have determined that if the urgency of a printer-related problem changes from Low to High, that incident should automatically be elevated to the Tier 2 level.

You can use the procedures in this section to create two incident templates, one to create email-related incidents and another to use with the Incident Change workflow for printer-related problems.

## Configuring incident support for email
Instead of placing a call to the help desk, your end-users can submit incidents by sending an email message to a dedicated email address. Several email addresses can be used, one for hardware, one for software, and one for printers. For example, when a message is sent to Helpdesk@Helpdesk.Woodgrove.com, Microsoft Exchange Server copies the message to a "drop folder" on the computer that is hosting an SMTP Server service. Service Manager monitors this share and processes the message into an incident. Service Manager parses the **From** address and attempts to match the user in the Service Manager database. If Service Manager cannot find the user in the Service Manager database, the message is moved into a "bad folder", and no incident is created. An administrator monitors the "bad folder".

The infrastructure that is required to handle incidents generated by email includes an existing server running Exchange Server or an SMTP Server and a new server that runs the SMTP service for Service Manager. For this new server, use Internet Information Services\\(IIS)\SMTP services (which is included with Windows Server) on either the computer that is hosting the Service Manager management server or on a separate remote server.

Delegate one of the existing servers that is running Exchange Server or SMTP Server in your enterprise to route all email messages addressed to the help desk, and then configure the IIS SMTP service for use with Service Manager. Providing precise instructions for various versions of Exchange Server or SMTP Service is beyond the scope of this guide.

## Set file attachment limits in Service Manager

Use the following procedure to limit the number and size of files that can be attached to an incident in Service Manager. In this example, set the maximum number of files to 5 and the maximum file size to 500 kilobytes (KB).

### To set file attachment limits

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.
3.  In the **Settings** pane, click **Incident Settings**.
4.  In the **Tasks** pane, under **Incident Settings**, click **Properties**.
5.  In the **Incident Settings** dialog box, click **General**.
6.  Set **Maximum number of attached files** to **5**.
7.  Set **Maximum size (KB)** to **500**, and then click **OK**.

### To validate file attachment limits

-   When you create a new incident or edit an existing one, no more than five files can be attached, and each file can be no larger than 500 KB.

## Set parent incident options

Use the following procedure to set default options for parent and child incidents in Service Manager. The default options determine whether child incidents automatically resolve, whether child incidents automatically activate, and whether child incident status automatically updates.

When choosing to automatically resolve child incidents or automatically reactivate child incidents when its parent is resolved or when its parent is reactivated, you can prompt the resolving analyst for their decision. When prompted, an analyst can choose a resolution category or activation status. Otherwise, when incidents are automatically resolved or activated, the analyst is not prompted and the changes are effectively immediately using the parent incident settings.

### To automatically resolve child incidents

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.
3.  In the **Settings** pane, click **Incident Settings**.
4.  In the **Tasks** pane, under **Incident Settings**, click **Properties**.
5.  In the **Incident Settings** dialog box, click **Parent Incident** and then choose one of the following actions:
    -   If you want to automatically resolve a child incident when its parent is resolved without any analyst interaction, set **Auto resolution of child incidents** to **Automatically resolve child incidents when parent incident is resolved**, and then choose either **Same as parent incident category** or **Choose a child incident category** and a default resolution category.
    -   If you want to automatically resolve a child incident when its parent is resolved and have an analyst review and verify the incident resolution category, select **Auto resolution of child incidents** to **Let the analyst decide when resolve the parent incident** and then choose either **Same as parent incident category** or **Choose a child incident category** and a default resolution category.
    -   If you do not want child incidents to automatically resolve, select **Auto resolution of child incidents** to **Do not resolve child incidents when parent incident is resolved**.
6.  Click **OK**.

### To automatically activate child incidents

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.
3.  In the **Settings** pane, click **Incident Settings**.
4.  In the **Tasks** pane, under **Incident Settings**, click **Properties**.
5.  In the **Incident Settings** dialog box, click **Parent Incident**, and then choose one of the following actions:
    -   If you want to automatically activate a child incident when its parent is activated without any analyst interaction, set **Auto reactivation of child incidents** to **Automatically reactivate child incidents when parent incident is reactivated**, and then choose a default reactivation status.
    -   If you want to automatically resolve a child incident when its parent is resolved and have an analyst review and verify the incident reactivation status, select **Auto reactivation of child incidents** to **Automatically reactivate child incidents when parent incident is reactivated**, and then choose a default reactivation status.
    -   If you do not want to automatically activate child incidents, set **Auto reactivation of child incidents** to **Do not reactivate child incidents when parent incident is reactivated**.
6.  Click **OK**.

### To automatically update child incident status

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.
3.  In the **Settings** pane, click **Incident Settings**.
4.  In the **Tasks** pane, under **Incident Settings**, click **Properties**.
5.  In the **Incident Settings** dialog box, click **Parent Incident**, and then choose one of the following actions:
    -   If you want to automatically update child incident status when it is linked to a parent incident, set **Status of active child incidents when linked to parent** to **Automatically change the status of active child incidents when linking to parent**, and then choose an available incident status.
    -   If you do not want to automatically update child incident status, set **Status of active child incidents when linked to parent** to **Do not change the status of child incidents**.
6.  Click **OK**.

## Set incident priority

Use the following procedure in Service Manager to define a priority calculation table based on impact and urgency settings that are defined during the creation of an incident.

### To set incident priority

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.
3.  In the **Settings** pane, click **Incident Settings**.
4.  In the **Tasks** pane, under **Incident Settings**, click **Properties**.
5.  In the **Incident Settings** dialog box, select **Priority Calculation**.
6.  For each of the High, Medium, and Low settings for both impact and urgency, select an incident priority value from 1 through 9, and then click **OK**.

### To validate incident priority

-   When you create a new incident or edit an existing one, the resulting priority setting must match the value that is entered in the table for a specific High, Medium, and Low setting that is defined for impact and urgency.

## Set the default incident resolution time

Use the following procedure to set a resolution time based on incident priority in Service Manager.

### To set resolution time

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.
3.  In the **Settings** pane, click **Incident Settings**.
4.  In the **Tasks** pane, under **Incident Settings**, click **Properties**.
5.  In the **Incident Settings** dialog box, select **Resolution Time**.
6.  For each of the priority settings of 1 through 9, specify the amount of time for incident resolution.
7.  Click **OK**.

### To validate resolution time

-   When you create a new incident or edit an existing one, the resulting resolution times for an incident matches the values that are defined in the preceding procedures.

## Set Operations Manager web settings in Service Manager

Use the following procedures to set the web settings of System Center Operations Manager in Service Manager and validate the settings.

### To set Operations Manager web settings

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.
3.  In the **Settings** pane, click **Incident Settings**.
4.  In the **Tasks** pane, under **Incident Settings**, click **Properties**.
5.  In the **Incident Settings** dialog box, click **Operations Manager Web Settings**.
6.  In the **Web Console URL** box, type the URL of the Operations Manager 2007 web console server, and then click **OK**. For example, type `http://servername:51908`, where *servername* is the name of the computer hosting the web console server.

### To validate Operations Manager web settings

-   Make sure that you can access the web console server by entering `http://servername:51908` into your browser, where *servername* is the name of the computer hosting the web console server.

## Configure email incident support for Exchange Server

Use the following procedures to configure your Microsoft Exchange Server infrastructure to support the creation of incidents through email.

### To install and configure the SMTP server

1.  Log on with administrative credentials on the server that will host the Simple Mail Transfer Protocol (SMTP) server role.

    > [!NOTE]
    > A server running Exchange Server cannot be your SMTP server.

2.  Click **Start**, navigate to **All Programs**, **Administrative Tools**, and then click **Server Manager**.
3.  In Server Manager, click **Features**, and in the **Features** pane, click **Add Features**.
4.  In the **Select Feature** window, click **SMTP Server**.
5.  The Add Features Wizard appears. If the dependent role services are not already selected, you are prompted to add role services and features for the SMTP server. Click **Add Required Role Services**.
6.  On the **Select Features** page, click **Next**.
7.  On the **Web Server (IIS)** page, click **Next**.
8.  On the **Select Role Service** page, click **Next**.
9. On the **Confirm Installation Selections** page, click **Install**.
10. When the **Installation Results** page appears, click **Close** to exit the wizard.

### To configure the IIS SMTP server service for Service Manager

1.  On the server that is hosting the SMTP server service, open **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.
2.  Expand the SMTP server until you see **SMTP Virtual Server #1**. The SMTP server might have a different name, but it appears with an email icon.
3.  Right-click **SMTP Virtual Server #1**, click **Rename**, and then type the name of your server.
4.  Expand **Domains**, and then rename the domain to the fully qualified domain name (FQDN) of the server or the domain name that you want to use.

    > [!NOTE]
    > This cannot be the same domain that the server is a member of. However, it can be a child domain.

    For example, if the domain name is contoso.com, you use a server name that resembles server.contoso.com.

5.  Using the server name from step 3, right-click the server name, and then click **Properties**.
6.  Click the **Access** tab, and then click **Relay**.
7.  On the **Relay Restrictions** tab, click **All except the list below**, click **Allow all computers which successfully authenticate to relay regardless of the list above**, and then click **OK**.
8.  Click the **Delivery** tab, and then click **Advanced**.
9. In the **Advanced Delivery** window, type the values as shown here:
    1.  For **Masquerade Domain**, type your root domain name, for example, **contoso.com**.
    2.  For the FQDN, type your Exchange server name, for example, **exchange.contoso.com**.
    3.  For **Smart host**, type your Exchange server name, for example, **exchange.contoso.com**.
    4.  Click **OK**, and then click **OK** again to close the **Advanced Delivery** window.
10. Close IIS Manager, open Windows Explorer, and navigate to *SystemDrive*:\Inetpub\Mailroot.
11. Create two child folders. Name the first folder **Badmail**, and name the second folder **Drop**.
12. Right-click the *SystemDrive*:\Inetpub\Mailroot folder, and then click **Share**.
13. For sharing permissions, select the domain user that you specified for the Service Manager account, click **Contributor**, click **Share**, and then click **Done**.
14. Restart the Simple Mail Transfer Protocol (SMTP) service, ensure that it is set to **Automatic**, and verify that it has started.

### To configure Service Manager for email

1.  Open the Service Manager console, and then select **Administration**.
2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.
3.  In the **Settings** pane, double-click **Incident Settings**.
4.  Scroll to **Incoming E-mail**.
5.  In **The SMTP Service drop folder location**, type the path, share, and folder for the Drop folder. In this example, type *computer_name\mailroot\Drop*, where *computer_name* is the name of the computer that is hosting the SMTP Server service, **Mailroot** is the share name, and **Drop** is the subfolder name.
6.  In **SMTP Service bad folder location**, type the path, share, and folder to the Badmail folder. In this example, type *computer_name\Mailroot\Badmail* where *computer_name* is the name of the computer that is hosting the SMTP Server service, **Mailroot** is the share name, and **Badmail** is the subfolder name.
7.  In **Maximum number of e-mails to process at a time**, type a number for the emails that you want Service Manager to process during an email processing cycle.
8.  Select **Turn on incoming e-mails processing**, and then click **OK**.

### To configure email notifications

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Notifications**, and then click **Channels**.
3.  In the **Channels** pane, click **E-Mail Notification Channel**.
4.  In the **Tasks** pane, under **E-Mail Notification Channel**, click **Properties** to open the **Configure E-Mail Notification Channel** dialog box.
5.  Click **Enable e-mail notifications**, and then click **Add**.
6.  In the **Add SMTP Server** dialog box, type the FQDN of the SMTP server that you want to use. For example, type **Servername.domain.com**.
7.  In **Port number**, type or select the SMTP port number that you want to use. For example, select **25**.
8.  Click **Add**, and in the **Add SMTP Server** dialog box, type the FQDN of the SMTP server that you want to use. For example, type **Exchange.domain.com**, and replace the information with your Exchange domain name information.
9. In **Port number**, type or select the SMTP port number that you want to use. For example, select **25**.
10. In **Authentication method**, click **Anonymous**, and then click **OK**.
11. In **Return e-mail address**, type the email address of the service account that was used during Setup. For example, type **Helpdek@Servername.domain.com**.
12. In **Retry primary after**, type or select the number of seconds that you want Service Manager to wait before trying to resend outgoing email notifications. For example, select **25**.
13. Click **OK** to close the dialog box.

### To validate email notification configuration

1.  In the **Channels** pane, **click E-Mail Notification Channel**.
2.  In the **Tasks** pane, under **E-Mail Notification Channel**, click **Configure** to open the **Configure E-Mail Notification Channel** dialog box.
3.  Confirm that the configuration you entered is correct.

### Configure Exchange Server for use with Service Manager
In the following procedures, you configure Exchange Server for use with Service Manager. You perform these procedures on the server that hosts Exchange Server.

#### To configure the Organization Hub Transport

1.  In Exchange Server, click **Organization Configuration**, and then click **Hub Transport**.
2.  In the **Hub Transport** window, click the **Accepted Domains** tab.
3.  In the **Actions** pane, click **New Accepted Domain**.
4.  In the New Accepted Domain Wizard, on the **New Accepted Domain** page, in the **Name** box, type a descriptive name. For example, type **From SMTP Server**, and in **Accepted Domain**, type the SMTP domain name that you created for Service Manager. For example, type **\*.Servername.domain.com**.
5.  Click **Authoritative Domain**, and then click **New**.

#### To configure the Server Configuration Hub Transport

1.  In Exchange Server, navigate to **Server Configuration**, and then click **Hub Transport**.
2.  In the **Actions** pane, click **New Receive Connector** to open the New Receive Connector Wizard.
3.  In **Name**, type a name that identifies the Service Manager SMTP server, select **Custom** for the intended use, and then click **Next**.
4.  On the **Local Network Settings** page, accept the default value, leave the **FQDN** box empty, and then click **Next**.
5.  On the **Remote Network Settings** page, remove the existing IP address, type the IP address of your Service Manager SMTP server, and then click **Next**.
6.  On the **New Connector** page, click **New** to complete the wizard.
7.  Double-click the newly created **Receive Connector** to open its properties, click the **Authentication** tab, and then clear any items that are selected.
8.  Click the **Permissions Groups** tab, click **only Anonymous users**, and then click **OK**.
9. To grant relay permission to anonymous connections on the new receive connector, open **Exchange Management Shell**, type the following, and then press ENTER:

    ```
    Get-ReceiveConnector "Anonymous Relay" | Add-ADPermission -User "NT AUTHORITY\ANONYMOUS LOGON" -ExtendedRights "Ms-Exch-SMTP-Accept-Any-Recipient"

    ```

10. Close Windows PowerShell.

#### To configure the mail contact in Exchange

1.  In Exchange Server, navigate to **Recipient Configuration**, and then click **Mail Contact**.
2.  In the **Action** pane, click **New Mail Contact**.
3.  In the New Mail Contact Wizard, click **New contact**, and then click **Next**.
4.  In **Name**, type the name that you want to use as the Service Manager return email address, without @domain.com. For example, type **Helpdesk**.
5.  In **Alias**, type the name that you want users to use as the **Email Alias** name. For example, type **Helpdesk**.
6.  Edit the **External e-mail address**, and type the FQDN for the email address. For example, type **helpdesk@server.domain.com**.
7.  Click **Next**, and then click **New** to complete the wizard.

#### To test email functionality between the SMTP server and the Exchange server

1.  Using Windows Explorer on the SMTP server, create a new text file named **TESTEMAIL**.
2.  Remove the TXT file name extension from the new file.
3.  Right-click the TESTMAIL file, and then click **Open**.
4.  When you are prompted to open the file with a program, click **Notepad**, and then click **OK**.
5.  In the file, type the following using your own information, similar to the following example:

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

6.  Save the file without a file name extension, and then close Notepad.
7.  Copy the file to a location where you can use it in the future for testing.
8.  Copy the file into the *SystemDrive*:\inetpub\mailroot\Pickup folder.

    > [!NOTE]
    > The file should be removed automatically. This indicates that the Exchange server is using it.

9. Using the user credentials for the **To** recipient that you typed previously, open Outlook and confirm that the email was received.

## Create Service Manager incident templates

Use the following procedures to create two incident templates in Service Manager. The first you use to create email-related incidents, and the second you use with the Incident Change workflow for printer-related problems.

### To create an email-related incident template

1.  In the Service Manager console, click **Library**.
2.  In the **Library** pane, expand **Library**, and then click **Templates**.
3.  In the **Tasks** pane, in the **Templates** area, click **Create Template**.
4.  In the **Create Template** dialog box, complete these steps:
    1.  In the **Name** box, type a name for the incident template. For example, type **E-mail Incident**.
    2.  In the **Description** box, type a description for the incident template. For example, type **Use this template to start all email-related incidents**.
    3.  Click **Browse** to choose a class.
    4.  In the **Choose Class** dialog box, click **Incident**, and then click **OK**.
    5.  In the **Management Pack** list, select **Service Manager Incident Management Configuration Library**, and then click **OK**.
5.  In the incident template form, complete these steps:
    1.  Leave the **Affected user** box empty.
    2.  Leave the **Alternate contact information** box empty. Alternate contact information for the affected user is entered when the incident is created.
    3.  In the **Title** box, type a title for the template. Or, type a preface, such as **Email:**.
    4.  In the **Classification Category** box, select the category that reflects the problem to report. For example, select **E-mail Problems**.
    5.  Leave the **Source** box empty. The **Source** box is automatically populated when the incident is created.
    6.  In the **Impact** box, select a value. For example, select **High**.
        In the **Urgency** box, select a value. For example, select **High**.
    7.  In the **Support Group** box, select a tier. For example, if you want all email-related issues to be assigned to the tier 2 support group, select **Tier 2**.
    8.  Click **OK**.

### To create a new printer-related incident template

1.  In the Service Manager console, click **Library**.
2.  In the **Library** pane, expand **Library**, and then click **Templates**.
3.  In the **Tasks** pane, click **Create Template**.
4.  In the **Create Template** dialog box, complete these steps:
    1.  In the **Name** box, type a name for the incident template. For example, type **Escalate Printer Problems to Tier 2**.
    2.  In the **Description** box, type a description for the incident template. For example, type **Use this template to assign high-urgency printer-related problems to tier 2**.
    3.  Click **Browse** to choose a class.
    4.  In the **Choose Class** dialog box, click **Incident**, and then click **OK**.
    5.  In the **Management Pack** list, select **Service Manager Incident Management Configuration Library**, and then click **OK**.
5.  In the incident template form, follow these steps:
    1.  In the **Support Group** box, select a tier. For example, if you want all printer-related issues to be assigned to the tier 2 support group, select **Tier 2**.
    2.  Click **OK**.
    3.  Press F5 to refresh the **Templates** pane.

### To validate that the new incident template was created

-   Verify that the new incident templates are listed in the **Templates** pane.
