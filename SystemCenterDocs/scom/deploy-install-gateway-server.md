---
ms.assetid: 212a5f25-9711-46b8-a466-775ef846dfc5
title: Install a Gateway Server
description: This article describes how to install the Operations Manager Gateway server.
author: sepaugh
ms.author: lornesepaugh
manager: amanan
ms.date: 02/17/2025
ms.service: system-center
ms.subservice: operations-manager
ms.topic: install-set-up-deploy
ms.custom:
  - intro-installation
  - engagement-fy23
  - engagement-fy24
  - sfi-ropc-nochange
---

# Install a gateway server

Gateway servers are typically used to enable monitoring of client computers that are outside the Kerberos trust boundary of management groups. However, gateways are also useful within the same domain, as if there's a requirement to segment the network and reduce the number of firewall ports opened. Another scenario is to use gateways for agents that are too "far away" to connect reliably a management server within the five-minute heartbeat interval.

Agents communicate directly with the gateway server, and the gateway server communicates with one or more management servers. Multiple gateway servers can be placed in a single domain so that the agents can fail over from one to the other if they lose communication with their primary gateway. Similarly, a single gateway server can be configured to fail over between management servers so that no single point of failure exists in the communication chain. The gateway server acts as a proxy for agent-to-management server communication, enabling only one port to be opened between networks in place of many. Certificates must be used to establish each computer's identity when outside the Kerberos trust boundary. Without certificates, the systems might connect but refuse to communicate due to being unable to authenticate the connection.

Before continuing, ensure that your server meets the minimum system requirements for System Center - Operations Manager. For more information, see [System Requirements for System Center Operations Manager](./system-requirements.md).

[!INCLUDE [ntauthority-note-operations-manager.md](../includes/ntauthority-note-operations-manager.md)]

::: moniker range="sc-om-2016"
> [!NOTE]
> If your security policies restrict TLS 1.0 and 1.1, installing a new Operations Manager 2016 gateway server role fails because the setup media doesn't include the updates to support TLS 1.2. The only way you can install this role is by enabling TLS 1.0 on the system, apply Update Rollup 4, and then enable TLS 1.2 on the system.
::: moniker-end

## Prerequisites

There are three major things that we need to have ready and in place before proceeding with the gateway role installation in a standard scenario:

1. Certificates need to be generated for the gateway and management servers and installed into the certificate stores.
    - If the gateway and client servers are being used in a Workgroup scenario, then the clients also need certificates.
1. The intended gateway server needs to be "Approved" to be a gateway within the management group before installation.
1. Port 5723 must be opened between the gateway and management server as defined in the guide here: [Configuring a Firewall for Operations Manager](plan-security-config-firewall.md)

### Certificates and Name resolution

1. Deployment of gateway servers in domains without a two-way transitive trust, or in a workgroup, requires the use of certificates for authentication. The primary and failover management servers need one in addition to the gateway that is connecting to them. These certificates can come from a Microsoft Certificate Services CA, or a non-Microsoft CA, if configured correctly for Operations Manager. If you need assistance with creating these certificates, use the guide here: [Obtain a certificate for use with Windows Servers and System Center Operations Manager](obtain-certificate-windows-server-and-operations-manager.md)

    > [!NOTE]
    >
    > - Gateway servers that are in the same domain or in a shared trust boundary as the management group don't require certificates.
    > - If the gateway and agents are in a workgroup, then we need certificates for each management server, gateway, and client computer as there's no domain within a workgroup to facilitate authentication of systems.

2. Reliable name resolution must exist between the agent-managed computers and the gateway server, and between the gateway server and the management server. This name resolution is typically done through DNS. However, if it isn't possible to get proper name resolution through DNS, it might be necessary to manually create entries in each computer's hosts file.

    > [!IMPORTANT]
    > Forward and reverse name resolutions are checked before authentication passes between servers. If we receive a different hostname or FQDN when checking the IP Address, then authentication fails.
    > [!TIP]
    > The hosts file, which is located in the `%SystemRoot%\system32\drivers\etc` directory, contains the directions for configuration. This file must be edited in a Notepad or other application run as an Administrator.

### Register the gateway with the management group

To prevent later issues, it's important to register and approve the intended gateway machine as a gateway before installation, otherwise we run the risk of the gateway being picked up as an agent.

These steps are to be performed from a management server, preferably your primary or "RMSE" server.

1. There's an executable included with the Operations Manager installation media called "Microsoft.EnterpriseManagement.GatewayApprovalTool.exe," which can be found in the install media under `..\SupportTools\amd64\`.
1. Once located, copy this executable and the configuration file with the same name to the installation path under: `%ProgramFiles%\Microsoft System Center\Operations Manager\Server`
1. Open a Command Prompt as an administrator and navigate to the Operations Manager installation directory. (ex. `cd %ProgramFiles%\Microsoft System Center\Operations Manager\Server`)
1. Use the following command to register the intended gateway as a gateway ensure to replace the server names with your own:

    ```cmd
    Microsoft.EnterpriseManagement.GatewayApprovalTool.exe /ManagementServerName=MS01.contoso.com /GatewayName=GW01.dmz.contoso.com /Action=Create
    ```

    > [!NOTE]
    > To prevent the gateway server from initiating communication with a management server, use the **/ManagementServerInitiatesConnection=True** parameter in the command. By default, the gateway initiates communication, but this parameter is useful if you want to avoid any inbound access to the primary domain from the network where the gateway is located. For example:
    >
    > ```cmd
    > Microsoft.EnterpriseManagement.GatewayApprovalTool.exe /ManagementServerName=MS01.contoso.com /GatewayName=GW01.dmz.contoso.com /ManagementServerInitiatesConnection=True /Action=Create
    > ```

1. If the approval is successful, the message `The approval of server <GatewayFQDN> completed successfully.` is returned.
1. If you need to remove the gateway server from the management group, run the same command, but substitute `/Action=Create` for the `/Action=Delete` flag.
1. Open the Operations console to the Monitoring view. Select the Discovered Inventory view to see that the gateway server is present. It should also be viewable under Administration > Device Management > Management Servers.

## Installation process

Once the intended gateway server is registered with the management group, it's time to install the role on the new gateway.

> [!NOTE]
> An installation fails when starting Windows Installer (for example, installing a gateway server by double-clicking MOMGateway.msi) if the local security policy "User Account Control: Run all administrators in Admin Approval Mode" is enabled.
> [!TIP]
> If you experience issues during installation, the logs are located here: `%LocalAppData%\SCOM\Logs`

#### [Install using the GUI](#tab/install-using-the-gui)

Follow these steps to install the gateway server:

1. Sign into the gateway server with Administrator rights.
1. From the Operations Manager installation media, start **Setup.exe**.
1. In the **Install** area, select the **Gateway management server** link (not the large "Install" link, towards the bottom of the window).
1. On the **Welcome** screen, select **Next**.
1. On the **Destination Folder** page, accept the default, or select **Change** to select a different installation directory, and select **Next**.
1. On the **Management Group Configuration** page, enter the target management group name in the **Management Group Name** field, enter the target management server name in the **Management Server** field, check that the **Management Server Port** field is **5723**, and select **Next**.
1. On the **Gateway Action Account** page, select the **Local System** account option, unless you're using a domain-based or local computer-based gateway Action account. Select **Next**.
1. On the **Microsoft Update** page, optionally indicate if you want to use Microsoft Update, and select **Next**. (Typically, this selection should be No.)

1. On the **Ready to Install** page, select **Install**.
1. On the **Completing** page, select **Finish**.

#### [Install using the Command Prompt](#tab/install-using-the-command-prompt)

Follow these steps to install the gateway server from the command prompt:

1. Sign in to the gateway server with Administrator rights.
1. Open the Command Prompt window by using the **Run as Administrator** option.
1. Run the following command, where **path\to\Installer** is the path of the installation media. The MOMGateway.msi can be found in the Operations Manager installation media under `..\gateway\amd64\`.

> [!TIP]
> The `^` character is used to allow for multi-line input in the Command Prompt for better readability and easier editing. If the command doesn't work in your environment, remove the `^` characters and ensure the command is on a single line.

If you're using **LocalSystem** as the action account:

```cmd
%WinDir%\System32\msiexec.exe /i C:\path\to\Installer\gateway\amd64\MOMGateway.msi /qn /l*v %LocalAppData%\SCOM\Logs\GatewayInstall.log ^
AcceptEndUserLicenseAgreement=1 ^
ADDLOCAL=MOMGateway ^
MANAGEMENT_GROUP="ManagementGroupName" ^
IS_ROOT_HEALTH_SERVER=0 ^
ROOT_MANAGEMENT_SERVER_AD="MS01.contoso.com" ^
ROOT_MANAGEMENT_SERVER_DNS="MS01.contoso.com" ^
ACTIONS_USE_COMPUTER_ACCOUNT=1 ^
ROOT_MANAGEMENT_SERVER_PORT=5723 ^
INSTALLDIR="C:\Program Files\System Center Operations Manager"
```

If you're using a **Domain User** as the action account:

```cmd
%WinDir%\System32\msiexec.exe /i C:\path\to\Installer\gateway\amd64\MOMGateway.msi /qn /l*v %LocalAppData%\SCOM\Logs\GatewayInstall.log ^
AcceptEndUserLicenseAgreement=1 ^
ADDLOCAL=MOMGateway ^
MANAGEMENT_GROUP="ManagementGroupName" ^
IS_ROOT_HEALTH_SERVER=0 ^
ROOT_MANAGEMENT_SERVER_AD="MS01.contoso.com" ^
ROOT_MANAGEMENT_SERVER_DNS="MS01.contoso.com" ^
ACTIONS_USE_COMPUTER_ACCOUNT=0 ^
ACTIONSDOMAIN="DomainName" ^
ACTIONSUSER="ActionAccountName" ^
ACTIONSPASSWORD="Password" ^
ROOT_MANAGEMENT_SERVER_PORT=5723 ^
INSTALLDIR="C:\Program Files\System Center Operations Manager"
```

> [!IMPORTANT]
> The action account password can't contain "illegal" characters in the Command Prompt, such as: `& < > ( ) @ ^ | "`.
> If it does, the installation fails as it can't parse the string, change the password to not contain these characters, and then wrap it in double quotes within the command itself.

---

### Import certificates with the MOMCertImport.exe tool

Perform this operation on each gateway and management server, along with any client computers that are to be agent managed in a workgroup.

1. Ensure the certificates are installed before continuing
1. Locate the **MOMCertImport.exe** file located in the installation media under `..\SupportTools\amd64\`
1. Copy this file to the root directory of the target server or to the Operations Manager installation directory
    - For example: `%ProgramFiles%\Microsoft System Center\Operations Manager\Server`).
1. Open a Command Prompt as an administrator, and change the directory to the directory where MOMCertImport.exe is.
    - For example: `cd %ProgramFiles%\Microsoft System Center\Operations Manager\Server`
1. Then run the command `MOMCertImport.exe /SubjectName subjectNameFQDN`, where "subjectNameFQDN" is the defined subject on the certificate.
    - You can also run `MOMCertImport.exe` without any arguments to allow you to choose a certificate from a pop-up window that shows the certificates in the Local Machine Personal Store.
1. If successful, the Microsoft Monitoring Agent service is restarted and eventID 20053 is logged to the Operations Manager event log. If this eventID isn't present, observe the details of one of these IDs for any issues and make corrections accordingly: `20049,20050,20052,20066,20069,20077`

> [!TIP]
> Once the certificate is successfully imported, you can see a mirrored version of the thumbprint in the registry here:
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\MachineSettings\ChannelCertificateSerialNumber`

## Configure gateway servers for failover between management servers

By default, gateway servers only communicate with one management server, their primary. If this connection is lost, the gateway and any attached agents show as grey in the console and not be monitored. If you have multiple management servers, we can prevent this issue by configuring management servers that the gateway can fail over to until the primary is available again. To configure a failover:

We're using the [Set-SCOMParentManagementServer](/powershell/module/operationsmanager/set-scomparentmanagementserver) cmdlet in the Operations Manager shell, as shown in the following example, to configure a gateway server to fail over to multiple management servers. The commands can be run from any Command Shell in the management group.

1. Sign into a management server using an account that is a member of the Operations Manager Administrators role.
1. From the Start Menu, run the **Operations Manager Shell** under the "Microsoft System Center" folder.
1. In the console, run the following commands:

    ```powershell
    $GatewayServer = Get-SCOMGatewayManagementServer -Name "GW01.dmz.contoso.com"
    $FailoverServer = Get-SCOMManagementServer -Name "MS02.Contoso.com","MS03.Contoso.com"
    Set-SCOMParentManagementServer -GatewayServer $GatewayServer -FailoverServer $FailoverServer
    ```

    > [!NOTE]
    > You can't set a failover server to be the same as the primary server without changing the primary at the same time, or first. If you want to change the primary and set it to a secondary, use the following commands:
    >
    >```powershell
    >$GatewayServer = Get-SCOMGatewayManagementServer -Name "GW01.dmz.contoso.com"
    >$PrimaryServer = Get-SCOMManagementServer -Name "MS02.Contoso.com"
    >$FailoverServer = Get-SCOMManagementServer -Name "MS01.Contoso.com","MS03.Contoso.com"
    >Set-SCOMParentManagementServer -GatewayServer $GatewayServer -PrimaryServer $PrimaryServer -FailoverServer $FailoverServer
    >```

## Chain multiple gateway servers

While uncommon, it's sometimes necessary to chain multiple gateways together in order to monitor across multiple untrusted boundaries. This section describes how to chain multiple gateways together.

> [!NOTE]
>
> - Only install one gateway at a time. Verify that each newly installed gateway is showing as healthy in the Operations Manager console before adding another gateway in the chain.
> - When adding gateways at the end of the chain to the same resource pool, **don't** configure failover to another chain by using the **Set-SCOMParentManagementServer** command. In such a scenario, the pool won't work as expected. For failover configuration and the resource pool to function together, the gateway end of the chain should have the same parent.

To configure a gateway chain, we utilize the **Microsoft.EnterpriseManagement.GatewayApprovalTool.exe** tool just as we did for the initial gateway server. However, this time we need to set the "ManagementServerName" as the upstream gateway server in the chain. For example, if GW02 is going to connect to GW01, then GW01 is the "ManagementServer" in this scenario.

1. Sign onto one of your management servers that has the GatewayApprovalTool set up already.
1. Open a Command Prompt as an administrator and navigate to the directory where the tool is saved
1. Then run the following command to approve the downstream gateway server, ensuring to replace the server names with your own:

   ```cmd
   Microsoft.EnterpriseManagement.GatewayApprovalTool.exe /ManagementServerName=GW01.dmz.contoso.com /GatewayName=GW02.dmz.contoso.com /Action=Create
   ```

1. Install the gateway role on a new server.
1. Configure the certificates between GW01 and GW02 in the same way that you would configure certificates between a gateway and a management server. The Health Service can only load and use a single certificate. Therefore, the same certificate is used by the parent and child of the gateway in the chain.

## Next steps

To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).
