---
ms.assetid: 
title: Remove a Gateway Server from a Management Group
description: This article describes the procedure to remove a gateway server from  a Management Group.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
---

# Remove a Gateway Server from a Management Group

Throughout the life cycle of your System Center – Operations Manager implementation, you might need to modify the structure and configuration of your deployment.

In the case of Gateway servers, these types of changes can stem from the decommissioning of an untrusted domain so that monitoring is no longer required or from the old server hardware being replaced with new hardware.  

This article describes the procedure to remove a Gateway server from a Management Group.

## Overview of Decommissioning a Gateway Server

1. Configure all the objects that are being managed by the Gateway server to use a different primary management server or Gateway. For an agent-managed computer, this means using either another Gateway server or a management server.

2. Uninstall the Gateway server software from the server.

3. Delete the Gateway server from the management group.

## Configure Managed Objects to use an alternate Primary Management Server

Gateway servers can manage three different types of objects:  

- Agent-managed computers

- Agentless-managed computers

- Network devices acting as a proxy agent

### Configure agent-managed computers using the Operations console

1. Sign-in to a management server with Administrator privileges for the Operations Manager management group.

2. In the Operations console, select **Administration**.

3. In the Administration pane, select **Administration** > **Device Management**, and then select **Agent Managed**.

4. In the Agent Managed pane, select the computers for which you want to change the primary management server, right-click them, and then select **Change Primary Management Server**.

     >[!Note]
     >The **Change Primary Management Server** option will be unavailable if Active Directory Domain Services was used to assign any of the selected computers to the management group using [Active Directory Integration for agent assignment](/system-center/scom/manage-ad-integration-agent-assignment?view=sc-om-2022). The **Change Primary Management Server** option can be disabled due to the Agents not being remotely managed.

5. In the Change Management Server dialog, select the new management server from the list, and then select **OK**. The change takes effect on the agent after its next update interval.

Alternatively, this configuration can be changed on the agent-managed computer itself using either of the following two procedures.

- [Change the primary management server for agent-managed computers using the MOMAgent.msi setup wizard](#change-the-primary-management-server-for-agent-managed-computers-using-the-momagentmsi-setup-wizard)

- [Change the primary management server for agent-managed computers using MOMAgent.msi from the command line](#change-the-primary-management-server-for-agent-managed-computers-using-momagentmsi-from-the-command-line)

#### Change the primary management server for agent-managed computers using the MOMAgent.msi setup wizard

1. Sign-in to the agent-managed computer with an account that is a member of the Administrators security group for the computer.

2. In **Add or Remove Programs**, select **Change** for System Center Operations Manager Agent.

     >[!Note]
     >The **Agent Setup Wizard** can also be run by double-clicking `MOMAgent.msi`, which is located on the Operations Manager installation media.

3. In the **System Center – Operations Manager Agent Setup** Wizard, select **Next**.

4. On the **Program Maintenance** page, select **Modify**, and then select **Next**.

5. On the **Management Group Configuration** page, leave **Specify Management Group information** selected, and then select **Next.**

6. In the next **Management Group Configuration** page, follow these steps:

     1. Enter the name of the **Management Server**.
     1. Enter a value for **Management Server Port** or retain the default value **5723**.
     1. Select **Next**.

7. On the **Ready to Install** page, review the settings, and select **Install** to display the **Installing the System Center - Operations Manager Agent** page.

8. When the **Completing the System Center - Operations Manager Agent Setup wizard** page displays, select **Finish**.

#### Change the primary management server for agent-managed computers using MOMAgent.msi from the command line

1. Sign-in to the agent-managed computer with an account that is a member of the Administrators security group for the computer.

2. Open the command window.

3. At the prompt, run the following command:

      ``` 
      %WinDir%\System32\msiexec.exe /i \\path\Directory\MOMAgent.msi /qn USE_SETTINGS_FROM_AD=0 MANAGEMENT_GROUP=MG1 MANAGEMENT_SERVER_DNS=MS2.Domain1.net
      ```

      This command reconfigures the agent to use **MS2.Domain1.net** as its primary management server for management group **MG1**.

>[!Note]
>- Microsoft Windows Installer public properties must be in uppercase, such as *PROPERTY=value*. For more information about Windows Installer, see [Windows Installer](/windows/win32/msi/windows-installer-portal) in the Microsoft Developer Network library. 
>- If the Domain Name System (DNS) and Active Directory names for the management server differ, the **MANAGEMENT_SERVER_AD_NAME** property also needs to be set to the fully qualified Active Directory Domain Services name.

### Redirect Agentless-Managed Computers and Network devices

#### Configure Agentless-Managed computers to use an alternate proxy agent using PowerShell

The following PowerShell script allows you to configure the proxy agent for agentless-managed computers to use another management server or gateway.

Edit the variable section of the PowerShell script as appropriate.

```powershell
#------------------------------- 
# Variables Section 
#------------------------------- 
$FromGatewayServer = 'GW01-2019.contoso-2019.com' # Management Server or Gateway Server to move FROM

$ToGatewayServer = 'MS01-2019.contoso-2019.com' # Management Server or Gateway Server to move TO 
#------------------------------- 

$MSList = Get-SCOMManagementServer 
$FromGatewayServer = $MSList | Where-Object {$_.Name -match $FromGatewayServer} 
$ToGatewayServer =  $MSList | Where-Object {$_.Name -match $ToGatewayServer} 

Get-SCOMAgentlessManagedComputer | Where-Object {$_.ProxyAgentPrincipalName -match $FromGatewayServer.DisplayName} | Set-SCOMAgentlessManagedComputer -ManagedByManagementServer $ToGatewayServer -PassThru 

```

#### Change the proxy agent for agentless-managed computers and network devices

1. Sign-in to a management server computer with an account that is a member of the Operations Manager Administrators role for the Operations Manager management group.

2. In the Operations console, select **Administration**.

3. In the Administration pane, expand **Administration**, expand **Device Management**, and then select **Agentless Managed**. If you are working with a network device, select **Device Management** and then **Network Devices**.

4. In the Agentless Managed pane, select the agentless-managed computers for which you want to change the proxy agent, right-click them, and then select **Change Proxy Agent**. Or if you are working with a network device, in the **Network Devices** pane, select the network devices for which you want to change the proxy agent, right-click them, and then select **Change Proxy Agent**.

5. In the **Change Proxy Agent** dialog, select the computer you want to as the new proxy agent, and then select **OK**.

## Uninstall System Center Operations Manager Gateway

To uninstall System Center Operations Manager Gateway, follow these steps:

1. Sign-in to the Gateway server with an account that has administrative rights.

2. Open **Control Panel** > **Programs and Features**.

3. Right-click **System Center Operations Manager Gateway**, and then select **Uninstall**.

### Distribute the Microsoft.EnterpriseManagement.GatewayApprovalTool

The `Microsoft.EnterpriseManagement.GatewayApprovalTool.exe` tool is required only on the management server and must be run only once.

### Copy Microsoft.EnterpriseManagement.GatewayApprovalTool.exe to management servers

1. From a target management server, open the Operations Manager installation media `\SupportTools\` (amd64 or x86) directory.

2. Copy `Microsoft.EnterpriseManagement.GatewayApprovalTool.exe` from the installation media to the Operations Manager installation directory.

## Delete the Gateway Server from the Management Group

The Gateway server is removed from the Management Servers view in the management group.

### Run the Gateway approval tool

1. On the management server that was targeted during the Gateway server installation, sign-in with the Operations Manager Administrator account.

2. Open a command prompt and navigate to the Operations Manager installation directory or to the directory to which you copied the `Microsoft.EnterpriseManagement.GatewayApprovalTool.exe`.

3. At the command prompt, run:

      ```powershell
      Microsoft.EnterpriseManagement.GatewayApprovalTool.exe /ManagementServerName=<managementserverFQDN> /GatewayName=<GatewayFQDN> /Action=Delete 
      ```

4. If the removal is successful, you'll see:
      The removal of server *GatewayFQDN* from the management group completed successfully.  If you have not already uninstalled the Gateway Server from *GatewayFQDN*, it may become a managed agent depending on your Auto Approval configuration.  If this is the case, you will need to uninstall it from the Agent Management view.

5. Open **Operations console** in Administration view and select **Management Servers view** to ensure that the Gateway server is uninstalled.
