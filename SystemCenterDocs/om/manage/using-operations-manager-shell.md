---
ms.assetid: 315fec65-847e-4621-92ce-1cf50296b43b
title: Using Operations Manager Shell
description: 
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Using Operations Manager Shell

>Applies To: System Center 2016 - Operations Manager

In System Center 2016 - Operations Manager, the Operations Manager Shell is installed with the Operations Manager console; it provides a command-line environment and task-based scripting technology that you can use to automate many Operations Manager administrative tasks.  
  
The Operations Manager Shell is built on Windows PowerShell. The Operations Manager Shell extends Windows PowerShell with an additional set of *cmdlets*, which can either be run directly from the command shell prompt or called from within a script. Cmdlets can be used individually to perform a specific task, or they can be combined with other cmdlets to perform complex administrative tasks. Unlike traditional command-line environments that work by returning text results to the end user or routing ("piping") text to different command-line utilities, Windows PowerShell manipulates Microsoft .NET Framework objects directly. This provides a more robust and efficient mechanism for interacting with the system.  
  
To open the Operations Manager Shell, from the Windows start screen, type **Operations Manager** and select **Operations Manager Shell** from the search results.  You can also import the Operations Manager module into an existing Windows PowerShell session by typing the following at the command prompt:  
  
```  
Import-Module -Name OperationsManager  
```  
  
You can access cmdlet help in the Operations Manager Shell by typing Get-Help *cmdlet name* or view the help online at [Cmdlets in System Center 2012 - Operations Manager](http://go.microsoft.com/fwlink/p/?LinkId=235161).  
  
To learn more about Windows PowerShell, see [Windows PowerShell Getting Started Guide](http://go.microsoft.com/fwlink/p/?LinkId=235162).  
  
## Next steps

- To stop monitoring of a computer, group of computers or monitored object temporarily during planned maintenance using a schedule, or to stop monitoring while troubleshooting an issue, see [How to Suspend Monitoring Temporarily by Using Maintenance Mode](How-to-Suspend-Monitoring-Temporarily-by-Using-Maintenance-Mode.md). 

- To learn how to launch common tools or commands from the Operations Manager console to help reduce your time investigating and diagnosing issues, see [Running Tasks in Operations Manager](Running-Tasks-in-Operations-Manager.md).    


  
