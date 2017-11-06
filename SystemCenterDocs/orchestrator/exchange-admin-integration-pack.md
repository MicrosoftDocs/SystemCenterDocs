---
title: Exchange Admin Integration Pack for Orchestrator in System Center 2016
description: Integration packs are add-ons for System Center 2016 - Orchestrator, a component of System Center 2016.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 3d807dc8-013d-45da-9647-825ab64aba2a
author: cfreemanwa
ms.author: raynew
manager: carmonm
---

# Exchange Admin Integration Pack for Orchestrator in System Center 2016

Integration packs are add-ons for System Center 2016 - Orchestrator, a component of System Center 2016. Integration packs help to optimize IT operations across heterogeneous environments. They enable you to design runbooks in Orchestrator that use activities performed by other System Center components, other Microsoft products, and other third party products.

The Integration Pack for Exchange Admin helps to facilitate the automation of Exchange administration tasks, such as mailbox management, for on-premise, remote, or cloud-based environments in Microsoft Exchange and Office 365.

Microsoft is committed to protecting your privacy while delivering software that brings you the performance, power, and convenience you want. For more information about Orchestrator-related privacy, see the [System Center Orchestrator 2016 Privacy Statement](https://www.microsoft.com/en-us/privacystatement/EnterpriseDev/default.aspx).

## System requirements

Before you implement the Integration Pack for Exchange Admin, the following listed software must be installed. For more information about installing and configuring Orchestrator and the Exchange Admin Integration Pack, refer to the respective product documentation.

-   System Center 2016 - Orchestrator or Orchestrator in System Center 2016
-   Microsoft .NET Framework 3.5 Service Pack 1
-   Microsoft Exchange 2010 Service Pack 2 or Microsoft Exchange 2012 or Microsoft Exchange Online/Office 365
-   Microsoft Exchange Management Shell
-   Microsoft PowerShell 2.0
-   Microsoft WinRM 2.0

## Downloading the Integration Pack

To download the Exchange Admin Integration Pack, see the [Download Center site](https://www.microsoft.com/en-us/download/details.aspx?id=54098).

## Register and Deploy the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How to install an Integration Pack](https://technet.microsoft.com/system-center-docs/orch/manage/how-to-add-an-integration-pack).

## Configure the Exchange Admin Integration Pack connections

A connection establishes a reusable link between and an Exchange server. You can specify as many connections as you require to create links to multiple servers. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.

### To set up an Exchange Configuration connection

1.  In the **Orchestrator Runbook Designer**, click **Options**, and then click **Exchange Admin**. The **Exchange Admin** dialog box appears.
2.  On the **Configurations** tab, click **Add** to begin the connection setup. The **Add Configuration** dialog box appears.
3.  In the **Name** box, enter a name for the connection. This can be the name of the **Exchange** server or a descriptive name to differentiate the type of connection.
4.  Click the **(...)** button and select **Exchange Configuration**.
5.  In the **Exchange Server Host** box, type the name or IP address of the Exchange server. To use a computer name, you can type the NetBIOS name or the fully qualified domain name (FQDN).
6.  In the **Exchange Server Port** box, enter the port that is used to communicate with the Exchange server. If you use SSL, be sure to select the appropriate port.
7.  In the **Exchange PowerShell Application** box, enter the application name segment of the connection URI.
8.  In the **Exchange User Name** and **Exchange User Password** boxes, type the credentials that Orchestrator will use to log on to the Exchange environment. The configured user must have the appropriate Exchange permissions.
9.  Configure the **Exchange Environment** as necessary for connecting to an On-Premise installation or to Office.
10. Set the **Use SSL** property to **True** to have all communication between the runbook server and the Exchange server encrypted over HTTPS.
11. If you use SSL, the **Skip CA Check** property specifies whether the client does not validate that the server certificate is signed by a trusted certification authority (CA).
12. If you use SSL, the **Skip CN Check** property specifies that the certificate common name (CN) of the server does not need to match the hostname of the server.
13. If you use SSL, the **Skip Revocation Check** property specifies whether the revocation status of the server certificate will not be checked for validity.
14. Click **OK**.
15. Add additional connections if applicable.
16. Click **Finish**.

## Configure Windows PowerShell and WinRM for the Exchange Admin Integration Pack

### To configure 32-bit PowerShell to run scripts

On the computer where Orchestrator runbooks are executed, make sure that 32-bit PowerShell scripts can be run:

1.  Start **Windows PowerShell (x86)** command line.
2.  To determine whether PowerShell 32-bit scripts can be executed, run the following command:

            Get-ExecutionPolicy

3.  If **Execution Policy** is **Restricted**, you must change it to **RemoteSigned**. Run the following command:

            Set-ExecutionPolicy -ExecutionPolicy RemoteSigned

### To configure remote PowerShell rights for the Exchange user

The configured user must be granted remote PowerShell rights on the Exchange server:

1.  On the Exchange server, start the **Exchange Management Shell**.
2.  To determine whether the user has remote PowerShell rights, run the following command and check the value in the **RemotePowerShellEnabled** field:

            Get-User <UserName>

3.  To grant the user remote PowerShell rights, run the following command:

            Set-User <UserName> -RemotePowerShellEnabled $true

### To configure Windows PowerShell to allow Basic Authentication on the Exchange server

1.  On the Exchange server, make sure that PowerShell Basic Authentication is enabled:
2.  Start **Internet Information Services (IIS) Manager**.
3.  Navigate to the **PowerShell** site.
4.  Open the **Authentication** settings.
5.  Make sure **Basic Authentication** is enabled.

### To configure WinRM for HTTP unencrypted communication

On the machine where Orchestrator runbooks are executed, configure WinRM trusted hosts and to allow unencrypted traffic:

1.  Open the **Local Group Policy** user interface: Windows Start Button &gt; Run &gt; gpedit.msc.
2.  Navigate to **Local Computer Policy** &gt; **Computer Configuration** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Windows Remote Management (WinRM)** &gt; **WinRM Client**.
3.  Make sure that **Allow unencrypted traffic** is Enabled.
4.  Add the targeted computer that runs Exchange Server to the **Trusted Hosts** list.

On the Exchange server, make sure that PowerShell does not require SSL:

1.  Start **Internet Information Services (IIS) Manager**.
2.  Navigate to the **PowerShell** site.
3.  Open **SSL Settings**.
4.  Make sure that the **Require SSL check box** is not selected.

