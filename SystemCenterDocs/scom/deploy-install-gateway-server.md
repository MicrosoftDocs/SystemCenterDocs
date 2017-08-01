---
ms.assetid: 212a5f25-9711-46b8-a466-775ef846dfc5
title: Install a Gateway Server
description: This article describes how to install the Operations Manager Gateway server.  
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 08/01/2017
ms.custom: na
ms.prod: system-center-2016
ms.technology: operations-manager
ms.topic: article
---

# Install a gateway server

>Applies To: System Center 2016 - Operations Manager

Gateway servers are used to enable agent-management of computers that are outside the Kerberos trust boundary of management groups, such as in a domain that is not trusted. The gateway server acts as a concentration point for agent-to-management server communication. Agents in domains that are not trusted communicate with the gateway server and the gateway server communicates with one or more management servers. Because communication between the gateway server and the management servers occurs over only one port (TCP 5723), that port is the only one that has to be opened on any intervening firewalls to enable management of multiple agent-managed computers. Multiple gateway servers can be placed in a single domain so that the agents can failover from one to the other if they lose communication with one of the gateway servers. Similarly, a single gateway server can be configured to failover between management servers so that no single point of failure exists in the communication chain.

Because the gateway server resides in a domain that is not trusted by the domain that the management group is in, certificates must be used to establish each computer's identity, agent, gateway server, and management server. This arrangement satisfies the requirement of Operations Manager for mutual authentication.

## How to deploy a gateway server

1.  Request certificates for any computer in the agent, gateway server, management server chain.

2.  Import those certificates into the target computers by using the MOMCertImport.exe tool.

3.  Distribute the Microsoft.EnterpriseManagement.GatewayApprovalTool.exe to the management server.

4.  Run the Microsoft.EnterpriseManagement.GatewayApprovalTool.exe tool to initiate communication between the management server and the gateway

5.  Install the gateway server.

## Preparing for installation

#### Before you start

1.  Deployment of gateway servers requires certificates. You need to have access to a certification authority (CA). This can be a public CA such as VeriSign, or you can use Microsoft Certificate Services. This procedure provides the steps to request, obtain, and import a certificate from Microsoft Certificate Services.

2.  Reliable name resolution must exist between the agent-managed computers and the gateway server and between the gateway server and the management servers. This name resolution is typically done through DNS. However, if it is not possible to get proper name resolution through DNS, it might be necessary to manually create entries in each computer's hosts file.

    > [!NOTE]
    > The hosts file is located in the \Windows\system32\drivers\ directory, and it contains directions for configuration.

### Obtaining computer certificates from Microsoft Certificate Services

For more information, see [Active Directory Certificate Services](https://technet.microsoft.com/en-us/library/hh831740.aspx)

### Distributing the Microsoft.EnterpriseManagement.GatewayApprovalTool

The Microsoft.EnterpriseManagement.GatewayApprovalTool.exe tool is needed only on the management server, and it only has to be run once.

##### To copy Microsoft.EnterpriseManagement.GatewayApprovalTool.exe to management servers

1.  From a target management server, open the Operations Manager installation media \SupportTools\<platform\> (amd64 or x86) directory.

2.  Copy the Microsoft.EnterpriseManagement.GatewayApprovalTool.exe from the installation media to the Operations Manager installation directory.

### Registering the gateway with the management group

This procedure registers the gateway server with the management group, and when this is completed, the gateway server appears in the Discovered Inventory view of the management group.

##### To run the gateway approval tool

1.  On the management server that was targeted during the gateway server installation, log on with the Operations Manager Administrator account.

2.  Open a command prompt, and navigate to the Operations Manager installation directory or to the directory that you copied the Microsoft.EnterpriseManagement.gatewayApprovalTool.exe to.

3.  At the command prompt, run `Microsoft.EnterpriseManagement.gatewayApprovalTool.exe /ManagementServerName=<managementserverFQDN> /GatewayName=<GatewayFQDN> /Action=Create`

    > [!NOTE] 
    > To prevent the gateway server from initiating communication with a management server, include the */ManagementServerInitiatesConnection* parameter on the command line.  

4.  If the approval is successful, you will see `The approval of server <GatewayFQDN> completed successfully.`

5.  If you need to remove the gateway server from the management group, run the same command, but substitute the `/Action=Delete` flag for the `/Action=Create` flag.

6.  Open the Operations console to the Monitoring view. Select the Discovered Inventory view to see that the gateway server is present.

### Installing gateway server

This procedure installs the gateway server. The server that is to be the gateway server should be a member of the same domain as the agent-managed computers that will be reporting to it.

> [!TIP]
> An installation will fail when starting Windows Installer (for example, installing a gateway server by double-clicking MOMGateway.msi) if the local security policy User Account Control: Run all administrators in Admin Approval Mode is enabled.

##### To run Operations Manager Gateway Windows Installer from a Command Prompt window

1.  On the Windows desktop, click **Start**, point to **Programs**, point to **Accessories**, right-click **Command Prompt**, and then click **Run as administrator**.

2.  In the **Administrator: Command Prompt** window, navigate to the local drive that hosts the Operations Manager installation media.

3.  Navigate to the directory where the .msi file is located, type the name of the .msi file, and then press ENTER.

##### To install the gateway server

1.  Log on to the gateway server with Administrator rights.

2.  From the Operations Manager installation media, start **Setup.exe**.

3.  In the **Install** area, click the **Gateway management server** link.

4.  On the **Welcome** screen, click **Next**.

5.  On the **Destination Folder** page, accept the default, or click **Change** to select a different installation directory, and then click **Next**.

6.  On the **Management Group Configuration** page, type the target management group name in the **Management Group Name** field, type the target management server name in the **Management Server** field, check that the **Management Server Port** field is **5723**, and then click **Next**. This port can be changed if you have enabled a different port for management server communication in the Operations console.

7.  On the **Gateway Action Account** page, select the **Local System** account option, unless you have specifically created a domain-based or local computer-based gateway Action account. Click **Next**.

8.  On the **Microsoft Update** page, optionally indicate if you want to use Microsoft Update, and then click **Next**.

9. On the **Ready to Install** page, click **Install**.

10. On the **Completing**  page, click **Finish**.

##### To Install the gateway server from the Command Prompt

1.  Log on to the gateway server with Administrator rights.

2.  Open the Command Prompt window by using the **Run as Administrator** option.

3.  Run the following command, where *path\Directory* is the location of the Momgateway.msi, and *path\Logs* is the location where you want to save the log file. Momgateway.msi can be found in the Operations Manager installation media.

    ```
    %WinDir%\System32\msiexec.exe /i path\Directory\MOMGateway.msi /qn /l*v path\Logs\GatewayInstall.log
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

### Importing certificates with the MOMCertImport.exe tool

Perform this operation on each gateway server, management server, and computer that will be agent-managed and that is in a domain that is not trusted.

##### To import computer certificates by using MOMCertImport.exe

1.  Copy the MOMCertImport.exe tool from the installation media \SupportTools\\<platform\> (amd64, x86 or ia64) directory to the root of the target server or to the Operations Manager installation directory if the target server is a management server.

2.  As an administrator, open a Command Prompt window and change the directory to the directory where MOMCertImport.exe is, and then run `momcertimport.exe /SubjectName <certificate subject name>`. This makes the certificate usable by Operations Manager.

### Configuring gateway servers for failover between management servers

Although gateway servers can communicate with any management server in the management group, this must be configured. In this scenario, the secondary management servers are identified as targets for gateway server failover.

Use the Set-SCOMParentManagementServer command in the Operations Manager shell, as shown in the following example, to configure a gateway server to failover to multiple management servers. The commands can be run from any Command Shell in the management group.

##### To configure gateway server failover between management servers

1.  Log on to the management server with an account that is a member of the Administrators role for the management group.

2.  On the Windows desktop, click **Start**, point to **Programs**, point to **System Center Operations Manager**, and then click **Command Shell**.

3.  In Command Shell, run the following commands:

    $GatewayServer = Get-SCOMGatewayManagementServer -Name "ComputerName.Contoso.com"
    $FailoverServer = Get-SCOMManagementServer -Name "ManagementServer.Contoso.com","ManagementServer2.Contoso.com"
    Set-SCOMParentManagementServer -GatewayServer $GatewayServer
    -FailoverServer $FailoverServer


## To chain multiple gateway servers

It is sometimes necessary to chain multiple gateways together in order to monitor across multiple untrusted boundaries. This topic describes how to chain multiple gateways together.

> [!NOTE] 
> You should install one gateway at a time and verify that each newly installed gateway is configured correctly before adding another gateway in the chain.

1. On the management server that was targeted during the gateway server installation, run the Microsoft.EnterpriseManagement.GatewayApprovalTool.exe tool to initiate communication between the management server and the gateway.
2. Open a command prompt, and navigate to the Operations Manager installation directory or, and then run the following: ```Microsoft.EnterpriseManagement.gatewayApprovalTool.exe /ManagementServerName=<managementserverFQDN> /GatewayName=<GatewayFQDN> /Action=Create```
3. Install the gateway server on a new server. 
4. Configure the certificates between gateways in the same way that you would configure certificates between a gateway and a management server. The Health Service can only load and use a single certificate. Therefore, the same certificate is used by the parent and child of the gateway in the chain. 

## Next steps

- See [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md) to understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group.   
