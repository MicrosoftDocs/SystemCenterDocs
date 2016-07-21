---
title: Using Operations Manager Shell
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74661318-fc5d-42f7-8a43-d1bcac5f12c5
author:mgoedtel
manager:cfreemanwa
---
# Using Operations Manager Shell
In [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)], the Operations Manager Shell is installed with the Operations Manager console; it provides a command\-line environment and task\-based scripting technology that you can use to automate many Operations Manager administrative tasks.  
  
The Operations Manager Shell is built on Windows PowerShell. The Operations Manager Shell extends Windows PowerShell with an additional set of *cmdlets*, which can either be run directly from the command shell prompt or called from within a script. Cmdlets can be used individually to perform a specific task, or they can be combined with other cmdlets to perform complex administrative tasks. Unlike traditional command\-line environments that work by returning text results to the end user or routing \("piping"\) text to different command\-line utilities, Windows PowerShell manipulates Microsoft .NET Framework objects directly. This provides a more robust and efficient mechanism for interacting with the system.  
  
To open the Operations Manager Shell, click **Start**, click **All Programs**, click **Microsoft System Center 2012**, click **Operations Manager**, and then click **Operations Manager Shell**. You can also import the Operations Manager module into an existing Windows PowerShell session by typing the following at the command prompt:  
  
```  
Import-Module -Name OperationsManager  
```  
  
You can access cmdlet help in the Operations Manager Shell by typing Get\-Help *cmdlet name* or view the help online at [Cmdlets in System Center&nbsp;2012&nbsp;-&nbsp;Operations Manager](http://go.microsoft.com/fwlink/p/?LinkId=235161).  
  
To learn more about Windows PowerShell, see [Windows PowerShell Getting Started Guide](http://go.microsoft.com/fwlink/p/?LinkId=235162).  
  
## See Also  
[General Tasks in Operations Manager_1](../Topic/General%20Tasks%20in%20Operations%20Manager_1.md)  
[Managing Alerts](../../om/manage/Managing-Alerts.md)  
[How to Suspend Monitoring Temporarily by Using Maintenance Mode](../../om/manage/How-to-Suspend-Monitoring-Temporarily-by-Using-Maintenance-Mode.md)  
[Creating and Managing Groups](../../om/manage/Creating-and-Managing-Groups.md)  
[Running Tasks in Operations Manager](../../om/manage/Running-Tasks-in-Operations-Manager.md)  
[How to Create a Resource Pool](../../om/manage/How-to-Create-a-Resource-Pool.md)  
[Managing Resource Pools for UNIX and Linux Computers](../../om/manage/Managing-Resource-Pools-for-UNIX-and-Linux-Computers.md)  
[Connecting Management Groups in Operations Manager](../../om/manage/Connecting-Management-Groups-in-Operations-Manager.md)  
  
