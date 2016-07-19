---
title: Logging and Debugging
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c098d83e-af45-4ee7-b71f-76356153583d
author:mgoedtel
manager:cfreemanwa
---
# Logging and Debugging
This topic describes how to enable logging and debug tools for troubleshooting issues with monitoring UNIX and Linux computers.  
  
## Enable Operations Manager Module Logging  
The Operations Manager Agents for UNIX and Linux maintain several log files which can be useful when troubleshooting client issues. These log files are located on the managed UNIX or Linux computer The logging level for the agent log files can be configured as needed. More verbose logging can be useful in diagnosing an issue. For normal operation, log levels should not be set to a value more verbose than the default configurations \(Intermediate\) in order to prevent excessive log file growth  
  
> [!NOTE]  
> Calls made outside of Windows Remote Management \(WinRM\) are made using SSH\/SFTP. These components rely on a separate logging mechanism than Operations Manager.  
  
> [!NOTE]  
> The logging level for the omiserver.log log file cannot be changed from the default in this version of the Operations Manager Agents for UNIX and Linux.  
  
#### To enable UNIX native module logs  
  
-   Create a blank file named **EnableOpsmgrModuleLogging** in the \\Temp directory for the user account calling these modules by typing at a command\-line prompt **COPY \/Y NUL %windir%\\TEMP\\EnableOpsMgrModuleLogging**.  
  
    > [!NOTE]  
    > Generally, it is the SYSTEM account making the calls, and C:\\Windows\\Temp is the default SYSTEM temp folder.  
  
After creation of the blank file, Operations Manager will immediately begin logging SSH and Certificate activity to the \\Temp directory.Scripts that call into SSH modules will log to <*Scriptname.vbs*>.log. Other modules have their own logs.  
  
In some cases, it may be required to restart the HealthService to get the EnableOpsmgrModuleLogging logging to take effect.  
  
## Enable Logging on the UNIX Agent  
These logs will report the UNIX agent actions. If there is a problem with the data returned to Operations Manager, look in this log. You can set the amount of information logged with the scxadmin command. The syntax for this command is:  
  
`scxadmin -log-set [all|cimom|provider] {verbose|intermediate|errors}`  
  
The following table lists the possible parameter values:  
  
|Level|Description|  
|---------|---------------|  
|Errors|Log only **Warning** or **Error** messages.|  
|Intermediate|Log **Info**, **Warning** and **Error** messages.|  
|Verbose|Log **Info**, **Warning**, and **Error** messages with debug logging. Note that This level of logging is likely to cause rapid growth in the size of the log files.  It is strongly recommended that this option only be used for short periods of time to diagnose a specific issue.|  
  
## Use DebugView to Troubleshoot Discovery Issues  
DebugView is an alternative method to EnableOpsmgrModuleLogging for troubleshooting discovery issues.  
  
#### To use DebugView  
  
1.  Download DebugView from: [http:\/\/go.microsoft.com\/fwlink\/?Linkid\=129486](http://go.microsoft.com/fwlink/?Linkid=129486).  
  
2.  Launch DebugView on the Management Server performing the discovery.  
  
3.  Start discovering the UNIX Agents. You should start seeing output in your DebugView windows.  
  
4.  DebugView will present a step\-by\-step readout of the discovery wizard process. This is often the fastest method of troubleshooting discovery issues.  
  
## See Also  
[Using Templates for Additional Monitoring of UNIX and Linux](../../om/manage/Using-Templates-for-Additional-Monitoring-of-UNIX-and-Linux.md)  
[Troubleshooting UNIX and Linux Monitoring](../../om/manage/Troubleshooting-UNIX-and-Linux-Monitoring.md)  
[Accessing UNIX and Linux Computers in Operations Manager](../../om/manage/Accessing-UNIX-and-Linux-Computers-in-Operations-Manager.md)  
[Required Capabilities for UNIX and Linux Accounts](../../om/manage/Required-Capabilities-for-UNIX-and-Linux-Accounts.md)  
[Management Pack Issues](../../om/manage/Management-Pack-Issues.md)  
[Operating System Issues](../../om/manage/Operating-System-Issues.md)  
[Certificate Issues](../../om/manage/Certificate-Issues.md)  
[Managing Certificates for UNIX and Linux Computers](../Topic/Managing%20Certificates%20for%20UNIX%20and%20Linux%20Computers.md)  
[Managing Resource Pools for UNIX and Linux Computers](../../om/manage/Managing-Resource-Pools-for-UNIX-and-Linux-Computers.md)  
[Install Agent on UNIX and Linux Using the Discovery Wizard](../Topic/Install%20Agent%20on%20UNIX%20and%20Linux%20Using%20the%20Discovery%20Wizard.md)  
[How to enable Operations Manager logging for Remote Management Queries](../../om/manage/How-to-enable-Operations-Manager-logging-for-Remote-Management-Queries.md)  
[Manage UNIX and Linux Log Files](../../om/manage/Manage-UNIX-and-Linux-Log-Files.md)  
  
