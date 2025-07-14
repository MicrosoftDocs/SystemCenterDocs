---
title: Integration pack for System Center - Virtual Machine Manager (VMM)
description: This article describes the System Center integration pack for System Center - Virtual Machine Manager (VMM). The integration pack is an add-in for System Center - Orchestrator.
ms.date: 07/07/2025
ms.service: system-center
ms.subservice: orchestrator
ms.topic: concept-article
author: jyothisuri
ms.author: jsuri
ms.custom: engagement-fy24
---

# Integration pack for System Center VMM

The integration pack for System Center - Virtual Machine Manager (VMM) is an add-in for System Center - Orchestrator. This pack enables you to automate the following activities:

- Manage the self-service virtual machine library
- Create virtual machine resources such as disks, virtual hard disks (VHDs), and network adapters, as needed
- Create virtual machines from templates, VHDs, and from other virtual machines (modifying disk and network resources if needed)
- Modify the existing virtual machines
- Turn on and shut down virtual machines in batch mode
- Restart virtual machines
- Move virtual machines to a new host to manage availability and performance
- Create and restore virtual machine checkpoints

[Learn more](https://go.microsoft.com/fwlink/?LinkID=275796) about integration packs.

## System requirements

The VMM Integration Pack requires the following software to be installed and configured before you deploy the integration. For more information about how to install and configure the Orchestrator and the System Center Virtual Machine Manager application, see the respective product documentation.

- System Center - Orchestrator
- The integration pack and System Center components should be the same version.
- System Center - Virtual Machine Manager (VMM)
- Windows Management Framework

The activities from the VMM Integration Pack connect to a VMM Console, which in turn connects to a VMM management server. You can install this console on the Orchestrator runbook server or connect to the Administration console on another computer. If the Orchestrator components and the VMM Administration Console are installed on the same 64-bit computer, the VMM server must be in the same domain to be able to connect to it.

## Download the pack

::: moniker range="sc-orch-2025"

VMM Integration Pack for Orchestrator 2022 continues to work with Orchestrator 2025.

Download the Integration Pack for VMM [here](https://www.microsoft.com/download/details.aspx?id=104340)

::: moniker-end

::: moniker range="sc-orch-2022"

- [Download the pack for 2022](https://www.microsoft.com/download/details.aspx?id=104340)

::: moniker-end

::: moniker range="<=sc-orch-2019"
- [Download the pack for 2019](https://www.microsoft.com/download/details.aspx?id=58111&WT.mc_id=rss_alldownloads_all)
- [Download the pack for 2016](https://www.microsoft.com/download/details.aspx?id=54098)
::: moniker-end

## Register and deploy the pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to Runbook servers and Runbook Designers. [Learn more](how-to-add-an-integration-pack.md) about installation.

## Configure Windows Management Framework

The VMM Integration Pack uses Windows PowerShell Remoting to be configured between the Orchestrator runbook server and the computer running the VMM Administration Console. Windows PowerShell Remoting relies on Windows Remote Management (WinRM) to establish the communications between the two systems. You must perform the following tasks before you configure the VMM connection in the Runbook Designer.

>[!NOTE]
>The Runbook Designer will also connect to the computer running the VMM Administration Console when you are configuring activities from the VMM Integration Pack. If the Runbook Designer is installed on a different computer than the runbook server, then you will also need to configure Windows PowerShell and WinRM on that computer.

### Confirm PowerShell installation

PowerShell must be installed on both the Orchestrator runbook server, and the computer running the VMM console.

1. Open Registry Editor.
2. Expand the **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\PowerShell\\1\\PowerShellEngine** subkey.
3. Confirm that the runtime entry appears (at least version 2.0).

## Confirm Windows Remote Management installation

Windows Remote Management (at least version 2.0) must be installed and configured on both the Orchestrator runbook server and the computer running the VMM console. You can do this using the Local Group Policy Editor.

1. Select **Start** and then **Run**, enter **gpedit.msc**, and select **OK**.
2. Under **Local Computer Policy**, then expand **Computer Configuration**, then expand **Administrative Templates**, and then expand **Windows Components**
3. Verify that **Windows Remote Management (WinRM)** is listed.

For more information about how to install and configure WinRM 2.0, see [Installation and Configuration for Windows Remote Management](/windows/win32/winrm/installation-and-configuration-for-windows-remote-management).

### Specify Windows Remote Management trusted hosts

WinRM requires that you explicitly specify the name of any host computers that you are going to connect to. This enhances security by ensuring that the Orchestrator runbook server is connecting to the expected computer running the VMM Administration Console.

1. On the Orchestrator runbook server, open the **Local Group Policy Editor**. To do this, select **Start**, select **Run**, enter **gpedit.msc**, and select **OK**.
2. Under **Local Computer Policy**, then expand **Computer Configuration**, then expand **Administrative Templates**, then expand **Windows Components**, then expand **Windows Remote Management**, and then select **WinRM Client**.
3. Double-click **Trusted Hosts**.
4. In the **Trusted Hosts** dialog, select **Enabled**.
5. Add the name or IP address of the computer running the VMM Administration Console to the **TrustedHostsList** . Select **OK**.

### Set the PowerShell execution policy

The execution policy in Windows PowerShell determines which scripts must be digitally signed before they will run. By default, the execution policy is set to **Restricted** which prohibits loading any configuration files or running any scripts. To run the scripts in this integration pack, you must set the execution policy to **RemoteSigned** on both the Orchestrator runbook server and the computer running the VMM Administration Console.

1. Select **Start**, then **All Programs**, then **Accessories**, and then **Windows PowerShell**.
2. Right-click **Windows PowerShell** and select **Run As Administrator**. Select **Yes** when prompted by **User Account Control**.
3. Enter the following command and select **Enter**:

    **set-executionpolicy remotesigned**

For more information about how to configure the Windows PowerShell execution policy, see [Set-ExecutionPolicy](/powershell/module/microsoft.powershell.security/set-executionpolicy?viewFallbackFrom=powershell-6) in the Microsoft TechNet Library.

### Set the PowerShell remote connection quota

You can use WS-Management quotas in Windows PowerShell remoting to protect the Orchestrator runbook server and the computer running the VMM Administration Console from excessive resource use, both accidental and malicious. The **MaxConcurrentOperationsPerUser** quota setting in the **WSMan:\\&lt;ComputerName&gt;\\Service** node provides this protection by imposing a limit on the number of VMM objects that can run concurrently.

By default, MaxConcurrentOperationsPerUser is set to 5. This means that a maximum of five VMM objects can run concurrently across all VMM activities. If this default setting doesn't meet the needs of your organization, see [About\_Remote\_Troubleshooting](/powershell/module/microsoft.powershell.core/about/about_remote_troubleshooting) in the Microsoft TechNet Library for information about how to configure remote operations in Windows PowerShell.

>[!NOTE]
>The **MaxConcurrentOperationsPerUser** affects all Windows PowerShell objects whether or not they are from a runbook. If there are remote sessions from other applications, they will be included in this limit.

## Configure the connections

Once you've validated the WinRM configuration, you must add a **Connection** that defines communications between the Orchestrator runbook server and a computer running the VMM Administration Console. This configuration will include the credentials required to access VMM and the authentication protocol that should be used. When you configure actions from the VMM Integration Pack, you select a configuration that defines the connection that the activity should use. You can create multiple configurations if you've multiple VMM computers to connect to.

1. In the Runbook Designer, select the **Options** menu, and then select VMM.
2. On the **Connections** tab, select **Add** to begin the connection setup. The **Connection Entry** dialog appears.
3. In the **Name** box, enter a name for the connection. This could be the name of the VMM computer for example.
4. In the **Properties** box, enter a value for each property according to the table below.
5. Select **OK**.
6. Add any additional configurations as required.
7. Select **Finish**.

### VMM properties

| Property   | Description   |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| VMM Administrator Console   | The name or IP address of the computer running the VMM Administrator Console.   |
| User   | The name of a user with access to VMM. This user account must have permissions to the VMM Administration Console and to the VMM server to perform the actions requested by the activities.<br>If you leave this property empty, the configuration will use the credentials from the Runbook Service Account. If this account has appropriate permissions to VMM, then you don't need to provide credentials for the configuration.   |
| Domain   | The domain that the user account resides in.   |
| Password   | The password for the specified user account.   |
| Authentication Type (Remote only) | The type of authentication to use. This is only required if the runbook server and VMM Administration Console are installed on different computers.<br>The authentication method that you choose must be enabled in WinRM. You can enable the authentication methods using the **Local Group Policy Editor**. For more information see [Installation and Configuration for Windows Remote Management](/windows/win32/winrm/installation-and-configuration-for-windows-remote-management). |
| Port (Remote only)   | The port used for PowerShell remoting between the Orchestrator runbook server and the computer with the VMM Administration Console. This is only required if the runbook server and VMM Administration Console are installed on different computers.   |
| Use SSL (Remote only)   | Specifies whether SSL should be used for the connection. This is only required if the runbook server and VMM Administration Console are installed on different computers.   |
| Cache Session Timeout (min.)   | The number of minutes before the session will time out from lack of activity and need to reconnect.   |
| VMM Server   | The name of the VMM server that action will be performed on. Use **localhost** if the VMM Administration Console is installed on the VMM server.   |
