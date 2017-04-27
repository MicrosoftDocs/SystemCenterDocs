---
title: System Center Integration Pack for System Center 2016 Data Protection Manager
description: The System Center Integration Pack for System Center 2016 Data Protection Manager is an add-in for System Center 2016 - Orchestrator that enables you to automate the protection of physical and virtual server resources.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 5e7c74e4-15ac-49e2-a97c-512065b71edc
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
---

# System Center Integration Pack for System Center 2016 Data Protection Manager

Applies To: System Center 2016 - Orchestrator

The System Center Integration Pack for System Center 2016 Data Protection Manager is an add-in for System Center 2016 - Orchestrator that enables you to automate the protection of physical and virtual server resources. You can use the activities in this integration pack to create runbooks that provide the following:

-   Automated virtual machine protection and recovery
-   Automated SharePoint farm protection and recovery
-   Automated SQL server protection and recovery
-   Automated system state protection
-   Ad hoc backups

For more information on the System Center integration pack for DPM and for other options for automating DPM, see the [System Center 2016 Integration Guide](http://go.microsoft.com/fwlink/?LinkID=275796).

## System Requirements

The DPM Integration Pack requires the following software to be installed and configured before you implement the integration. For more information about how to install and configure the Orchestrator and System Center 2016 - Data Protection Manager (DPM), see the documentation for each of the following products:

-   System Center 2016 integration packs require System Center 2016 - Orchestrator and System Center 2016 - Data Protection Manager (DPM)
-   Windows Management Framework

## Downloading the Integration Pack

For information about how to obtain this integration pack, see [System Center 2016 - Orchestrator 2016 Component Add-ons and Extensions](https://www.microsoft.com/en-us/download/details.aspx?id=54098).

## Registering and Deploying the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to Runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How To Install an Integration Pack](https://technet.microsoft.com/system-center-docs/orch/manage/how-to-add-an-integration-pack).

## Windows Management Framework

The DPM Integration Pack uses Windows PowerShell remoting on the Runbook Designer and on the Runbook Server to run commands on the DPM server. By default, Windows PowerShell 2.0 and Windows Remote Management (Win-RM) 2.0 is included and enabled in Windows Server 2008 R2.

The WinRM service is started automatically, but by default, no WinRM listener is configured. Even if the WinRM service is running, WS-Management protocol messages that request data cannot be received or sent.

Perform the following tasks on the Orchestrator server and on the DPM server before you use this Integration Pack.

### To enable Windows Remote Management Trusted Hosts

1.  On the Orchestrator computer, open the **Local Group Policy Editor**. To do this, click **Start**, click **Run**, type **gpedit.msc**, and then click **OK**.
2.  In the Local Group Policy Editor, under **Local Computer Policy**, expand **Computer Configuration**, **Administrative Templates**, **Windows Components**, **Windows Remote Management (WinRM)**, **WinRM Client**, and then double-click **Trusted Hosts**.
3.  Select **Enabled**. Add the name or IP address of the DPM server to the box below **Trusted Hosts List**. Click **OK**.

## Execution Policy

The execution policy in Windows PowerShell determines which scripts must be digitally signed before they will run. By default, the execution policy is set to **Restricted.** This prohibits loading any configuration files or running any scripts.

To run the scripts in this integration pack, you must set the execution policy to **RemoteSigned** using the following procedure..

### To set the execution policy in Windows PowerShell

1.  Open a Windows PowerShell (x86) console as an administrator.

2.  Type the command **&lt;System Drive&gt;:\\PS&gt;set-executionpolicy remotesigned** and press Enter.

3.  When prompted, type **Y** and press Enter.

For more information abouthow to configure the Windows PowerShell execution policy, see [Set-ExecutionPolicy](http://go.microsoft.com/fwlink/?linkID=113394).

## Remote Connection Settings

This integration pack uses Windows PowerShell remote commands to communicate with the DPM server, regardless of whether the server is remote or local. If you have not already done so, you must configure the DPM server and the Orchestrator client computer to receive Windows PowerShell remote commands that are sent by the Orchestrator server.

Run the following command only one time on each computer that will receive commands. You do not have to run it on computers that only send commands. Because the command activates listeners, we recommend that you run it only where it is needed.

### To enable or confirm remote connection settings in Windows PowerShell

1.  Open a Windows PowerShell (x86) console as an administrator.
2.  Type *System Drive***:\\PS&gt;enable-psremoting** and press Enter.

For more information about how to use the **Enable-PSRemoting** cmdlet, see [Enable PSRemoting](http://go.microsoft.com/fwlink/?linkID=144300).

You can use WS-Management quotas in Windows PowerShell remoting to protect the Orchestrator and DPM computers from excessive resource use, both accidental and malicious. The MaxConcurrentOperationsPerUser quota setting in the WSMan:\\*ComputerName*\\Service node provides this protection by imposing a limit on the number of remote connections that can run concurrently.

By default, MaxConcurrentOperationsPerUser is set to 15 in Windows Server 2008 R2. This means that you can run a maximum of 15 DPM activities (shells) concurrently across all DPM runbooks.

WM-Management also provides provides a setting for MaxConnections (regardless of users), which is set to 25 by default in Windows Server 2008 R2. If these default settings do not meet the needs of your organization, see [About\_Remote\_Troubleshooting](http://go.microsoft.com/fwlink/?linkID=135188) for information about how to configure remote operations in Windows PowerShell.

## Configuring the System Center 2016 Data Protection Manager Connections

Connections provide a way for you to define the way that the DPM Activities will connect to the DPM server(s) in your infrastructure. You must define at least one connection in order to use the DPM activities, but you can define as many as you need in order to connect to different DPM servers or utilize different connection settings or credentials.

### To configure a System Center 2016 Data Protection Manager connection

1.  In the Runbook Designer, click the **Options** menu, and then select **SC 2016 Data Protection Manager**.
2.  In the **SC 2016 Data Protection Manager** dialog box, on the **Configurations** tab, click **Add** to begin the connection setup.
3.  In the **Name** box, type a name for the connection. The name may be the name of the DPM server or any other name you wish to describe the connection.
4.  Click the ellipsis button (...) next to the **Type** box, select **PowerShell Remoting**, and then click **OK**.
5.  In the **Properties** pane, the elements that are required to define this integration are displayed. Enter a value for each element, as defined in the table below.
6.  Click **OK** to save the configuration, then click **Finish** to close the dialog.

### Data Protection Manager Properties

| Property   | Description   |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| DPM Administrator Console   | The name or IP address of the computer where the DPM Administrator Console (and PowerShell Management Shell) is installed.   |
| DPM Server   | The name or IP address of the DPM server.   |
| User   | The name of a user with access to DPM. This user account must have permissions to the DPMserver to perform the actions requested by the activities.<br>If you leave this property empty, the configuration will use the credentials from the Runbook Service Account. If this account has appropriate permissions to DPM, then you do not need to provide credentials for the configuration.   |
| Domain   | The domain that the user account resides in.   |
| Password   | The password for the specified user account.   |
| Authentication Type (Remote only) | The type of authentication to use. This is only required if the runbook server and DPMare installed on different computers. Options are as follows:<br> Default - Use the authentication method implemented by the WS-Management protocol. This is the default.<br> Basic - a scheme in which the user name and password are sent in clear text to the server or proxy.<br> Negotiate - a challenge-response scheme that negotiates with the server or proxy to determine the scheme to use for authentication<br> NegotiateWithImplicitCredential - The connection is made using the credentials cached on the local computer.<br> Digest - a challenge-response scheme that uses a server-specified data string for the challenge.<br> Kerberos - The client computer and the server mutually authenticate by using Kerberos certificates.<br> The authentication method that you choose must be enabled in WinRM. You can enable the authentication methods using the **Local Group Policy Editor**. For more information see [Installation and Configuration for Windows Remote Management](http://go.microsoft.com/fwlink/?linkID=171111). |
| Port (Remote only)   | Specifies the port to use when the client connects to the WinRM service on the remote server. By default, the port used is 5985.   |
| Use SSL (Remote only)   | Specifies whether SSL should be used for the connection.   |
| Cache Session Timeout (min.)   | The number of minutes before the session will timeout from lack of activity and need to reconnect. By default, this is 10 minutes.   |
