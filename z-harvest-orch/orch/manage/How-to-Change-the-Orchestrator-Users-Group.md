---
title: How to Change the Orchestrator Users Group
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1d182f3-b80b-4414-90e6-4c0a10d62f60
author:bwren
manager:cfreemanwa
---
# How to Change the Orchestrator Users Group
You might want to change the [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] users group after installation because of changes in your environment. For example, you might want to use a local group during installation, and then change it to a domain account later.  
  
## PermissionsConfig tool  
You can change the Orchestrator Users group by using the PermissionsConfig tool, which is located on the management server in **<InstallDir>\\Management Server**. The syntax of this tool is as follows:  
  
**PermissionsConfig-OrchestratorUsersGroup***GroupName***-OrchestratorUser***UserName***\-remote**  
  
Note that the PermissionsConfig tool does not send results to standard output. To view the results of the command, check the **%errorlevel%** in the [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] log file that is located at **C:\\Users\\SCXSVC\\AppData\\Local\\SCO\\LOGS**. The results are 1 for failure, 0 for success.  
  
You can get an explanation of the parameters for the PermissionsConfig tool by typing the following command:  
  
```  
PermissionsConfig -help  
```  
  
The following table explains the parameters.  
  
|Parameter|Details|  
|-------------|-----------|  
|OrchestratorUsersGroup|The name of the group to use for [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] permissions.|  
|OrchestratorUser|If this parameter is specified with a user name, the user is granted immediate access to [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] whether a member of the specified group or not. This is to prevent the requirement for the user to log off and on if the group has just been created.|  
|Remote|Indicates that the Runbook Designer can be run from a computer other than the management server.|  
  
For example, to change the [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] users group to a group that is named [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] Users in a domain that is named Contoso, use the following command:  
  
```  
PermissionsConfig -OrchestratorUsersGroup "Contoso\Orchestrator Users" -remote  
```  
  
> [!IMPORTANT]  
> You must run the PermissionsConfig tool at a command prompt with administrative credentials because it modifies group memberships. To do this, right\-click the **Command Prompt** icon to select **Run as Administrator**.  
  
## See Also  
[Orchestrator Security Planning](assetId:///358c5344-8649-4d40-a53c-37f8e70e58f6)  
  
