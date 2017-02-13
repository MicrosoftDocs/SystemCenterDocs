---
ms.assetid: f257a38b-38b3-4688-8c56-19317fc68d8e
title: Install Agent on Nano Server
description: This article describes how to install the Operations Manager agent on Nano Server. 
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 02/14/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Install agent on Nano Server

>Applies To: System Center 2016 - Operations Manager

Windows Server 2016 Nano Server is a new installation option introduced in Windows Server 2016. Nano Server is optimized for private cloud and datacenter operations. With System Center 2016  - Operations Manager you can now monitor Nano Server by installing the Operations Manager agent.

## Nano Server monitoring capabilities

With the release of Nano Server you can  monitor the basic operations of the Server by using the Windows Server Operating System Management Pack.  You can also monitor a Nano Server running the following workloads:

- Windows Failover Cluster  
- Domain Name System (DNS) server
- Internet Information Services (IIS)
  
You can download these management packs for Nano Server from the [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=48256).  

Monitoring a Nano Server installation is similar to monitoring any other installation of Windows Server, however, there are some key differences in how you install the agent on a Nano Server.

You will need to follow the steps listed below to start monitoring a Nano Server.

1.  [Deploy the Operations Manager agent from the Operations console using the Discovery Wizard](Install-Agent-on-Windows-Using-the-Discovery-Wizard.md) or [Manually install the Operations Manager agent on a Nano server](#manually-install-the-operations-manager-agent-on-a-nano-server).

3.  [Validate that the Operations Manager agent has been successfully installed](#validate-that-the-operations-manager-agent-has-been-successfully-installed)

4.  [Process Manual Agent Installations](Process-Manual-Agent-Installations.md) if you installed the agent manually on Nano Server.

5.  [Verify that you are monitoring your Nano Server](#verify-that-you-are-monitoring-your-nano-server).

There are several limitations in this release of the Nano Server agent. The following operations are not supported in this release:

-   Installing the Operations Manager Agent via an MSI package.

-   Monitoring a Nano Server that is not in the same domain as the Operations Manager Management Server.

-   Monitoring a Nano Server with a Management Pack written in VBScript or JScript.

-   Monitoring .Net applications running on a Nano Server.

-   Process Monitoring on the Nano Server.

-   ICMP monitoring on the Nano Server.

-   OLE DB monitoring on the Nano Server.

-   Integrating the Nano Server with Active Directory.

-   Updating the Operations Manager agent on a Nano Server by applying updates.

-   Using network discovery rules to discover devices that support ICMP.

-   Monitoring specific URL's on a Nano Server.

-   Collecting data from the Application Log of a Nano Server.

-   Putting a Nano Server into maintenance mode.


## Manually install the Operations Manager agent on a Nano server

1.  Follow the instructions for manually installing Nano Server on either a physical computer or a virtual machine. See [Getting Started with Nano Server](https://technet.microsoft.com/library/mt126167.aspx) for complete instructions.

    > [!NOTE]
    > The Nano Server must be in the same domain as the Operations Manager Management Server.

2.  Add the Microsoft-OneCore-ReverseForwarders package as described in the Getting Started with Nano Server topic.

3.  Join the Nano Server to the same domain as the  Operations Manager Management Server.
There are two methods available for installing the Operations Manager agent on Nano Servers, Discovery Wizard from the Operations console or PowerShell script.  The process of installing the agent using the Discovery Wizard is consistent with the steps described in the following document [Discover and install agent on Windows](Install-Agent-on-Windows-Using-the-Discovery-Wizard.md).

Use the following procedure to install the agent with a PowerShell script.   

1.  Copy the NanoServer directory from the System Center Operations Manager setup directory to the Nano Server.

2.  Open a PowerShell command window on the Nano Server from a computer running in the same domain as the Nano Server.

3.  Set the file path on the Nano Server to NanoAgent\NanoServer

4.  Run the following script:

    ```
    .\InstallNanoServerScomAgentOnline.ps1 -ManagementServerFQDN <<Management Server Name FQDN>> -ManagementGroupName <<Management Group Name>> -NanoServerFQDN <<Nano server FQDN on which the agent will be installed>> -BinaryFolder ..\
    ```

    > [!NOTE]
    > If the installation is successful you will see "Installation successful" in the Installlog.txt file which the installer will add to the NanoAgent\NanoServer directory on the Nano Server. You should not see any errors in that file.

8.  Run the following command on the Nano Server:

    ```
    Net Start HealthService
    ```
### Troubleshooting agent installation

If you encounter any difficulties with setting up the Operations Manager Agent on a Nano Server you can follow the checklist below for possible solutions.

|Error Message|Possible Reason|Resolution|
|-------------|-------------|-------------|
|There was an error opening the firewall port|Insufficient permissions for setting the Remote Event Log Management firewall rule.|Make sure the account the script is running under has sufficient permissions to set the firewall rule.|
|Agent directory already present in Nano Server. Please uninstall the agent using the uninstallation script and then try again.|If you ran the installation script already and it did not complete, the Agent directory might have been created already.|Run the uninstallation script as suggested by the error message.|
|Setting up and importing the registry failed.|Insufficient permissions to edit the registry.|Make sure the account the script is running under has sufficient permissions to edit the registry and run the installation script again.|
|Failed to install performance counters.|Insufficient permissions to edit the registry.|Make sure the account the script is running under has sufficient permissions to edit the registry and run the installation script again.|

### Validate that the Operations Manager agent has been successfully installed

1.  Open the Services console on a computer joined to the same domain as the Nano Server by running the running the services.msc command.

2.  Connect to the Nano Server in the Action panel by specifying the Fully Qualified Domain Name (FQDN) of the Nano Server.

3.  Verify that the Status of the Microsoft Monitoring Agent Service is "Running".

## Start Monitoring your Nano Server
  
> [!NOTE]
> The following procedure is only required for a PowerShell-based agent installation.
 
1.  Open the **Pending Management** section of the Administration pane in the Operations Manager console.

2.  Approve the Nano Server for management.

### Verify that you are monitoring your Nano Server

1.  Open the **Agent Managed** list in the Device Management section of the Operations Manager Console Administration pane.

2.  Verify that the Health State is shown as Healthy.

## Remove the Operations Manager Agent from your Nano Server

1.  Open a PowerShell window as an administrator on the Nano Server.

2.  Change to the \NanoAgent\NanoServer folder.

3.  Run the following script:

    ```
    .\UnInstallNanoServerScomAgentOnline.ps1 -ManagementServerFQDN <<Management Server Name FQDN>> -ManagementGroupName <<Management Group Name>> -NanoServerFQDN <<Nano Server FQDN from which the agent needs to be uninstalled>>
    ```

    > [!NOTE]
    > You can  validate that the Operations Manager agent has been removed by checking that the uninstalllog.txt file in the \NanoAgent\NanoServer folder does not contain any errors and that  you see the message "Successfully un-installed the agent from Nano Server" in the log file.

## Troubleshooting agent uninstall

If you encounter any difficulties with removing the Operations Manager Agent on a Nano Server you can follow the checklist below for possible solutions.

|Error Message|Possible Reason|Resolution|
|-------------|-------------|-------------|
|HealthService was not found on the Nano Server. Assuming previous uninstall didn't complete.|If the installation did not complete the HealthService might not have been setup. Another process could also be using the HealthService.|Make sure the HealthService is not being used and run the uninstall script again.|
|Unable to delete HealthService on Nano Server.|The HealthService may be busy or another process is using the HealthService.|Make sure the HealthService is not in use and run the uninstall script again.|
|Unable to kill the MonitoringHost(s) on the Nano Server.|The Operations Manager agent runs in the MonitoringHost process. If that process is active the Uninstallation script will not be able to terminate it.|Make sure the MonitoringHost process is not running, and run the uninstall script again.|
|Unable to uninstall the performance counters.|Insufficient permissions to edit the registry.|Make sure the account the script is running under has sufficient permissions to edit the registry and run the uninstall script again.|
|Unable to remove registry changes done by the Operations Manager agent on Nano Server.|Insufficient permissions to edit the registry.|Make sure the account the script is running under has sufficient permissions to edit the registry and run the Uninstallation script again.|
|Unable to delete the agent directory.|Insufficient permissions to access the NanoAgent directory.|Make sure the account the script is running under has sufficient permissions to access the NanoAgent directory and run the uninstall script again.|
|Unable to locate agent folder on the Nano Server.|Either the NanoAgent directory has been moved, or the account has insufficient permissions to access the NanoAgent directory.|Make sure the account the script is running under has sufficient permissions to access the NanoAgent directory and that the NanoAgent directory is present and run the uninstall script again.|
|Unable to remove the agent directory. Try restarting the Nano Server and then re-running this script.|A process may be using the Operations Manager agent.|Make sure there are no processes attached to the Operations Manager agent and run the uninstall script again.|

## Installing updates to the Nano agent

The Nano agent can be updated by one of the following methods:

1. Push updates from a management server.  

    Updates are offered and installed automatically from Microsoft Update to an Operations Manager management server. With Operations Manager 2016, the management server updates will also carry the updated files for Nano agent.  
    
    After the management server is upgraded, the Nano agents will be placed in a pending management state, as described in the [process manual agent installations](process-manual-agent-installations.md) topic. After approving updates, the agents will receive and apply the update.  Alternatively, you can trigger repair from the Operations console on any Nano agent. This will cause the update to be pushed and installed on the Nano agent from the management server. 

2. Manually install update 
 
    Updates to the Nano agent are available for download by following the instructions in the KB articles and updating manually. You can install these downloaded updates on a Nano agent machine using the following Powershell script. 

    ```powershell
      .\UpdateNanoServerScomAgentOnline.ps1 -NanoServerFQDN <FQDN of the Nano server> -BinaryFolder <<Path where the update .cab is already expanded OR path to one or more Nano-agent update .cab files> -IsCabExpanded <$true if BinaryFolder path is to an expanded .cab, $false if it is for a packed .cab file(s)> -RemoveBackup <$true to remove the previous binaries from the agent machine>
    ```
### Uninstalling updates from the Nano Agent

Directly uninstalling the most recent update from the Nano agent is not supported. Instead, you should uninstall the agent completely and reinstall the agent with the desired set of updates.

## Next steps

- After manually installing the Operations Manager agent on Windows and Nano Server, you need to [Process Manual Agent Installations](Process-Manual-Agent-Installations.md)

