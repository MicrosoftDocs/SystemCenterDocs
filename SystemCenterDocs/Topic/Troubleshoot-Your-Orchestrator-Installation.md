---
title: Troubleshoot Your Orchestrator Installation
ms.custom: na
ms.prod: system-center-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17b3dbfc-f129-4da2-9d39-bce126c00aff
---
# Troubleshoot Your Orchestrator Installation
The latest troubleshooting information for [!INCLUDE[orchlong](../Token/orchlong_md.md)] is available in the release notes under the [Release Notes for System Center 2012 - Orchestrator_1](../Topic/Release-Notes-for-System-Center-2012---Orchestrator_1.md) topic in the [Orchestrator](http://go.microsoft.com/fwlink/?LinkId=264231) library on TechNet. The following information provides additional instructions and caveats that you can use during installation to resolve problems you might experience.

## [!INCLUDE[orchshort](../Token/orchshort_md.md)] log files
If you experience problems during installation, installation log files are located in the folder **C:\\Users\\%USERNAME%\\AppData\\Local\\SCO\\LOGS**.

If you experience problems when you are running [!INCLUDE[orchshort](../Token/orchshort_md.md)], the product log files are located in the folder **C:\\ProgramData\\Microsoft System Center 2012\\Orchestrator\\**.

## Windows Firewall
When you deploy additional Runbook Designer applications to your environment, you might see a failed installation message. To correctly install the Runbook Designer, enable the following firewall rules as they apply to your operating system and deployment configuration.

### Windows Firewall with Advanced Security for Windows Server 2012 R2
By default, **Windows Firewall with Advanced Security** is enabled on all Windows Server 2012 R2 computers, and blocks all incoming traffic unless it is a response to a request by the host, or it is specifically allowed. You can explicitly allow traffic by specifying a port number, application name, service name, or other criteria by configuring Windows Firewall with Advanced Security settings.

If you are running Windows Server 2012 R2, enable the following rules to allow all Monitor Event activities to function correctly:

-   Windows Management Instrumentation \(Async\-In\)

-   Windows Management Instrumentation \(DCOM\-In\)

-   Windows Management Instrumentation \(WMI\-In\)

#### Automated deployment
When a runbook server or Runbook Designer is installed behind a firewall, specific firewall rules are required between the remote computers that are used to deploy the runbook server and Runbook Designer. An additional rule is required for the remote connection between the Runbook Designer and the runbook server to allow the [!INCLUDE[orchshort](../Token/orchshort_md.md)] management service to accept remote connections. If you are using the **Monitor WMI** task, the runbook server requires a special firewall rule on the computer that uses PolicyModule.exe.

Enable the following firewall rules on your computer:

### Firewall rule between the Runbook Designer and the [!INCLUDE[orchshort](../Token/orchshort_md.md)] management server

|Operating system|Firewall rule|
|--------------------|-----------------|
|64\-bit|%ProgramFiles \(x86\)%\\Microsoft System Center 2012 R2\\Orchestrator\\Management Server\\OrchestratorManagementService.exe|
|32\-bit|%ProgramFiles%Microsoft System Center 2012 R2\\Orchestrator\\Management Server\\OrchestratorManagementService.exe|

### Firewall rules between remote computers

|Operating system|Firewall rules|
|--------------------|------------------|
|Windows Server 2012 R2|<ul><li>File and Printer Sharing</li><li>Windows Management Instrumentation \(WMI\)</li><li>Program rule for OrchestratorRemotingService to accept remote connections. This rule must be enabled through the Advanced Firewall mode:<br /><br /><ul><li>%SystemRoot%\\SysWOW64\\OrchestratorRemotingService.exe \(for a 64\-bit operating system\)</li><li>%SystemRoot%\\System32\\OrchestratorRemotingService.exe \(for a 32\-bit operating system\)</li></ul></li></ul>|

### Firewall rules between the runbook server and the computer that uses PolicyModule.exe

|Operating system|Firewall rule|
|--------------------|-----------------|
|64\-bit|%ProgramFiles \(x86\)%\\Microsoft System Center 2012 R2\\Orchestrator\\Runbook Server\\PolicyModule.exe|
|32\-bit|%ProgramFiles\\Microsoft System Center 2012 R2\\Orchestrator\\Runbook Server\\PolicyModule.exe|

[!INCLUDE[crabout](../Token/crabout_md.md)] adding firewall rules, see [Add or Edit a Firewall Rule](http://go.microsoft.com/fwlink/p/?LinkID=201019).

## <a name="BKMK_RunbookServicefailstostart"></a>RunbookService fails to start after computer reboot
When you reboot your runbook server, the RunbookService attempts to connect to the orchestration database. If the database is not available, the RunbookService fails. The event log message is **This computer was unable to communicate with the computer providing the server.**. Typically, this can occur when the SQL server and the runbook server are installed on the same computer.

To solve this problem. you can manually start the RunbookService, or configure the RunbookService to make multiple attempts during startup to connect to database before failing.

## Cannot restart runbook service if you uninstall with an account without administrator permissions
If you attempt to uninstall [!INCLUDE[orchshort](../Token/orchshort_md.md)] while logged in with an account that is a member of OrchestratorSystemGroup but is not an administrator, uninstall removes all accounts from OrchestratorSystemGroup. If you stop the runbook service and attempt to restart the service, the service fails because the user account does not have the correct permissions to retrieve the orchestration database connection. An account that is an administrator or a member of the OrchestratorSystemGroup is required to retrieve the orchestration database connection.

To solve this problem, an administrator can add the user back to OrchestratorSystemGroup.

## Other resources for this product

-   TechNet Library main page for [Orchestrator](http://go.microsoft.com/fwlink/?LinkId=264231)

-   [Deploying System Center 2012 - Orchestrator](../Topic/Deploying-System-Center-2012---Orchestrator.md) in the [Orchestrator](http://go.microsoft.com/fwlink/?LinkId=264231) library on TechNet.

