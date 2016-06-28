---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to Configure Your Infrastructure for Email Incident Support With Exchange Server
ms.technology:  service-manager
ms.assetid:  fba0077d-5ddb-4bf1-bceb-a6211c91294c
---

# How to Configure Your Infrastructure for Email Incident Support with Exchange Server

>Applies To: System Center 2016 Technical Preview - Service Manager

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

10. Close IIS Manager, open Windows Explorer, and navigate to <SystemDrive\>:\Inetpub\Mailroot.

11. Create two child folders. Name the first folder **Badmail**, and name the second folder **Drop**.

12. Right-click the <SystemDrive\>:\Inetpub\Mailroot folder, and then click **Share**.

13. For sharing permissions, select the domain user that you specified for the Service Manager account, click **Contributor**, click **Share**, and then click **Done**.

14. Restart the Simple Mail Transfer Protocol (SMTP) service, ensure that it is set to **Automatic**, and verify that it has started.

### To configure Service Manager for email

1.  Open the Service Manager console, and then select **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.

3.  In the **Settings** pane, double-click **Incident Settings**.

4.  Scroll to **Incoming E-mail**.

5.  In **The SMTP Service drop folder location**, type the path, share, and folder for the Drop folder. In this example, type **\\\\<computer_name>\mailroot\Drop**, where **<computer_name>** is the name of the computer that is hosting the SMTP Server service, **Mailroot** is the share name, and **Drop** is the subfolder name.

6.  In **SMTP Service bad folder location**, type the path, share, and folder to the Badmail folder. In this example, type **\\\\<computer_name>\Mailroot\Badmail** where **<computer_name>** is the name of the computer that is hosting the SMTP Server service, **Mailroot** is the share name, and **Badmail** is the subfolder name.

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

## Configuring Exchange Server for use with Service Manager
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

8.  Copy the file into the <SystemDrive\>:\inetpub\mailroot\Pickup folder.

    > [!NOTE]
    > The file should be removed automatically. This indicates that the Exchange server is using it.

9. Using the user credentials for the **To** recipient that you typed previously, open Outlook and confirm that the email was received.



