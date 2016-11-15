---
title: Troubleshoot Your Orchestrator Installation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17b3dbfc-f129-4da2-9d39-bce126c00aff
author: cfreemanwa
ms.author: cfreeman
manager: cfreeman
ms.date: 10/12/2016

---
# Troubleshoot Your Orchestrator Installation

>Applies To: System Center 2016 - Orchestrator

The following information provides additional instructions and caveats that you can use during installation to resolve problems you might experience.  

## Orchestrator log files  
If you experience problems during installation, installation log files are located in the folder **C:\\Users\\%USERNAME%\\AppData\\Local\\SCO\\LOGS**.  

If you experience problems when you are running Orchestrator, the product log files are located in the folder **C:\\ProgramData\\Microsoft System Center 2016\\Orchestrator\\**.  

## Windows Firewall  
When you deploy additional Runbook Designer applications to your environment, you might see a failed installation message. To correctly install the Runbook Designer, enable the following firewall rules as they apply to your operating system and deployment configuration.  

### Windows Firewall with Advanced Security for Windows Server 2016  
By default, **Windows Firewall with Advanced Security** is enabled on all Windows Server 2016 computers, and blocks all incoming traffic unless it is a response to a request by the host, or it is specifically allowed. You can explicitly allow traffic by specifying a port number, application name, service name, or other criteria by configuring Windows Firewall with Advanced Security settings.  

If you are running Windows Server 2016, enable the following rules to allow all Monitor Event activities to function correctly:  

-   Windows Management Instrumentation \(Async\-In\)  

-   Windows Management Instrumentation \(DCOM\-In\)  

-   Windows Management Instrumentation \(WMI\-In\)  

#### Automated deployment  
When a runbook server or Runbook Designer is installed behind a firewall, specific firewall rules are required between the remote computers that are used to deploy the runbook server and Runbook Designer. An additional rule is required for the remote connection between the Runbook Designer and the runbook server to allow the Orchestrator management service to accept remote connections. If you are using the **Monitor WMI** task, the runbook server requires a special firewall rule on the computer that uses PolicyModule.exe.  

Enable the following firewall rules on your computer:  

### Firewall rule between the Runbook Designer and the Orchestrator management server  

|Operating system|Firewall rule|  
|--------------------|-----------------|  
|64\-bit|%ProgramFiles \(x86\)%\\Microsoft System Center 2016\\Orchestrator\\Management Server\\OrchestratorManagementService.exe|  
|32\-bit|%ProgramFiles%Microsoft System Center 2016\\Orchestrator\\Management Server\\OrchestratorManagementService.exe|  

### Firewall rules between remote computers  

|Operating system|Firewall rules|  
|--------------------|------------------|  
|Windows Server 2016|<ul><li>File and Printer Sharing</li><li>Windows Management Instrumentation \(WMI\)</li><li>Program rule for OrchestratorRemotingService to accept remote connections. This rule must be enabled through the Advanced Firewall mode:<br /><br /><ul><li>%SystemRoot%\\SysWOW64\\OrchestratorRemotingService.exe \(for a 64\-bit operating system\)</li><li>%SystemRoot%\\System32\\OrchestratorRemotingService.exe \(for a 32\-bit operating system\)</li></ul></li></ul>|  

### Firewall rules between the runbook server and the computer that uses PolicyModule.exe  

|Operating system|Firewall rule|  
|--------------------|-----------------|  
|64\-bit|%ProgramFiles \(x86\)%\\Microsoft System Center 2016\\Orchestrator\\Runbook Server\\PolicyModule.exe|  
|32\-bit|%ProgramFiles\\Microsoft System Center 2016\\Orchestrator\\Runbook Server\\PolicyModule.exe|  

For more information about adding firewall rules, see [Add or Edit a Firewall Rule](http://go.microsoft.com/fwlink/p/?LinkID=201019).  

## <a name="BKMK_RunbookServicefailstostart"></a>RunbookService fails to start after computer reboot  
When you reboot your runbook server, the RunbookService attempts to connect to the orchestration database. If the database is not available, the RunbookService fails. The event log message is **This computer was unable to communicate with the computer providing the server.**. Typically, this can occur when the SQL server and the runbook server are installed on the same computer.  

To solve this problem. you can manually start the RunbookService, or configure the RunbookService to make multiple attempts during startup to connect to database before failing.  

## Cannot restart runbook service if you uninstall with an account without administrator permissions  
If you attempt to uninstall Orchestrator while logged in with an account that is a member of OrchestratorSystemGroup but is not an administrator, uninstall removes all accounts from OrchestratorSystemGroup. If you stop the runbook service and attempt to restart the service, the service fails because the user account does not have the correct permissions to retrieve the orchestration database connection. An account that is an administrator or a member of the OrchestratorSystemGroup is required to retrieve the orchestration database connection.  

To solve this problem, an administrator can add the user back to OrchestratorSystemGroup.  

## Other resources for this product  

-   TechNet Library main page for [Orchestrator](http://go.microsoft.com/fwlink/?LinkId=264231)  
