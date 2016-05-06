---
title: Monitoring Nano Server
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3b1e34e3-7a86-42f3-acc6-363fc00b0e62
---
# Monitoring Nano Server
[!INCLUDE[winthreshold_nano](./Token/winthreshold_nano_md.md)] is a new installation option introduced in [!INCLUDE[winthreshold_server_1](./Token/winthreshold_server_1_md.md)]. Nano Server is optimized for private cloud and datacenter operations. With [!INCLUDE[scom_threshold_1](./Token/scom_threshold_1_md.md)] you can now monitor Nano Server by installing the Operations Manager agent.

## Nano Server monitoring capabilities
With the release of Nano Server you can  monitor the basic operations of the Server by using the Windows Server Operating System Management Pack. You can also monitor a Nano Server running the following workloads:
- Windows Failover Cluster  
- Domain Name System (DNS) server
- Internet Information Services (IIS)
  
You can download these management packs for Nano Server from the [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=48256).  

>[!NOTE] 
> The Internet Information Services and DNS Server management packs will be available shortly from the Microsoft Download Center.

Monitoring a Nano Server installation is similar to monitoring any other installation of Windows Server, however, there are some key differences in how you install the agent on a Nano Server.

You will need to follow the steps listed below to start monitoring a Nano Server.

1.  [Install the Operations Manager agent on a Nano server](Install-Agent-on-Windows-Using-the-Discovery-Wizard.xml).

2.  [Validate that the Operations Manager agent has been successfully installed](#BKMK_validateinstall)

3.  [Start Monitoring your  Nano Server](#BKMK_enablemonitor)

4.  [Verify that you are monitoring your Nano Server](#BKMK_verifymonitor).

There are several limitations in this release of the Nano Server agent. The following operations are not supported in this initial release:

-   Installing the Operations Manager Agent via an MSI package.

-   Monitoring a Nano Server that is not in the same domain as the Operations Manager Management Server.

-   Monitoring a Nano Server with a Management Pack written in VBScript or JScript.

-   Monitoring .Net applications running on a Nano Server.

-   Process Monitoring on the Nano Server.

-   ICMP monitoring on the Nano Server.

-   OLE DB monitoring on the Nano Server.

-   Integrating the Nano Server with Active Directory.

-   Updating the Operations Manager agent on a Nano Server  by applying updates.

-   Using network discovery rules to discover devices that support ICMP.

-   Monitoring specific url's on a Nano Server.

-   Collecting data from the Application Log of a Nano Server.


### <a name="BKMK_installagent"></a>Install the Operations Manager agent on a Nano server

1.  Follow the instructions for installing Nano Server on either a physical computer or a virtual machine. See   [Getting Started with Nano Server](https://technet.microsoft.com/library/mt126167.aspx) for complete instructions.

    > [!NOTE]
    > The  Nano Server must be in  the same domain as the Operations Manager Management Server.

2.  Add the Microsoft\-OneCore\-ReverseForwarders package as described in the Getting Started with Nano Server topic.

3.  Join the Nano Server to the same domain as the  Operations Manager Management Server.
There are two methods available for installing the Operations Manager agent on Nano Servers, Discovery Wizard from the Operations console or PowerShell script.  The process of installing the agent using the Discovery Wizard is consistent with the steps described in the following document [Use the Discovery Wizard to Deploy Agents](Install-Agent-on-Windows-Using-the-Discovery-Wizard.xml).

Use the following procedure to install the agent with a PowerShell script.   

1.  Copy the NanoServer directory from the System Center Operations Manager setup directory to the Nano Server.

2.  Open a PowerShell command window on the Nano Server from a computer running in the same domain as the Nano Server.

3.  Set the file path on the Nano Server to NanoAgent\\NanoServer

4.  Run the following script:

    ```
    .\InstallNanoServerScomAgentOnline.ps1 -ManagementServerFQDN <<Management Server Name FQDN>> -ManagementGroupName <<Management Group Name>> -NanoServerFQDN <<Nano server FQDN on which the agent will be installed>> -BinaryFolder ..\
    ```

    > [!NOTE]
    > If the installation is successful you will see "Installation successful" in the Installlog.txt file which the installer will add to the NanoAgent\\NanoServer directory on the Nano Server. You should not see any errors in that file.

8.  Run the following command on the Nano Server:

    ```
    Net Start HealthService
    ```

#### <a name="BKMK_validateinstall"></a>Validate that the Operations Manager agent has been successfully installed

1.  Open the Services console on a computer joined to the same domain as the Nano Server by running the running the services.msc command.

2.  Connect to the Nano Server in the Action panel by specifying the Fully Qualified Domain Name \(FQDN\) of the Nano Server.

3.  Verify that the Status of the Microsoft Monitoring Agent Service is "Running".

#### <a name="BKMK_enablemonitor"></a>Start Monitoring your Nano Server
  
> [!NOTE]
> The following procedure is only required for a PowerShell-based agent installation.
 
1.  Open the **Pending Management** section of the Administration pane in the Operations Manager console.

2.  Approve the Nano Server for management.

#### <a name="BKMK_verifymonitor"></a>Verify that you are monitoring your Nano Server

1.  Open the **Agent Managed** list in the Device Management section of the Operations Manager Console Administration pane.

2.  Verify that the Health State is shown as Healthy.

##### Remove the Operations Manager Agent from your Nano Server

1.  Open a PowerShell window as an administrator on the Nano Server.

2.  Change to the \\NanoAgent\\NanoServer folder.

3.  Run the following script:

    ```
    .\UnInstallNanoServerScomAgentOnline.ps1 -ManagementServerFQDN <<Management Server Name FQDN>> -ManagementGroupName <<Management Group Name>> -NanoServerFQDN <<Nano Server FQDN from which the agent needs to be uninstalled>>
    ```

    > [!NOTE]
    > You can  validate that the Operations Manager agent has been removed by checking that the uninstalllog.txt file in the \\NanoAgent\\NanoServer folder does not contain any errors and that  you see the message "Successfully un\-installed the agent from Nano Server" in the log file.


