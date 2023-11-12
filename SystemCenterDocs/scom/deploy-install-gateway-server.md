---
ms.assetid: 212a5f25-9711-46b8-a466-775ef846dfc5
title: Install a Gateway Server
description: This article describes how to install the Operations Manager Gateway server.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 11/11/2023
ms.custom: intro-installation, engagement-fy23
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# Install a gateway server

::: moniker range=">= sc-om-1801 <= sc-om-1807"
[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]
::: moniker-end

Gateway servers are used to enable monitoring of client computers that are outside the Kerberos trust boundary of management groups. Clients outside of the trust boundary are typically in a domain that doesn't have a two-way transitive trust, a DMZ, or a Workgroup. The gateway server acts as a proxy of sorts for agent-to-management server communication. Agents in domains that aren't trusted communicate with the gateway server, and the gateway server communicates with one or more management servers. Because communication between the gateway server and the management servers occurs over only one port (TCP 5723), we only need to open one port to enable management of multiple agent-managed computers, versus needing to have the same port opened across all agent servers.

For high availability, multiple gateway servers can be placed in a single domain so that the agents can fail over from one to the other if they lose communication with one of the gateway servers. Similarly, a single gateway server can be configured to fail over between management servers so that no single point of failure exists in the communication chain.

As gateway servers typically reside outside a Kerberos trust boundary, certificates must be used to establish each computer's identity. Without certificates, the systems might connect, but will be rejected due to authentication failures.

Before continuing, ensure that your server meets the minimum system requirements for System Center - Operations Manager. For more information, see [System Requirements for System Center Operations Manager](./system-requirements.md).

::: moniker range="sc-om-2016"
> [!NOTE]
> If your security policies restrict TLS 1.0 and 1.1, installing a new Operations Manager 2016 gateway server role will fail because the setup media doesn't include the updates to support TLS 1.2. The only way you can install this role is by enabling TLS 1.0 on the system, apply Update Rollup 4, and then enable TLS 1.2 on the system. This limitation doesn't apply to Operations Manager version 1801.
::: moniker-end

## Prerequisites

Overall steps to deploy a gateway server:

1. Determine if the domain the gateway is in has a two way transitive trust with the management group's domain. If it does not, we will need to generate certificates for the gateway and management server(s).
1. Approve the intended gateway server as a gateway using the Microsoft.EnterpriseManagement.GatewayApprovalTool.exe utility from a management server.
1. Install the gateway role on the intended server.
1. Import certificates into the target computers by using the MOMCertImport.exe tool.

### Certificates and Name Resolution

1. Deployment of gateway servers in domains without a two-way transitive trust, or in a workgroup, requires the use of certificates for authentication. The primary and failover management servers need one in addition to the gateway that is connecting to them. These certificates can come from a Microsoft Certificate Services CA, or a third-party CA, if configured correctly for Operations Manager. If you need assistance with creating these certificates, use the guide here: [Obtain a certificate for use with Windows Servers and System Center Operations Manager](obtain-certificate-windows-server-and-operations-manager.md)

2. Reliable name resolution must exist between the agent-managed computers and the gateway server, and between the gateway server and the management server. This name resolution is typically done through DNS. However, if it isn't possible to get proper name resolution through DNS, it might be necessary to manually create entries in each computer's hosts file.

    > [!IMPORTANT]
    > Forward and reverse name resolutions are checked before authentication will pass between servers. If we receive a different hostname or FQDN when checking the IP Address, then authentication will fail.
    > [!TIP]
    > The hosts file is located in the `%SystemRoot%\system32\drivers\etc` directory, and it contains the directions for configuration. This must be edited in a Notepad or other application run as an Administrator.

### Register the gateway with the management group

Before proceeding with gateway setup and installation, it's important to register and approve the intended gateway machine as a gateway first. If the gateway role is installed and runs before the server is approved to be a gateway, we run the risk of it being picked up as an agent, which can cause issues with the gateway role. 

These steps are to be performed from a management server, preferrably your primary or "RMSE" server.

1. There's an executable included with the SCOM installation media called "Microsoft.EnterpriseManagement.GatewayApprovalTool.exe," which can be found in the install media under `..\SupportTools\amd64\`.
1. Once located, copy this executable and the configuration file with the same name to one of the management server's installation path under `%ProgramFiles%\Microsoft System Center\Operations Manager\Server`
1. Open a Command Prompt as an administrator and navigate to the Operations Manager installation directory.
1. Use the following command to register the intended gateway as a gateway ensure to replace "managementServerFQDN" with the actual DNS entry for the management server, and "gatewayFQDN" with the DNS entry for the inteded gateway:

    ```cmd
    Microsoft.EnterpriseManagement.GatewayApprovalTool.exe /ManagementServerName=managementserverFQDN /GatewayName=GatewayFQDN /Action=Create
    ```

    > [!NOTE]
    > If you want to prevent the gateway server from initiating communication with a management server, include the */ManagementServerInitiatesConnection=True* parameter as used in the following command. Otherwise by default communication will initiate from the gateway itself.
    >
    > ```cmd
    > "Microsoft.EnterpriseManagement.GatewayApprovalTool.exe" /ManagementServerName=<managementserverFQDN/GatewayName=<GatewayFQDN/ManagementServerInitiatesConnection=True /Action=Create
    > ```

1. If the approval is successful, the message `The approval of server <GatewayFQDN> completed successfully.` will be returned.
1. If you need to remove the gateway server from the management group, run the same command, but substitute `/Action=Delete` for the `/Action=Create` flag.
1. Open the Operations console to the Monitoring view. Select the Discovered Inventory view to see that the gateway server is present. It shoud also be viewable under Administration > Device Management > Management Servers.

## Installation Process

Once the intended gateway server has been registered with the management group, it is time to install the role on the new gateway.

> [!NOTE]
> An installation will fail when starting Windows Installer (for example, installing a gateway server by double-clicking MOMGateway.msi) if the local security policy "User Account Control: Run all administrators in Admin Approval Mode" is enabled.
> [!TIP]
> If you experience issues during installation, the logs are located here: `%LocalAppData%\SCOM\Logs`

#### [Install using the GUI](#tab/install-using-the-gui)

Follow these steps to install the gateway server:

1. Sign into the gateway server with Administrator rights.
1. From the Operations Manager installation media, start **Setup.exe**.
1. In the **Install** area, select the **Gateway management server** link (not the large "Install" link, it will be towards the bottom of the window).
1. On the **Welcome** screen, select **Next**.
1. On the **Destination Folder** page, accept the default, or select **Change** to select a different installation directory, and select **Next**.
1. On the **Management Group Configuration** page, enter the target management group name in the **Management Group Name** field, enter the target management server name in the **Management Server** field, check that the **Management Server Port** field is **5723**, and select **Next**.
1. On the **Gateway Action Account** page, select the **Local System** account option, unless you're using a domain-based or local computer-based gateway Action account. Select **Next**.
1. On the **Microsoft Update** page, optionally indicate if you want to use Microsoft Update, and select **Next**. (Typically this selection should be No.)
1. On the **Ready to Install** page, select **Install**.
1. On the **Completing**  page, select **Finish**.

#### [Install using the Command Prompt](#tab/install-using-the-command-prompt)

Follow these steps to install the gateway server from the command prompt:

1. Sign in to the gateway server with Administrator rights.
1. Open the Command Prompt window by using the **Run as Administrator** option.
1. Run the following command, where *path\toInstaller* is the location of the MOMGateway.msi. The MOMGateway.msi can be found in the Operations Manager installation media under `..\gateway\amd64\`.

> [!TIP]
> The ^ characters are to allow for multi-line input into the console window and easier editing, if this does not work in your environment, remove the ^ characters and edit the command to be on one line.

```cmd
%WinDir%\System32\msiexec.exe /i path\toInstaller\gateway\amd64\MOMGateway.msi /qn /l*v %LocalAppData%\SCOM\Logs\GatewayInstall.log
ADDLOCAL=MOMGateway ^
MANAGEMENT_GROUP="ManagementGroupName" ^
IS_ROOT_HEALTH_SERVER=0 ^
ROOT_MANAGEMENT_SERVER_AD="ParentMSFQDN" ^
ROOT_MANAGEMENT_SERVER_DNS="ParentMSFQDN" ^
ACTIONS_USE_COMPUTER_ACCOUNT=0 ^
ACTIONSDOMAIN="DomainName" ^
ACTIONSUSER="ActionAccountName" ^
ACTIONSPASSWORD="Password" ^
ROOT_MANAGEMENT_SERVER_PORT=5723 ^
INSTALLDIR="C:\Program Files\System Center Operations Manager"
```

> [!IMPORTANT]
> The action account password cannot contain "illegal" characters in the Command Prompt, such as: `& < > ( ) @ ^ | "`.
> If it does, the installation will fail as it cannot parse the string, change the password to not contain these characters, and then wrap it in double quotes within the command itself.

---

### Import certificates with the MOMCertImport.exe tool

Perform this operation on each gateway server, and management server, along with any client computers that are to be agent managed in a workgroup.

1. The **MOMCertImport.exe** utility is located in the installation media under `..\SupportTools\amd64\`
1. Copy this file to the root of the target server or to the Operations Manager installation directory if the target server is a management server.
1. As an administrator, open a Command Prompt window and change the directory to the directory where MOMCertImport.exe is, and then run `momcertimport.exe /SubjectName <certificate subject name>`. This action makes the certificate usable by Operations Manager. You may also run `momcertimport.exe` without any arguments to allow you to select from a GUI (Graphical User Interface) a list of Certificates in your Local Machine Personal Store. 
1. Look in the OperationsManager event log for a 20053 eventID that confirms the import was successful. If this eventID is not present, observe the details of one of these IDs for any issues and make corrections accordingly: `20049,20050,20052,20066,20069,20077`

## Configure gateway servers for failover between management servers

By default, gateway servers will only communicate with one management server, their primary. If this connection is lost, the gateway and any attached agents will show as grey in the console and not be monitored. If you have multiple management servers, we can prevent this issue by configuring management servers that the gateway can failover to until the primary is available again. To configure a failovers:

We will be using the [Set-SCOMParentManagementServer](/powershell/module/operationsmanager/set-scomparentmanagementserver) cmdlet in the Operations Manager shell, as shown in the following example, to configure a gateway server to fail over to multiple management servers. The commands can be run from any Command Shell in the management group.

1. Sign into a management server using an account that is a member of the Operations Manager Administrators role.
1. From the Start Menu, run the **Operations Manager Shell** under the "Microsoft System Center" folder.
1. In the console, run the following commands:

    ```powershell
    $GatewayServer = Get-SCOMGatewayManagementServer -Name "ComputerName.Contoso.com"
    $FailoverServer = Get-SCOMManagementServer -Name "ManagementServer.Contoso.com","ManagementServer2.Contoso.com"
    Set-SCOMParentManagementServer -GatewayServer $GatewayServer -FailoverServer $FailoverServer
    ```

## Chain multiple gateway servers

While uncommon, it is sometimes necessary to chain multiple gateways together in order to monitor across multiple untrusted boundaries. This section describes how to chain multiple gateways together.

> [!NOTE]
>
> - You should install one gateway at a time, and verify that each newly installed gateway is configured correctly and showing as healthy in the SCOM console before adding another gateway in the chain.
> - When you add the gateways end of chain to the same resource pool, don't configure failover to the other chain by using the **Set-SCOMParentManagementServer** command. In such a scenario, the pool doesn't work as expected. For failover configuration and the resource pool to function together, the gateway end of the chain should have the same parent.

To configure a gateway chain, we will utilize the **Microsoft.EnterpriseManagement.GatewayApprovalTool.exe** tool just as we did for the initial gateway server. However, this time we need to set the "ManagementServerName" as the upstream gateway server in the chain. For example, if GatewayB is going to connect to GatewayA, then GatewayA is the "ManagementServer" in this scenario.

1. Sign onto one of your management servers that has the GatewayApprovalTool set up already.
1. Open a Command Prompt as an administrator and navigate to the directory where the tool is saved
1. Then run the below command to approve the downstream gateway server:

   ```cmd
   Microsoft.EnterpriseManagement.GatewayApprovalTool.exe /ManagementServerName=<managementserverFQDN> /GatewayName=<GatewayFQDN> /Action=Create
   ```

1. Install the gateway role on a new server.
1. Configure the certificates between GatewayA and GatewayB in the same way that you would configure certificates between a gateway and a management server. The Health Service can only load and use a single certificate. Therefore, the same certificate is used by the parent and child of the gateway in the chain.

## Next steps

To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).
