---
title: How to Deploy a Gateway Server
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc38412e-d5c6-429a-ac70-b01b7651e4d5
---
# How to Deploy a Gateway Server
To monitor computers that lie outside the trust boundary of a management server without the use of a gateway server, you need to install and manually maintain certificates on the management servers and the computers to be monitored. When this configuration is used instead of using a gateway server, additional ports must be opened for agent\-to\-management server communication. For a listing of all ports that are necessary, see [System Requirements for System Center 2012 – Operations Manager](http://go.microsoft.com/fwlink/p/?LinkID=219650).

### Procedure overview

1.  Request certificates for any computer in the agent, gateway server, management server chain.

2.  Import those certificates into the target computers by using the MOMCertImport.exe tool.

3.  Distribute the Microsoft.EnterpriseManagement.GatewayApprovalTool.exe to the management server.

4.  Run the Microsoft.EnterpriseManagement.GatewayApprovalTool.exe tool to initiate communication between the management server and the gateway

5.  Install the gateway server.

## Preparing for Installation

#### Before You Start

1.  Deployment of gateway servers requires certificates. You need to have access to a certification authority \(CA\). This can be a public CA such as VeriSign, or you can use Microsoft Certificate Services. This procedure provides the steps to request, obtain, and import a certificate from Microsoft Certificate Services.

2.  Reliable name resolution must exist between the agent\-managed computers and the gateway server and between the gateway server and the management servers. This name resolution is typically done through DNS. However, if it is not possible to get proper name resolution through DNS, it might be necessary to manually create entries in each computer's hosts file.

    > [!NOTE]
    > The hosts file is located in the \\Windows\\system32\\drivers\\ directory, and it contains directions for configuration.

### Obtaining Computer Certificates from Microsoft Certificate Services
For more information, see [Authentication and Data Encryption for Windows Computers](assetId:///8ee895a9-7bac-4274-80b8-092475a83c67).

### Distributing the Microsoft.EnterpriseManagement.GatewayApprovalTool
The Microsoft.EnterpriseManagement.GatewayApprovalTool.exe tool is needed only on the management server, and it only has to be run once.

##### To copy Microsoft.EnterpriseManagement.GatewayApprovalTool.exe to management servers

1.  From a target management server, open the [!INCLUDE[om12short](./Token/om12short_md.md)] installation media \\SupportTools directory.

2.  Copy the Microsoft.EnterpriseManagement.GatewayApprovalTool.exe from the installation media to the [!INCLUDE[om12short](./Token/om12short_md.md)] installation directory.

### Registering the Gateway with the Management Group
This procedure registers the gateway server with the management group, and when this is completed, the gateway server appears in the Discovered Inventory view of the management group.

##### To run the gateway Approval tool

1.  On the management server that was targeted during the gateway server installation, log on with the [!INCLUDE[om12short](./Token/om12short_md.md)] Administrator account.

2.  Open a command prompt, and navigate to the [!INCLUDE[om12short](./Token/om12short_md.md)] installation directory or to the directory that you copied the Microsoft.EnterpriseManagement.gatewayApprovalTool.exe to.

3.  At the command prompt, run `Microsoft.EnterpriseManagement.gatewayApprovalTool.exe /ManagementServerName=<managementserverFQDN> /GatewayName=<GatewayFQDN> /Action=Create`

4.  If the approval is successful, you will see `The approval of server <GatewayFQDN> completed successfully.`

5.  If you need to remove the gateway server from the management group, run the same command, but substitute the `/Action=Delete` flag for the `/Action=Create` flag.

6.  Open the Operations console to the Monitoring view. Select the Discovered Inventory view to see that the gateway server is present.

### <a name="BKMK_InstallGateway"></a>Installing Gateway Server
This procedure installs the gateway server. The server that is to be the gateway server should be a member of the same domain as the agent\-managed computers that will be reporting to it.

> [!TIP]
> An installation will fail when starting Windows Installer \(for example, installing a gateway server by double\-clicking MOMGateway.msi\) if the local security policy User Account Control: Run all administrators in Admin Approval Mode is enabled.

##### To run Operations Manager Gateway Windows Installer from a Command Prompt window

1.  On the Windows desktop, click **Start**, point to **Programs**, point to **Accessories**, right\-click **Command Prompt**, and then click **Run as administrator**.

2.  In the **Administrator: Command Prompt** window, navigate to the local drive that hosts the [!INCLUDE[om12short](./Token/om12short_md.md)] installation media.

3.  Navigate to the directory where the .msi file is located, type the name of the .msi file, and then press ENTER.

##### To install the gateway server

1.  Log on to the gateway server with Administrator rights.

2.  From the [!INCLUDE[om12short](./Token/om12short_md.md)] installation media, start **Setup.exe**.

3.  In the **Install** area, click the **Gateway management server** link.

4.  On the **Welcome** screen, click **Next**.

5.  On the **Destination Folder** page, accept the default, or click **Change** to select a different installation directory, and then click **Next**.

6.  On the **Management Group Configuration** page, type the target management group name in the **Management Group Name** field, type the target management server name in the **Management Server** field, check that the **Management Server Port** field is **5723**, and then click **Next**. This port can be changed if you have enabled a different port for management server communication in the Operations console.

7.  On the **Gateway Action Account** page, select the **Local System** account option, unless you have specifically created a domain\-based or local computer\-based gateway Action account. Click **Next**.

8.  On the **Microsoft Update** page, optionally indicate if you want to use Microsoft Update, and then click **Next**.

9. On the **Ready to Install** page, click **Install**.

10. On the **Completing**  page, click **Finish**.

##### To Install the gateway server by using the Command Prompt window

1.  Log on to the gateway server with Administrator rights.

2.  Open the Command Prompt window by using the **Run as Administrator** option.

3.  Run the following command, where *path\\Directory* is the location of the Momgateway.msi, and *path\\Logs* is the location where you want to save the log file. Momgateway.msi can be found in the [!INCLUDE[om12short](./Token/om12short_md.md)] installation media.

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

### <a name="BKMK_ImportCert"></a>Importing Certificates with the MOMCertImport.exe Tool
Perform this operation on each gateway server, management server, and computer that will be agent\-managed and that is in a domain that is not trusted.

##### To import computer certificates by using MOMCertImport.exe

1.  Copy the MOMCertImport.exe tool from the installation media \\SupportTools\\<platform> \(x86 or ia64\) directory to the root of the target server or to the [!INCLUDE[om12short](./Token/om12short_md.md)] installation directory if the target server is a management server.

2.  As an administrator, open a Command Prompt window and change the directory to the directory where MOMCertImport.exe is, and then run `momcertimport.exe /SubjectName <certificate subject name>`. This makes the certificate usable by [!INCLUDE[om12short](./Token/om12short_md.md)].

### Configuring Gateway Servers for Failover Between Management Servers
Although gateway servers can communicate with any management server in the management group, this must be configured. In this scenario, the secondary management servers are identified as targets for gateway server failover.

Use the Set\-ManagementServer\-gatewayManagementServer command in [!INCLUDE[om12shell](./Token/om12shell_md.md)], as shown in the following example, to configure a gateway server to failover to multiple management servers. The commands can be run from any Command Shell in the management group.

##### To configure gateway server failover between management servers

1.  Log on to the management server with an account that is a member of the Administrators role for the management group.

2.  On the Windows desktop, click **Start**, point to **Programs**, point to **System Center Operations Manager**, and then click **Command Shell**.

3.  In Command Shell, follow the example that is described in the next section.

### Description
The following example can be used to configure gateway server failover to multiple management servers.

### Code

```
$GatewayServer = Get-SCOMGatewayManagementServer –Name “ComputerName.Contoso.com”
$FailoverServer = Get-SCOMManagementServer –Name “ManagementServer.Contoso.com”,”ManagementServer2.Contoso.com”
Set-SCOMParentManagementServer -GatewayServer $GatewayServer -FailoverServer $FailoverServer

```

## See Also
[Deploying a Gateway Server](assetId:///b890d6e8-1363-423d-bf2b-7c7cf6d6ce5b)


