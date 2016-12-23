---
title: System Center Integration Pack for System Center 2016 Virtual Machine Manager
description: The System Center Integration Pack for System Center 2016 Virtual Machine Manager is an add-in for System Center 2016 - Orchestrator that enables you to automate VMM activities.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b4b8abbd-8fe0-45bd-9112-e43e308f510e
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
System Center Integration Pack for System Center 2016 Virtual Machine Manager
=============================================================================

Applies To: System Center 2016 - Orchestrator

The System Center Integration Pack for System Center 2016 Virtual Machine Manager is an add-in for System Center 2016 - Orchestrator that enables you to automate the following activities:

-   Manage the self-service virtual machine library
-   Create virtual machine resources such as disks, virtual hard disks (VHDs), and network adapters, as needed
-   Create virtual machines from templates, VHDs, and from other virtual machines (modifying disk and network resources if needed)
-   Modify existing virtual machines
-   Turn on and shut down virtual machines in batch mode
-   Restart virtual machines
-   Move virtual machines to a new host to manage availability and performance
-   Create and restore virtual machine checkpoints

For more information about the System Center integration pack for System Center 2016 - Virtual Machine Manager (VMM) and for other options for automating VMM, see the [System Center 2016 Integration Guide](http://go.microsoft.com/fwlink/?LinkID=275796).

System Requirements
-------------------

The VMM Integration Pack requires the following software to be installed and configured before you deploy the integration. For more information about how to install and configure the Orchestrator and the System Center Virtual Machine Manager application, see the respective product documentation.

-   System Center 2016 integration packs require System Center 2016 - Orchestrator
-   System Center 2016 Service Pack 1 (SP1) integration packs require Orchestrator in System Center 2016 Service Pack 1 (SP1)
-   System Center 2016 - Virtual Machine Manager (VMM)
-   Windows Management Framework (Windows PowerShell 2.0 and WinRM 2.0)

The activities from the VMM Integration Pack connect to a Virtual Machine Manager Administration Console which in turn connects to a Virtual Machine Manager server. You can install this console on the Orchestrator runbook server or connect to the Administration console on another computer. If the Orchestrator components and the VMM Administration Console are installed on the same 64-bit computer, the VMM server must be in the same domain to be able to connect to it.

Downloading the Integration Pack
--------------------------------

For information about how to obtain this integration pack, see [System Center 2016 - Orchestrator 2016 Component Add-ons and Extensions](https://www.microsoft.com/en-us/download/details.aspx?id=54098).

Registering and Deploying the Integration Pack
----------------------------------------------

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to Runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How To Install an Integration Pack](https://technet.microsoft.com/system-center-docs/orch/manage/how-to-add-an-integration-pack).

Configuring Windows Management Framework
----------------------------------------

The VMM Integration Pack uses Windows PowerShell Remoting to be configured between the Orchestrator runbook server and the computer running the VMM Administration Console. Windows PowerShell Remoting relies on Windows Remote Management (WinRM) to establish the communications between the two systems. You must perform the following tasks before you configure the VMM connection in the Runbook Designer.

<br><br><strong>Note </strong><br>The Runbook Designer will also connect to the computer running the VMM Administration Console when you are configuring activities from the VMM Integration Pack. If the Runbook Designer is installed on a different computer than the runbook server, then you will also need to configure Windows PowerShell and WinRM on that computer.<br><br>

### Confirm Windows PowerShell 2.0 Installation

PowerShell 2.0 must be installed on both the Orchestrator runbook server and the computer running the VMM Administration Console.

#### To confirm Windows PowerShell 2.0 installation

1.  Open Registry Editor.

2.  Expand the **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\PowerShell\\1\\PowerShellEngine** subkey.

3.  Confirm that the value of the Runtime Version entry begins with v2.0.

4.  If this value begins with 1.0, or the subkey is not present, see [Windows Management Framework (Windows PowerShell 2.0, WinRM 2.0, and BITS 4.0)](http://go.microsoft.com/fwlink/?linkID=193574) for information on installing Windows PowerShell 2.0.

### Confirm Windows Remote Management Installation

Windows Remote Management 2.0 (WinRM 2.0) must be installed and configured on the on both the Orchestrator runbook server and the computer running the VMM Administration Console. You can do this using the Local Group Policy Editor.

#### To confirm Windows Remote Management installation

1.  Click **Start** and then **Run**, type **gpedit.msc**, and then click **OK**.

2.  Under **Local Computer Policy**, then expand **Computer Configuration**, then expand **Administrative Templates**, and then expand **Windows Components**

3.  Verify that **Windows Remote Management (WinRM)** is listed.

For more information about how to install and configure WinRM 2.0, see [Installation and Configuration for Windows Remote Management](http://go.microsoft.com/fwlink/?linkID=171111).

### Windows Remote Management Trusted Hosts

WinRM requires that you explicitly specify the name of any host computers that you are going to connect to. This enhances security by ensuring that the Orchestrator runbook server is connecting to the expected computer running the VMM Administration Console.

#### To enable Windows Remote Management Trusted Hosts

1.  On the Orchestrator runbook server, open the **Local Group Policy Editor**. To do this click **Start**, click **Run**, type **gpedit.msc**, and then click **OK**.

2.  Under **Local Computer Policy**, then expand **Computer Configuration**, then expand **Administrative Templates**, then expand **Windows Components**, then expand **Windows Remote Management**, and then select **WinRM Client**.

3.  Double-click **Trusted Hosts**.

4.  In the **Trusted Hosts** dialog box, select **Enabled**.

5.  Add the name or IP address of the computer running the VMM Administration Console to the **TrustedHostsList** . Click **OK**.

### PowerShell Execution Policy

The execution policy in Windows PowerShell determines which scripts must be digitally signed before they will run. By default, the execution policy is set to **Restricted** which prohibits loading any configuration files or running any scripts. To run the scripts in this integration pack, you must set the execution policy to **RemoteSigned** on both the Orchestrator runbook server and the computer running the VMM Administration Console.

#### To set the execution policy in Windows PowerShell

1.  Click **Start**, then **All Programs**, then **Accessories**, and then **Windows PowerShell**.

2.  Right-click **Windows PowerShell** and select **Run As Administrator**. Click **Yes** when prompted by **User Account Control**.

3.  Type the following command and press **Enter**:

    **set-executionpolicy remotesigned**

For more information abouthow to configure the Windows PowerShell execution policy, see [Set-ExecutionPolicy](http://go.microsoft.com/fwlink/?linkID=113394) in the Microsoft TechNet Library.

### Windows PowerShell Remote Connection Quota

You can use WS-Management quotas in Windows PowerShell remoting to protect the Orchestrator runbook server and the computer running the VMM Administration Console from excessive resource use, both accidental and malicious. The **MaxConcurrentOperationsPerUser** quota setting in the **WSMan:\\&lt;ComputerName&gt;\\Service** node provides this protection by imposing a limit on the number of VMM objects that can run concurrently.

By default, MaxConcurrentOperationsPerUser is set to 5. This means that a maximum of five VMM objects can run concurrently across all VMM activities. If this default setting does not meet the needs of your organization, see [About\_Remote\_Troubleshooting](http://go.microsoft.com/fwlink/?linkID=135188) in the Microsoft TechNet Library for information about how to configure remote operations in Windows PowerShell.

<br><br><strong>Note </strong><br>The **MaxConcurrentOperationsPerUser** affects all Windows PowerShell objects whether or not they are from a runbook. If there are remote sessions from other applications, they will be included in this limit.<br><br>

Configuring the System Center 2016 Virtual Machine Manager Connections
----------------------------------------------------------------------

Once you have validated the WinRM configuration, you must add a **Connection** that defines communications between the Orchestrator runbook server and a computer running the VMM Administration Console. This configuration will include the credentials required to access VMM and the authentication protocol that should be used. When you configure actions from the VMM Integration Pack, you select a configuration that defines the connection that the activity should use. You can create multiple configurations if you have multiple VMM computers to connect to.

#### To configure a System Center 2016 Virtual Machine Manager connection

1.  In the Runbook Designer, click the **Options** menu, and then select **System Center 2016 Virtual Machine Manager**. The **System Center 2016 Virtual Machine Manager** dialog box appears.

2.  On the **Connections** tab, click **Add** to begin the connection setup. The **Connection Entry** dialog box appears.

3.  In the **Name** box, type a name for the connection. This could be the name of the VMM computer for example.

4.  In the **Properties** box, enter a value for each property according to the table below.

5.  Click **OK**.

6.  Add any additional configurations as required.

7.  Click **Finish**.

**Virtual Machine Manager Properties**

| Property   | Description   |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| VMM Administrator Console   | The name or IP address of the computer running the VMM Administrator Console.   |
| User   | The name of a user with access to VMM. This user account must have permissions to the VMM Administration Console and to the VMM server to perform the actions requested by the activities.<br>If you leave this property empty, the configuration will use the credentials from the Runbook Service Account. If this account has appropriate permissions to VMM, then you do not need to provide credentials for the configuration.   |
| Domain   | The domain that the user account resides in.   |
| Password   | The password for the specified user account.   |
| Authentication Type (Remote only) | The type of authentication to use. This is only required if the runbook server and VMM Administration Console are installed on different computers.<br>The authentication method that you choose must be enabled in WinRM. You can enable the authentication methods using the **Local Group Policy Editor**. For more information see [Installation and Configuration for Windows Remote Management](http://go.microsoft.com/fwlink/?linkID=171111). |
| Port (Remote only)   | The port used for PowerShell remoting between the Orchestrator runbook server and the computer with the VMM Administration Console. This is only required if the runbook server and VMM Administration Console are installed on different computers.   |
| Use SSL (Remote only)   | Specifies whether SSL should be used for the connection. This is only required if the runbook server and VMM Administration Console are installed on different computers.   |
| Cache Session Timeout (min.)   | The number of minutes before the session will timeout from lack of activity and need to reconnect.   |
| VMM Server   | The name of the VMM server that action will be performed on. Use **localhost** to if the VMM Administration Console is installed on the VMM server.   |
