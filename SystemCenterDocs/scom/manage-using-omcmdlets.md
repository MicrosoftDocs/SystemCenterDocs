---
ms.assetid: 315fec65-847e-4621-92ce-1cf50296b43b
title: Using Operations Manager Shell
description: This article describes how to use the Operations Manager shell to perform administrative tasks with PowerShell.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# Using Operations Manager Shell



In System Center Operations Manager, the Operations Manager Shell is installed with the Operations Manager console; it provides a command-line environment and task-based scripting technology that you can use to automate many Operations Manager administrative tasks.  

The Operations Manager Shell is built on Windows PowerShell. The Operations Manager Shell extends Windows PowerShell with an additional set of *cmdlets*, which can either be run directly from the command shell prompt or called from within a script. Cmdlets can be used individually to perform a specific task, or they can be combined with other cmdlets to perform complex administrative tasks. Unlike traditional command-line environments that work by returning text results to the end-user or routing (**piping**) text to different command-line utilities, Windows PowerShell manipulates Microsoft .NET Framework objects directly. This provides a more robust and efficient mechanism for interacting with the system.  

To open the Operations Manager Shell, from the Windows start screen, enter **Operations Manager** and select **Operations Manager Shell** from the search results.  You can also import the Operations Manager module into an existing Windows PowerShell session by entering the following at the command prompt:  

```  
Import-Module -Name OperationsManager  
```  

You can access cmdlet help in the Operations Manager Shell by entering Get-Help *cmdlet name* or view the help online at [Cmdlets in System Center Operations Manager](/powershell/module/operationsmanager/).  

To learn more about Windows PowerShell, see [Windows PowerShell Getting Started Guide](/previous-versions//aa973757(v=vs.85)).  

## Next steps

- To stop monitoring a computer, group of computers, or monitored object temporarily during planned maintenance using a schedule, or to stop monitoring while troubleshooting an issue, see [How to Suspend Monitoring Temporarily by Using Maintenance Mode](manage-maintenance-mode-overview.md).

- To learn how to launch common tools or commands from the Operations Manager console to help reduce your time investigating and diagnosing issues, see [Running Tasks in Operations Manager](manage-running-tasks.md).
