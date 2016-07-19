---
title: Trace Logs
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3165d194-b63d-455a-b6d9-dedf895ab096
author:bwren
manager:cfreemanwa
---
# Trace Logs
[!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] can create trace log messages on the management server to help you identify problems in the environment. By default, trace log messages are only written when there is an exception in the [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] Management Service, but you can increase this level of logging by modifying a registry setting. Trace log files are available in directories for each [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] feature under **C:\\ProgramData\\Microsoft System Center 2012\\Orchestrator**. You can change these log locations by changing the registry values for the different features.  
  
> [!NOTE]  
> The **C:\\ProgramData** directory is often a hidden system folder.  
  
## Modifying Trace Log Settings  
Trace log settings are configured with registry values under the key **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\SystemCenter2012\\Orchestrator\\TraceLogger**. Each of the [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] services has a set of registry values as shown in the following table.  
  
|Feature|Registry key|  
|-----------|----------------|  
|Audit Trail tool|Atlc.exe|  
|Data Store Configuration Utility|DBSetup.exe|  
|Management Service|ManagementService.exe|  
|Permissions Configuration tool|PermissionsConfig.exe|  
|Runbooks and activities|PolicyModule.exe|  
|Runbook Designer|RunbookDesigner.exe|  
|Runbook Server Monitor|RunbookServerMonitorService.exe|  
|Runbook Service|RunbookService.exe|  
|Runbook Tester|Runbook Tester.exe|  
  
The following table shows the values that are under each key. Modify these values as appropriate to change the logging details for that feature.  
  
|Registry value name|Default value|Description|  
|-----------------------|-----------------|---------------|  
|LogFolder|C:\\ProgramData\\Microsoft System Center 2012\\Orchestrator\\ManagementService.exe\\Logs|Location where trace logs are stored.|  
|LogLevel|1|Level of detail of information that is logged. Possible values are in the table below.|  
|LogPrefix|ManagementService.exe|Prefix of the log file name. This prefix is followed by the date and time when the log file is created.|  
|NewLogEvery|3600|Number of seconds until a new log file is created.|  
  
The following table provides the possible values that you can use for the log level.  
  
|Log level|Description|  
|-------------|---------------|  
|1|Exception detail only. This is the default setting.|  
|3|Exception detail with warnings and errors.|  
|7|Full logging.|  
  
## See Also  
[Orchestrator Logs](../../orch/manage/Orchestrator-Logs.md)  
  
