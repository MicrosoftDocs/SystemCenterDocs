---
title: Best Practices Analyzer
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f6789a1-d389-40d9-a3e4-92ea745f062d
author:bwren
manager:cfreemanwa
---
# Best Practices Analyzer
The Microsoft System Center 2012 \- Orchestrator Best Practices Analyzer is a tool that looks at the configuration data in an Orchestrator deployment and identifies settings that may cause issues within your environment. It performs the following functions:  
  
-   Gathers information about an Orchestrator deployment  
  
-   Determines if the configurations are set according to the Microsoft recommended best practices  
  
-   Reports on collected configurations, indicating settings that differ from recommendations  
  
-   Indicates potential problems in the deployment  
  
## Installation  
The Orchestrator BPA must be installed on the Orchestrator Management server. It depends on having the Microsoft Baseline Configuration Analyzer 2.1 \([http:\/\/www.microsoft.com\/download\/en\/details.aspx?displaylang\=en&id\=16475](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=16475)\) installed on the Orchestrator Management Server prior to installation.  
  
Install process:  
  
1.  Install Microsoft Baseline Configuration Analyzer 2.1  
  
2.  Run Microsoft.SystemCenter.2012.Orchestrator.BestPracticesAnalyzer.msi  
  
Uninstall process:  
  
1.  Remove Microsoft System Center 2012 Orchestrator – Best Practices Analyzer \(BPA\) from the Programs and Features panel within Windows Control Panel.  
  
## Usage  
  
1.  Run the Microsoft Baseline Configuration Analyzer 2.1 from the Start menu in windows.  
  
    > [!NOTE]  
    > To learn how to run the Microsoft Baseline Configuration Analyzer scans from PowerShell cmdlets, please see the MBCA 2.1 help file.  
  
2.  Select System Center 2012 – Orchestrator BPA from the product dropdown within the MBCA 2.1 user interface.  
  
3.  Click Start Scan.  
  
4.  Review the results and recommendations.  
  
## Orchestrator rules  
[!INCLUDE[orchlong](../../orch/deploy/includes/orchlong_md.md)] configuration checks:  
  
|Orchestrator Component|Rule|Description|  
|--------------------------|--------|---------------|  
|Management Server|Check log purge is set to the default value|This rule checks that the default log purging for Runbooks is set to the default values for running every one day and to keep the last five hundred entries. Please refer to [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=239613](http://go.microsoft.com/fwlink/?LinkID=239613) for more information about setting the purging policy for Runbook logs.|  
|Management Server|Check the refresh interval for permissions in the Orchestration console|This rule checks that the default refresh interval for generating the cache that allows access to runbooks from the Orchestration Console is set to six hundred seconds. Please refer to [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=239946](http://go.microsoft.com/fwlink/?LinkID=239946) for more information on how the refresh cache is set up.|  
|Management Server|Check logging on ManagementService.exe|This rule checks that the default trace logging on the ManagementService.exe is set to the default of 1. This can impact performance if a different value is configured. Please refer to [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=239530](http://go.microsoft.com/fwlink/?LinkID=239530) for more information on configuring trace logs.|  
|Management Server|Check logging on PermissionsConfig.exe|This rule checks that the default trace logging on the PermissionsConfig.exe is set to the default of 1. This can impact performance if a different value is configured. Please refer to [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=239530](http://go.microsoft.com/fwlink/?LinkID=239530) for more information on configuring trace logs.|  
|Management Server|Check logging on Runbooks|This rule checks if logging is enabled on Runbooks. This can impact performance if logging is enabled on frequently used Runbooks. Please refer to [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=239614](http://go.microsoft.com/fwlink/?LinkID=239614) for more information on enabling logging on Runbooks.|  
|Management Server|Check memory on Management  Servers|This rule checks that the memory allocated to the Management Server is greater than 2048MB. If the Management Server has less than 2048MB you should monitor its performance to ensure it is meeting the expected goals in the environment. Please refer to [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=242545](http://go.microsoft.com/fwlink/?LinkID=242545) for information on the Orchestrator Management Pack.|  
|Runbook Server|Check that maximum concurrent runbooks is set to the default value of 50.|This rule checks that the maximum number of concurrent runbooks that are configured to run on a Runbook Server is set to fifty. This can impact performance if a different value is configured. Please refer to [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=239560](http://go.microsoft.com/fwlink/?LinkID=239560) for more information on configuring Runbook throttling.|  
|Runbook Server|Check logging for PolicyModule.exe|This rule checks that the default trace logging on the PolicyModule.exe is set to the default of 1. This can impact performance if a different value is configured. Please refer to [HYPERLINK "http:\/\/go.microsoft.com\/fwlink\/?LinkID\=239530http:\/\/go.microsoft.com\/fwlink\/?LinkID\=239530" http:\/\/go.microsoft.com\/fwlink\/?LinkID\=239530](http://go.microsoft.com/fwlink/?LinkID=239530) for more information on configuring trace logs.|  
|Runbook Server|Check logging for RunbookService.exe|This rule checks that the default trace logging on the RunbookService.exe is set to the default of 1. This can impact performance if a different value is configured. Please refer to [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=239530](http://go.microsoft.com/fwlink/?LinkID=239530) for more information on configuring trace logs.|  
|Runbook Server|Check memory on Runbook Servers|This rule checks that the memory allocated to the Runbook Servers is greater than 2048MB. If the Runbook Server has less than 2048MB you should monitor its performance to ensure it is meeting the expected goals in the environment.|  
|Web components|Check memory on the server hosting the Orchestration Console|This rule checks that the memory allocated to the Orchestration Console server is greater than 2048MB. If the server has less than 2048MB you should monitor its performance to ensure it is meeting the expected goals in the environment. Please refer to [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=242545](http://go.microsoft.com/fwlink/?LinkID=242545) for information on the Orchestrator Management Pack.|  
|Web components|Check users group managing runbook access|This rule checks that the windows group that is used to manage access to runbooks is configured as a domain group if the web components are not installed on the Management Server. The group must be a domain group in order for users to have access through the web service and Orchestration console when the web components are installed on a separate server than the Management Server. Please refer to [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=239561](http://go.microsoft.com/fwlink/?LinkID=239561) for more information on configuring the Orchestrator users group.|  
|Designer|Check memory on the computer hosting the Orchestrator Designer|This rule checks that the memory allocated to the Orchestrator Designer is greater than 2048MB. If the computer has less than 2048MB you should monitor its performance to ensure it is meeting the expected goals in the environment. Please refer to [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=242545](http://go.microsoft.com/fwlink/?LinkID=242545) for information on the Orchestrator Management Pack.|  
  
