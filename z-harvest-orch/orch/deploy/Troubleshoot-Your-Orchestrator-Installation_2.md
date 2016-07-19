---
title: Troubleshoot Your Orchestrator Installation_2
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f1b561c-6298-4ee9-a64c-061eda1b01be
author:bwren
manager:cfreemanwa
---
# Troubleshoot Your Orchestrator Installation_2
The latest troubleshooting information for [!INCLUDE[orchlong](../../orch/deploy/includes/orchlong_md.md)] is available in the release notes at [Release Notes for System Center 2012 - Orchestrator_1](../Topic/Release%20Notes%20for%20System%20Center%202012%20-%20Orchestrator_1.md). The following information provides additional instructions and caveats that you can use during installation to resolve problems you might experience.  
  
## [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] log files  
If you experience problems during installation, installation log files are located in the folder **C:\\Users\\%USERNAME%\\AppData\\Local\\SCO\\LOGS**.  
  
If you experience problems when you are running [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)], the product log files are located in the folder **C:\\ProgramData\\Microsoft System Center 2012\\Orchestrator\\**.  
  
## Windows Firewall  
When you deploy additional Runbook Designer applications to your environment, you might see a failed installation message. To correctly install the Runbook Designer, enable the following firewall rules as they apply to your operating system and deployment configuration.  
  
### Windows Firewall with Advanced Security for Windows Server 2012 R2  
By default, **Windows Firewall with Advanced Security** is enabled on all Windows Server 2008 R2 computers, and blocks all incoming traffic unless it is a response to a request by the host, or it is specifically allowed. You can explicitly allow traffic by specifying a port number, application name, service name, or other criteria by configuring Windows Firewall with Advanced Security settings.  
  
If you are running Windows Server 2012 R2, enable the following rules to allow all Monitor Event activities to function correctly:  
  
-   Windows Management Instrumentation \(Async\-In\)  
  
-   Windows Management Instrumentation \(DCOM\-In\)  
  
-   Windows Management Instrumentation \(WMI\-In\)  
  
#### Automated deployment  
When a runbook server or Runbook Designer is installed behind a firewall, specific firewall rules are required between the remote computers that are used to deploy the runbook server and Runbook Designer. An additional rule is required for the remote connection between the Runbook Designer and the runbook server to allow the [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] management service to accept remote connections. If you are using the **Monitor WMI** task, the runbook server requires a special firewall rule on the computer that uses PolicyModule.exe.  
  
Enable the following firewall rules on your computer:  
  
### Firewall rule between the Runbook Designer and the [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] management server  
  
|Operating system|Firewall rule|  
|--------------------|-----------------|  
|64\-bit|%ProgramFiles \(x86\)%\\Microsoft System Center 2012 R2\\Orchestrator\\Management Server\\OrchestratorManagementService.exe|  
|32\-bit|%ProgramFiles%Microsoft System Center 2012 R2\\Orchestrator\\Management Server\\OrchestratorManagementService.exe|  
  
### Firewall rules between remote computers  
  
|Operating system|Firewall rules|  
|--------------------|------------------|  
|Windows Server 2008 R2|<ul><li>File and Printer Sharing</li><li>Windows Management Instrumentation \(WMI\)</li><li>Program rule for OrchestratorRemotingService to accept remote connections. This rule must be enabled through the Advanced Firewall mode:<br /><br /><ul><li>%SystemRoot%\\SysWOW64\\OrchestratorRemotingService.exe \(for a 64\-bit operating system\)</li><li>%SystemRoot%\\System32\\OrchestratorRemotingService.exe \(for a 32\-bit operating system\)</li></ul></li></ul>|  
  
### Firewall rules between the runbook server and the computer that uses PolicyModule.exe  
  
|Operating system|Firewall rule|  
|--------------------|-----------------|  
|64\-bit|%ProgramFiles \(x86\)%\\Microsoft System Center 2012 R2\\Orchestrator\\Runbook Server\\PolicyModule.exe|  
|32\-bit|%ProgramFiles\\Microsoft System Center 2012 R2\\Orchestrator\\Runbook Server\\PolicyModule.exe|  
  
[!INCLUDE[crabout](../../orch/deploy/includes/crabout_md.md)] adding firewall rules, see [Add or Edit a Firewall Rule](http://go.microsoft.com/fwlink/p/?LinkID=201019).  
  
## <a name="BKMK_RunbookServicefailstostart"></a>RunbookService fails to start after computer reboot  
When you reboot your runbook server, the RunbookService attempts to connect to the orchestration database. If the database is not available, the RunbookService fails. The event log message is **This computer was unable to communicate with the computer providing the server.**. Typically, this can occur when the SQL server and the runbook server are installed on the same computer.  
  
To solve this problem. you can manually start the RunbookService, or configure the RunbookService to make multiple attempts during startup to connect to database before failing.  
  
## Cannot restart runbook service if you uninstall with an account without administrator permissions  
If you attempt to uninstall [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] while logged in with an account that is a member of OrchestratorSystemGroup but is not an administrator, uninstall removes all accounts from OrchestratorSystemGroup. If you stop the runbook service and attempt to restart the service, the services fails because the user account does not have the correct permissions to retrieve the orchestration database connection. An account that is an administrator or a member of the OrchestratorSystemGroup is required to retrieve the orchestration database connection.  
  
To solve this problem, an administrator can add the user back to OrchestratorSystemGroup.  
  
## HTTP errors when starting the Orchestration console  
If you get HTTP errors when starting the Orchestration console, try the following mitigations:  
  
-   **HTTP error 404.3 – Not Found**: Ensure that both .NET Framework 4.5 and Windows Communication Foundation \(WCF\) HTTP Activation are installed. You can find the instructions in [Single\-Computer Requirements for System Center 2012 R2 Orchestrator](assetId:///8960870a-e5e4-4674-baa1-94a55fee089c).  
  
-   **HTTP error 404.17 – Not Found**: Ensure that Windows Communication Foundation \(WCF\) HTTP Activation is installed. You can find the instructions in [Single\-Computer Requirements for System Center 2012 R2 Orchestrator](assetId:///8960870a-e5e4-4674-baa1-94a55fee089c).  
  
## Other resources for this product  
  
-   TechNet Library main page for [Orchestrator_1](../Topic/Orchestrator_1.md)  
  
-   [Deploying System Center 2012 - Orchestrator](../../orch/deploy/Deploying-System-Center-2012---Orchestrator.md)  
  
-   [Deployment Overview](../../orch/deploy/Deployment-Overview.md)  
  
-   [Plan Your Orchestrator Deployment](../../orch/deploy/Plan-Your-Orchestrator-Deployment.md)  
  
-   [Install Orchestrator](../../orch/deploy/Install-Orchestrator.md)  
  
-   [Perform Post-Installation Tasks](../../orch/deploy/Perform-Post-Installation-Tasks.md)  
  
