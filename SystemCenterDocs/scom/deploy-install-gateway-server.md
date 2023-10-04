---
ms.assetid: 212a5f25-9711-46b8-a466-775ef846dfc5
title: Install a Gateway Server
description: This article describes how to install the Operations Manager Gateway server.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/27/2023
ms.custom: intro-installation, engagement-fy23
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# Install a gateway server

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

Gateway servers are used to enable agent-management of computers that are outside the Kerberos trust boundary of management groups, such as in a domain that isn't trusted. The gateway server acts as a concentration point for agent-to-management server communication. Agents in domains that aren't trusted communicate with the gateway server, and the gateway server communicates with one or more management servers. Because communication between the gateway server and the management servers occurs over only one port (TCP 5723), that port is the only one that has to be opened on any intervening firewalls to enable management of multiple agent-managed computers. Multiple gateway servers can be placed in a single domain so that the agents can fail over from one to the other if they lose communication with one of the gateway servers. Similarly, a single gateway server can be configured to fail over between management servers so that no single point of failure exists in the communication chain.

Because the gateway server resides in a domain that isn't trusted by the domain that the management group is in, certificates must be used to establish each computer's identity, agent, gateway server, and management server. This arrangement satisfies the requirement of Operations Manager for mutual authentication.

You must ensure that your server meets the minimum system requirements for System Center - Operations Manager. For more information, see [System Requirements for System Center Operations Manager](./system-requirements.md).

::: moniker range="sc-om-2016"

> [!NOTE]
> If your security policies restrict TLS 1.0 and 1.1, installing a new Operations Manager 2016 gateway server role will fail because the setup media doesn't include the updates to support TLS 1.2. The only way you can install this role is by enabling TLS 1.0 on the system, apply Update Rollup 4, and then enable TLS 1.2 on the system. This limitation doesn't apply to Operations Manager version 1801.

::: moniker-end


## Deploy a gateway server

Follow these steps to deploy a gateway server:

1.  Request certificates for any computer in the agent, gateway server, management server chain.

2.  Import those certificates into the target computers by using the MOMCertImport.exe tool.

3.  Distribute the Microsoft.EnterpriseManagement.GatewayApprovalTool.exe to the management server.

4.  Run the Microsoft.EnterpriseManagement.GatewayApprovalTool.exe tool to initiate communication between the management server and the gateway.

5.  Install the gateway server.

## Prepare for installation

### Before you start

1.  Deployment of gateway servers requires certificates. You need to have access to a certification authority (CA). This can be a public CA such as VeriSign, or you can use Microsoft Certificate Services. This procedure provides the steps to request, obtain, and import a certificate from Microsoft Certificate Services.

2.  Reliable name resolution must exist between the agent-managed computers and the gateway server and between the gateway server and the management servers. This name resolution is typically done through DNS. However, if it isn't possible to get proper name resolution through DNS, it might be necessary to manually create entries in each computer's hosts file.

    > [!NOTE]
    > The hosts file is located in the `\Windows\system32\drivers\` directory, and it contains the directions for configuration.

### Obtain computer certificates from Microsoft Certificate Services

For more information, see [Active Directory Certificate Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831740(v=ws.11)).

### Distribute the Microsoft.EnterpriseManagement.GatewayApprovalTool

The Microsoft.EnterpriseManagement.GatewayApprovalTool.exe tool is needed only on the management server, and it only has to be run once.

#### Copy Microsoft.EnterpriseManagement.GatewayApprovalTool.exe to management servers

1.  From a target management server, open the Operations Manager installation media `\SupportTools\` (amd64 or x86) directory.

2.  Copy the Microsoft.EnterpriseManagement.GatewayApprovalTool.exe from the installation media to the Operations Manager installation directory.

### Register the gateway with the management group

This procedure registers the gateway server with the management group, and when this is completed, the gateway server appears in the Discovered Inventory view of the management group.

#### Run the gateway approval tool

1.  On the management server that was targeted during the gateway server installation, sign in with the Operations Manager Administrator account.

2.  Open a command prompt, and navigate to the Operations Manager installation directory or to the directory that you copied the Microsoft.EnterpriseManagement.GatewayApprovalTool.exe to.

3.  At the command prompt, run:
    ```
    Microsoft.EnterpriseManagement.GatewayApprovalTool.exe /ManagementServerName=<managementserverFQDN> /GatewayName=<GatewayFQDN> /Action=Create
    ```

    > [!NOTE]
    > To prevent the gateway server from initiating communication with a management server, include the */ManagementServerInitiatesConnection=True* parameter on the command.
    > **Example**
    > ```
    > "C:\Program Files\Microsoft System Center\Operations Manager\Server\Microsoft.EnterpriseManagement.GatewayApprovalTool.exe" /ManagementServerName=<managementserverFQDN> /GatewayName=<GatewayFQDN> /ManagementServerInitiatesConnection=True /Action=Create
    > ```

4.  If the approval is successful, you'll see `The approval of server <GatewayFQDN> completed successfully.`

5.  If you need to remove the gateway server from the management group, run the same command, but substitute the `/Action=Delete` flag for the `/Action=Create` flag.

6.  Open the Operations console to the Monitoring view. Select the Discovered Inventory view to see that the gateway server is present.

### Install gateway server

This procedure installs the gateway server. The server that is to be the gateway server should be a member of the same domain as the agent-managed computers that will be reporting to it.

> [!TIP]
> An installation will fail when starting Windows Installer (for example, installing a gateway server by double-clicking MOMGateway.msi) if the local security policy User Account Control: Run all administrators in Admin Approval Mode is enabled.

#### Run Operations Manager Gateway Windows Installer from a command prompt window

Follow these steps to run the Operations Manager Gateway Windows Installer from a command prompt window:

1.  On the Windows desktop, select **Start**, point to **Programs**, point to **Accessories**, right-click **Command Prompt**, and select **Run as administrator**.

2.  In the **Administrator: Command Prompt** window, navigate to the local drive that hosts the Operations Manager installation media.

3.  Navigate to the directory where the .msi file is located, enter the name of the .msi file, and then press ENTER.

Select the required tab to run the Operations Manager Gateway Windows Installer and install the gateway server:

# [Install the gateway server](#tab/InstallGatewayServer)

Follow these steps to install the gateway server:

1.  Sign in to the gateway server with Administrator rights.

2.  From the Operations Manager installation media, start **Setup.exe**.

3.  In the **Install** area, select the **Gateway management server** link.

4.  On the **Welcome** screen, select **Next**.

5.  On the **Destination Folder** page, accept the default, or select **Change** to select a different installation directory, and select **Next**.

6.  On the **Management Group Configuration** page, enter the target management group name in the **Management Group Name** field, enter the target management server name in the **Management Server** field, check that the **Management Server Port** field is **5723**, and select **Next**. This port can be changed if you've enabled a different port for management server communication in the Operations console.

7.  On the **Gateway Action Account** page, select the **Local System** account option, unless you've created a domain-based or local computer-based gateway Action account. Select **Next**.

8.  On the **Microsoft Update** page, optionally indicate if you want to use Microsoft Update, and select **Next**.

9. On the **Ready to Install** page, select **Install**.

10. On the **Completing**  page, select **Finish**.

# [Install the gateway server from the command prompt](#tab/InstallfromCommandPrompt)

Follow these steps to install the gateway server from the command prompt:

1.  Sign in to the gateway server with Administrator rights.

2.  Open the Command Prompt window by using the **Run as Administrator** option.

3.  Run the following command, where *path\Directory* is the location of the MOMGateway.msi, and *path\Logs* is the location where you want to save the log file. MOMGateway.msi can be found in the Operations Manager installation media.

    ```
    %WinDir%\System32\msiexec.exe /i path\Directory\MOMGateway.msi /qn /l*v C:\Logs\GatewayInstall.log
    ADDLOCAL=MOMGateway
    MANAGEMENT_GROUP="<ManagementGroupName>"
    IS_ROOT_HEALTH_SERVER=0
    ROOT_MANAGEMENT_SERVER_AD=<ParentMSFQDN>
    ROOT_MANAGEMENT_SERVER_DNS=<ParentMSFQDN>
    ACTIONS_USE_COMPUTER_ACCOUNT=0
    ACTIONSDOMAIN=<DomainName>
    ACTIONSUSER=<ActionAccountName>
    ACTIONSPASSWORD=<Password>
    ROOT_MANAGEMENT_SERVER_PORT=5723
    [INSTALLDIR=<path\Directory>]
    ```
---

### Import certificates with the MOMCertImport.exe tool

Perform this operation on each gateway server, management server, and computer that will be agent-managed and that is in a domain that isn't trusted.

#### Import computer certificates by using MOMCertImport.exe

1.  Copy the MOMCertImport.exe tool from the installation media `\SupportTools\` (amd64 or x86) directory to the root of the target server or to the Operations Manager installation directory if the target server is a management server.

2.  As an administrator, open a Command Prompt window and change the directory to the directory where MOMCertImport.exe is, and then run `momcertimport.exe /SubjectName <certificate subject name>`. This makes the certificate usable by Operations Manager. You may also run `momcertimport.exe` without any arguments to allow you to select from a GUI (Graphical User Interface) a list of Certificates in your Local Machine Personal Store.

### Configure gateway servers for failover between management servers

Although gateway servers can communicate with any management server in the management group, this must be configured. In this scenario, the secondary management servers are identified as targets for gateway server failover.

Use the Set-SCOMParentManagementServer command in the Operations Manager shell, as shown in the following example, to configure a gateway server to fail over to multiple management servers. The commands can be run from any Command Shell in the management group.

#### Configure gateway server failover between management servers

1.  Sign in to the management server with an account that is a member of the Administrators role for the management group.

2.  On the Windows desktop, select **Start**, point to **Programs**, point to **System Center Operations Manager**, and select **Command Shell**.

3.  In Command Shell, run the following commands:
    ```powershell
    $GatewayServer = Get-SCOMGatewayManagementServer -Name "ComputerName.Contoso.com"
    $FailoverServer = Get-SCOMManagementServer -Name "ManagementServer.Contoso.com","ManagementServer2.Contoso.com"
    Set-SCOMParentManagementServer -GatewayServer $GatewayServer -FailoverServer $FailoverServer
    ```

## Chain multiple gateway servers

It's sometimes necessary to chain multiple gateways together in order to monitor across multiple untrusted boundaries. This section describes how to chain multiple gateways together.

> [!NOTE]
> - You should install one gateway at a time, and verify that each newly installed gateway is configured correctly before adding another gateway in the chain.
> - When you add the gateways end of chain to the same resource pool, don't configure failover to the other chain by using the **Set-SCOMParentManagementServer** command. In such a scenario, the pool doesn't work as expected. For failover configuration and the resource pool to function together, the gateway end of the chain should have the same parent.

1. On the management server that was targeted during the gateway server installation, run the **Microsoft.EnterpriseManagement.GatewayApprovalTool.exe** tool to initiate communication between the management server and the gateway.
2. Open a command prompt, navigate to the Operations Manager installation directory, and then run the following: 
   ```
   Microsoft.EnterpriseManagement.GatewayApprovalTool.exe /ManagementServerName=<managementserverFQDN> /GatewayName=<GatewayFQDN> /Action=Create
   ```
3. Install the gateway server on a new server.
4. Configure the certificates between gateways in the same way that you would configure certificates between a gateway and a management server. The Health Service can only load and use a single certificate. Therefore, the same certificate is used by the parent and child of the gateway in the chain.

## Next steps

To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).
