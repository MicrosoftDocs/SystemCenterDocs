---
title: Modify the Orchestrator users group
description: Describes how to change the users group for System Center - Orchestrator.
ms.date: 01/17/2018
ms.prod: system-center
ms.technology: orchestrator
ms.topic: article
author: rayne-wiselman
ms.author: raynew
manager: carmonm
---

# Modify the Orchestrator users group

You might want to change the Orchestrator users group after installation because of changes in your environment. For example, you might want to use a local group during installation, and then change it to a domain account later.  

## PermissionsConfig tool  
You can change the Orchestrator Users group by using the PermissionsConfig tool, which is located on the management server in **<InstallDir>\\Management Server**. The syntax of this tool is as follows:  

**PermissionsConfig-OrchestratorUsersGroup***GroupName***-OrchestratorUser***UserName***\-remote**  

Note that the PermissionsConfig tool does not send results to standard output. To view the results of the command, check the **%errorlevel%** in the Orchestrator log file that is located at **C:\\Users\\SCXSVC\\AppData\\Local\\SCO\\LOGS**. The results are 1 for failure, 0 for success.  

You can get an explanation of the parameters for the PermissionsConfig tool by typing the following command:  

```  
PermissionsConfig -help  
```  

The following table explains the parameters.  

|Parameter|Details|  
|-------------|-----------|  
|OrchestratorUsersGroup|The name of the group to use for Orchestrator permissions.|  
|OrchestratorUser|If this parameter is specified with a user name, the user is granted immediate access to Orchestrator whether a member of the specified group or not. This is to prevent the requirement for the user to log off and on if the group has just been created.|  
|Remote|Indicates that the Runbook Designer can be run from a computer other than the management server.|  

For example, to change the Orchestrator users group to a group that is named Orchestrator Users in a domain that is named Contoso, use the following command:  

```  
PermissionsConfig -OrchestratorUsersGroup "Contoso\Orchestrator Users" -remote  
```  

> [!IMPORTANT]  
> You must run the PermissionsConfig tool at a command prompt with administrative credentials because it modifies group memberships. To do this, right-click the **Command Prompt** icon to select **Run as Administrator**.  

## Next steps
Review best practices for Orchestrator security at [Orchestrator Security Planning](https://technet.microsoft.com/en-us/library/hh420367.aspx).  
