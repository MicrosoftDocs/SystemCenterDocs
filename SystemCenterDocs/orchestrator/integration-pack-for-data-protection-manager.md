---
title: Integration Pack for System Center DPM in System Center - Orchestrator
description: This article describes the System Center DPM integration pack provided by System Center - Orchestrator.
ms.date: 03/04/2019
ms.prod: system-center
ms.technology: orchestrator
ms.topic: reference
author: jyothisuri
ms.author: jsuri
manager: evansma
---

# Integration pack for System Center - DPM

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The integration pack for System Center - Data Protection Manager (DPM) is an add-in for System Center - Orchestrator. The pack enables you to automate the protection of physical and virtual server resources. You can use the activities in this integration pack to create runbooks that provide the following:

-   Automated virtual machine protection and recovery
-   Automated SharePoint farm protection and recovery
-   Automated SQL server protection and recovery
-   Automated system state protection
-   Ad hoc backups

> [!NOTE]
>  Currently, the integration pack does not support remote SQL servers for DPM.

 [Learn more](list-of-orchestrator-integration-packs.md) about Orchestrator integration packs.

## System requirements

The DPM integration pack requires the following software to be installed and configured, before you implement the integration.

- System Center - Orchestrator
- System Center - Data Protection Manager (DPM)
- Windows Management Framework

## Download the integration pack

::: moniker range="sc-orch-2022"

- [Download the pack for 2022](https://www.microsoft.com/download/details.aspx?id=104334)

::: moniker-end

::: moniker range="<=sc-orch-2019"
- [Download the pack for 2019](https://www.microsoft.com/download/details.aspx?id=58111&WT.mc_id=rss_alldownloads_all)
- [Download the pack for 1801](https://www.microsoft.com/download/details.aspx?id=56605)
- [Download the pack for 2016](https://www.microsoft.com/download/details.aspx?id=54098)
::: moniker-end

## Register and deploy the pack

After you download the integration pack file, you must register it with the Orchestrator management server, and then deploy it to Runbook servers and Runbook Designers. [Learn more](how-to-add-an-integration-pack.md) about installing an integration pack.

## Windows Management Framework

The DPM integration pack uses Windows PowerShell remoting on the Runbook Designer, and on the Runbook Server, to run commands on the DPM server. The WinRM service is started automatically. By default, no WinRM listener is configured. Even if the WinRM service is running, WS-Management protocol messages that request data can't be received or sent.



## Enable Windows Remote Management trusted hosts

1.  On the Orchestrator computer, click **Start** >  **Run**. Then type **gpedit.msc**, and click  **OK** to open the **Local Group Policy Editor**.
2.  In the Local Group Policy Editor, under **Local Computer Policy**, expand **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Windows Remote Management (WinRM)** > **WinRM Client**. Double-click **Trusted Hosts**.
3.  Select **Enabled**, and add the name or IP address of the DPM server to the box below **Trusted Hosts List**. Then, click **OK**.

## Set the execution policy

The execution policy in Windows PowerShell determines which scripts must be digitally signed before they run. By default, the execution policy is set to **Restricted.** This prohibits loading any configuration files or running any scripts. To run the scripts in this integration pack, you must set the execution policy to **RemoteSigned**, as follows:

1.  Open a Windows PowerShell (x86) console as an administrator.

2.  Type the command **&lt;System Drive&gt;:\\PS&gt;set-executionpolicy remotesigned** and press Enter.

3.  When prompted, type **Y** and press Enter.

Learn more about [Set-ExecutionPolicy](/powershell/module/microsoft.powershell.security/set-executionpolicy?preserve-view=true&view=powershell-6).

## Configure remote connection settings

This integration pack uses Windows PowerShell remote commands to communicate with the DPM server, regardless of whether the server is remote or local. You must configure the DPM server and the Orchestrator client computer, to receive Windows PowerShell remote commands that are sent by the Orchestrator server.

Run the following command once on each computer that will receive commands. You don't need to run it on computers that only send commands. Because the command activates listeners, we recommend that you run it only where it is needed.


1.  Open a Windows PowerShell (x86) console as an administrator.
2.  Type _System Drive_**:\\PS&gt;enable-psremoting** and press Enter.

[Learn more](/powershell/module/Microsoft.PowerShell.Core/Enable-PSRemoting?preserve-view=true&view=powershell-3.0) about Enable PSRemoting.

You can use WS-Management quotas in Windows PowerShell remoting to protect the Orchestrator and DPM computers from excessive resource use, both accidental and malicious. The MaxConcurrentOperationsPerUser quota setting in the WSMan:\\*ComputerName*\\Service node provides this protection by imposing a limit on the number of remote connections that can run concurrently.

By default, MaxConcurrentOperationsPerUser is set to 15 in Windows Server 2008 R2. This means that you can run a maximum of 15 DPM activities (shells) concurrently across all DPM runbooks.

WM-Management also provides a setting for MaxConnections (regardless of users), which is set to 25 by default in Windows Server 2008 R2. If these default settings do not meet the needs of your organization, see [About\_Remote\_Troubleshooting](/powershell/module/microsoft.powershell.core/about/about_remote_troubleshooting?preserve-view=true&view=powershell-5.1) for information about how to configure remote operations in Windows PowerShell.

## Configure connections

Connections provide a way for you to define how DPM Activities connect to the DPM servers in your infrastructure. You must define at least one connection, in order to use the DPM activities. You can define as many as you need, to connect to different DPM servers, or to use different connection settings or credentials.


1.  In the Runbook Designer, click the **Options** menu, and then select DPM.
2.  On the **Configurations** tab, click **Add** to begin the connection setup.
3.  In the **Name** box, type a name for the connection. The name may be the name of the DPM server or any other name you wish to describe the connection.
4.  Click the ellipsis button (...) next to the **Type** box, select **PowerShell Remoting**, and then click **OK**.
5.  In the **Properties** pane, the elements that are required to define this integration are displayed. Enter a value for each element, as defined in the table below.
6.  Click **OK** to save the configuration, then click **Finish** to close the dialog.

### DPM properties

| Property   | Description   |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| DPM Administrator Console   | The name or IP address of the computer where the DPM Administrator Console (and PowerShell Management Shell) is installed.   |
| DPM Server   | The name or IP address of the DPM server.   |
| User   | The name of a user with access to DPM. This user account must have permissions on the DPM server, to perform the actions requested by the activities.<br>If you leave this property empty, the configuration will use the credentials from the Runbook Service Account. If this account has appropriate permissions in DPM, then you do not need to provide credentials for the configuration.   |
| Domain   | The domain that the user account resides in.   |
| Password   | The password for the specified user account.   |
| Authentication Type (Remote only) | The type of authentication to use. This is only required if the runbook server and DPMare installed on different computers. Options are as follows:<br> Default - Use the authentication method implemented by the WS-Management protocol. This is the default.<br> Basic - a scheme in which the user name and password are sent in clear text to the server or proxy.<br> Negotiate - a challenge-response scheme that negotiates with the server or proxy to determine the scheme to use for authentication<br> NegotiateWithImplicitCredential - The connection is made using the credentials cached on the local computer.<br> Digest - a challenge-response scheme that uses a server-specified data string for the challenge.<br> Kerberos - The client computer and the server mutually authenticate by using Kerberos certificates.<br> The authentication method that you choose must be enabled in WinRM. You can enable the authentication methods using the **Local Group Policy Editor**. For more information see [Installation and Configuration for Windows Remote Management](/windows/desktop/WinRM/installation-and-configuration-for-windows-remote-management). |
| Port (Remote only)   | Specifies the port to use when the client connects to the WinRM service on the remote server. By default, the port used is 5985.   |
| Use SSL (Remote only)   | Specifies whether SSL should be used for the connection.   |
| Cache Session Timeout (min.)   | The number of minutes before the session will time out from lack of activity and need to reconnect. By default, this is 10 minutes.   |