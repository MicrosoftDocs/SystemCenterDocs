---
ms.assetid: 212a5f25-9711-46b8-a466-775ef846dfc5
title: Install a Gateway Server
description: This article describes how to install an Operations Manager gateway server.
author: sepaugh
ms.author: lornesepaugh
manager: amanan
ms.date: 02/17/2025
ms.custom: intro-installation, engagement-fy23, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: install-set-up-deploy
---

# Install an Operations Manager gateway server

Organizations typically use gateway servers in System Center Operations Manager to enable monitoring of client computers that are outside the Kerberos trust boundary of management groups. However, gateways are also useful within the same domain. For example, you might have a requirement to segment the network and reduce the number of firewall ports opened. Another scenario is to use gateways for agents that are too "far away" to connect reliably a management server within the five-minute heartbeat interval.

Agents communicate directly with the gateway server, and the gateway server communicates with one or more management servers. Multiple gateway servers can be placed in a single domain so that the agents can fail over from one to the other if they lose communication with their primary gateway. Similarly, a single gateway server can be configured to fail over between management servers so that no single point of failure exists in the communication chain.

The gateway server acts as a proxy for agent-to-management server communication. It enables only one port to be opened between networks, in place of many.

Certificates must be used to establish each computer's identity when it's outside the Kerberos trust boundary. Without certificates, the systems might connect but refuse to communicate because they can't authenticate the connection.

## Prerequisites

- Ensure that your server meets the minimum [system requirements for Operations Manager](./system-requirements.md).

- Ensure that port 5723 is open between the gateway and management server, as defined in [Configuring a firewall for Operations Manager](plan-security-config-firewall.md).

[!INCLUDE [ntauthority-note-operations-manager.md](../includes/ntauthority-note-operations-manager.md)]

::: moniker range="sc-om-2016"

## Important considerations

If your security policies restrict TLS 1.0 and 1.1, installing a new Operations Manager 2016 gateway server role fails because the setup media doesn't include the updates to support TLS 1.2. The only way you can install this role is by enabling TLS 1.0 on the system, apply Update Rollup 4, and then enable TLS 1.2 on the system.
::: moniker-end

## Generate certificates and perform name resolution

Before you proceed with the gateway role installation in a standard scenario, certificates need to be generated for the gateway and management servers and installed in the certificate stores. If you're using the gateway and client servers in a workgroup scenario, the clients also need certificates.

### Certificates for authentication

Deployment of gateway servers in domains without a two-way transitive trust, or in a workgroup, requires the use of certificates for authentication. The primary and failover management servers need a certificate, in addition to the gateway that's connecting to them. These certificates can come from a Microsoft Certificate Services certificate authority (CA) or a non-Microsoft CA, if it's configured correctly for Operations Manager.

If you need assistance with creating these certificates, see [Obtain a certificate for use with Windows Servers and System Center Operations Manager](obtain-certificate-windows-server-and-operations-manager.md).

Keep these points in mind:

- Gateway servers that are in the same domain or in a shared trust boundary as the management group don't require certificates.
- If the gateway and agents are in a workgroup, you need certificates for each management server, gateway, and client computer, because there's no domain within a workgroup to facilitate authentication of systems.

### Reliable name resolution

Reliable name resolution must exist between the agent-managed computers and the gateway server, and between the gateway server and the management server. This name resolution is typically done through DNS. However, if it isn't possible to get proper name resolution through DNS, you might need to manually create entries in each computer's hosts file.

The hosts file, which is located in the `%SystemRoot%\system32\drivers\etc` directory, contains the directions for configuration. This file must be edited in Notepad or another application that you run as an administrator.

> [!IMPORTANT]
> Forward and reverse name resolutions are checked before authentication passes between servers. If you receive a different host name or fully qualified domain name (FQDN) when you're checking the IP address, authentication fails.

## Register the gateway with the management group

To prevent later problems, it's important to register and approve the intended gateway machine as a gateway before installation. Otherwise, you run the risk of the gateway being picked up as an agent.

Perform these steps from a management server, preferably your primary or Root Management Server Emulator (RMSE) server:

1. In the Operations Manager installation media, find `Microsoft.EnterpriseManagement.GatewayApprovalTool.exe` under `..\SupportTools\amd64\`.

1. Copy the executable file and the configuration file with the same name to the installation path under `%ProgramFiles%\Microsoft System Center\Operations Manager\Server`.

1. Open a command prompt as an administrator and go to the Operations Manager installation directory (for example, `cd %ProgramFiles%\Microsoft System Center\Operations Manager\Server`).

1. Use the following command to register the intended gateway as a gateway. Be sure to replace the server names with your own.

    ```cmd
    Microsoft.EnterpriseManagement.GatewayApprovalTool.exe /ManagementServerName=MS01.contoso.com /GatewayName=GW01.dmz.contoso.com /Action=Create
    ```

    > [!NOTE]
    > To prevent the gateway server from initiating communication with a management server, use the `/ManagementServerInitiatesConnection=True` parameter in the command. By default, the gateway initiates communication. But this parameter is useful if you want to avoid any inbound access to the primary domain from the network where the gateway is located. For example:
    >
    > ```cmd
    > Microsoft.EnterpriseManagement.GatewayApprovalTool.exe /ManagementServerName=MS01.contoso.com /GatewayName=GW01.dmz.contoso.com /ManagementServerInitiatesConnection=True /Action=Create
    > ```

1. If the approval is successful, the message `The approval of server <GatewayFQDN> completed successfully` appears.

1. If you need to remove the gateway server from the management group, run the same command but substitute `/Action=Create` for the `/Action=Delete` flag.

1. Open the operations console to the **Monitoring** view. Select the **Discovered Inventory** view to verify that the gateway server is present. It should also be viewable under **Administration** > **Device Management** > **Management Servers**.

## Install the gateway role

After the intended gateway server is registered with the management group, it's time to install the role on the new gateway.

> [!NOTE]
> An installation fails when you start Windows Installer (for example, installing a gateway server by double-clicking `MOMGateway.msi`) if the local security policy **User Account Control: Run all administrators in Admin Approval Mode** is enabled.
>
> If you experience problems during installation, you can find the logs in `%LocalAppData%\SCOM\Logs`.

### [GUI](#tab/install-using-the-gui)

1. Sign in to the gateway server with administrator rights.

1. From the Operations Manager installation media, start **Setup.exe**.

1. In the **Install** area, select the **Gateway management server** link (not the large **Install** link toward the bottom of the window).

1. On the **Welcome** screen, select **Next**.

1. On the **Destination Folder** page, accept the default, or select **Change** to select a different installation directory. Then select **Next**.

1. On the **Management Group Configuration** page, make the following selections, and then select **Next**:

   - In the **Management Group Name** box, enter the name of the target management group.
   - In the **Management Server** field, enter the name of the target management server.
   - Check that the **Management Server Port** field is **5723**.

1. On the **Gateway Action Account** page, select the **Local System** account option, unless you're using a gateway action account that's based on the domain or the local computer. Then select **Next**.

1. On the **Microsoft Update** page, optionally indicate if you want to use Microsoft Update, and then select **Next**. (Typically, this selection is **No**.)

1. On the **Ready to Install** page, select **Install**.

1. On the **Completing** page, select **Finish**.

### [Command prompt](#tab/install-using-the-command-prompt)

1. Sign in to the gateway server with administrator rights.

1. Open the Command Prompt window by using the **Run as Administrator** option.

1. Run one of the following commands. Keep these points about the commands in mind:

   - `path\to\Installer` is the path of the installation media.
   - You can find `MOMGateway.msi` in the Operations Manager installation media under `..\gateway\amd64\`.
   - The action account password can't contain illegal characters in the command prompt, such as: `& < > ( ) @ ^ | "`. If it does, the installation fails because it can't parse the string. Change the password to not contain these characters, and then wrap it in double quotation marks within the command.
   - The caret (`^`) character allows for multiple-line input in the command prompt for better readability and easier editing. If the command doesn't work in your environment, remove the `^` characters and ensure that the command is on a single line.

   If you're using the local system as the action account, use this command:

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

   If you're using a domain user as the action account, use this command:

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

---

## Import certificates by using the MOMCertImport.exe tool

Perform this operation on each gateway and management server, along with any client computers that will be agent managed in a workgroup:

1. Ensure that the certificates are installed.

1. In the installation media, find the `MOMCertImport.exe` file under `..\SupportTools\amd64\`.

1. Copy this file to the root directory of the target server or to the Operations Manager installation directory. For example: `%ProgramFiles%\Microsoft System Center\Operations Manager\Server`.

1. Open a command prompt as an administrator, and change the directory to the directory that contains `MOMCertImport.exe`. For example: `cd %ProgramFiles%\Microsoft System Center\Operations Manager\Server`.

1. Run the command `MOMCertImport.exe /SubjectName subjectNameFQDN`, where `subjectNameFQDN` is the defined subject on the certificate.

    You can also run `MOMCertImport.exe` without any arguments. You can then choose a certificate from a pop-up window that shows the certificates in the Local Machine Personal Store.

1. If the import is successful, the Microsoft Monitoring Agent service is restarted and event ID 20053 is logged to the Operations Manager event log. If this event ID isn't present, observe the details of one of the following IDs for any problems and make corrections accordingly: 20049, 20050, 20052, 20066, 20069, 20077.

> [!TIP]
> After the certificate is successfully imported, you can see a mirrored version of the thumbprint in the registry at `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\MachineSettings\ChannelCertificateSerialNumber`.

## Configure gateway servers for failover between management servers

By default, gateway servers communicate with only one management server: their primary. If this connection is lost, the gateway and any attached agents are unavailable in the console and can't be monitored. If you have multiple management servers, you can prevent this problem by configuring management servers that the gateway can fail over to until the primary is available again. The following steps show how to configure a failover.

The example commands in the following steps use the [Set-SCOMParentManagementServer](/powershell/module/operationsmanager/set-scomparentmanagementserver) cmdlet in the Operations Manager shell to configure a gateway server to fail over to multiple management servers. You can run the commands from any command shell in the management group.

1. Sign in to a management server by using an account that's a member of the Operations Manager Administrators role.

1. On the **Start** menu, under **Microsoft System Center**, run **Operations Manager Shell**.

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

It's sometimes necessary (though uncommon) to chain multiple gateways together in order to monitor them across multiple untrusted boundaries.

The following tips apply to chaining gateways:

- Install only one gateway at a time. Verify that each newly installed gateway appears as healthy in the Operations Manager console before you add another gateway in the chain.
- When you're adding gateways at the end of the chain to the same resource pool, *don't* configure failover to another chain by using the `Set-SCOMParentManagementServer` command. In such a scenario, the pool won't work as expected. For failover configuration and the resource pool to function together, the gateway end of the chain should have the same parent.

To configure a gateway chain, use the `Microsoft.EnterpriseManagement.GatewayApprovalTool.exe` tool, just as you did for the initial gateway server. But this time, you need to set `ManagementServerName` as the upstream gateway server in the chain. For example, if GW02 is going to connect to GW01, then `GW01` is the `ManagementServer` value in this scenario.

1. Sign in to a management server where the `GatewayApprovalTool.exe` tool is already set up.

1. Open a command prompt as an administrator and go to the directory where the tool is saved.

1. Run the following command to approve the downstream gateway server. Be sure to replace the server names with your own.

   ```cmd
   Microsoft.EnterpriseManagement.GatewayApprovalTool.exe /ManagementServerName=GW01.dmz.contoso.com /GatewayName=GW02.dmz.contoso.com /Action=Create
   ```

1. Install the gateway role on a new server.

1. Configure the certificates between GW01 and GW02 in the same way that you would configure certificates between a gateway and a management server. The Health Service can load and use only a single certificate. Therefore, the parent and child of the gateway in the chain use the same certificate.

## Related content

- To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed deployment of Operations Manager](deploy-distributed-deployment.md).
