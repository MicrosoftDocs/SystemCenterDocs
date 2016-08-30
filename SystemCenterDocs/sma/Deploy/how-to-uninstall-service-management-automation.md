---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to uninstall Service Management Automation
ms.technology:  service-management-automation
ms.assetid:  adf42c66-20e4-450c-abfd-71bb0ff816da
---

# How to uninstall Service Management Automation

>Applies To: Windows Azure Pack for Windows Server, System Center 2012 R2 Orchestrator

You can use the following procedures to uninstall a Service Management Automation web console, runbook worker, or PowerShell module. Before uninstalling an Automation runbook worker, ensure that you have stopped the Runbook Worker service (rbsvc) on the computer where the runbook worker is installed. For instructions on how to avoid any data loss when removing a runbook worker, including Windows PowerShell cmdlets and scripting help for this operation, see the [overview of runbook worker deployments](http://go.microsoft.com/fwlink/?LinkId=301478).

#### To uninstall a Service Management Automation web service

1.  On the computer on which the web service is installed, click **Start**, and then click **Control Panel**.

2.  Under **Programs**, click **Uninstall a program**.

3.  Under **Name**, double-click **System Center 2012 R2 Service Management Automation Web Service**.

4.  Follow the prompts, and the **Uninstalling features** page appears and uninstallation progress is displayed.

#### To uninstall a Service Management Automation runbook worker

1.  Ensure that you have prepared for removing the runbook worker as described in the [overview of runbook worker deployments](http://go.microsoft.com/fwlink/?LinkId=301478).

2.  On the computer on which the runbook worker is installed, click **Start**, and then click **Control Panel**.

3.  Under **Programs**, click **Uninstall a program**.

4.  Under **Name**, double-click **System Center 2012 R2 Service Management Automation Runbook Worker**.

5.  Follow the prompts, and the **Uninstalling features** page appears and uninstallation progress is displayed.

#### To uninstall a Service Management Automation PowerShell module

1.  On the computer on which the PowerShell module is installed, click **Start**, and then click **Control Panel**.

2.  Under **Programs**, click **Uninstall a program**.

3.  Under **Name**, double-click **System Center 2012 R2 Service Management Automation Powershell**.

4.  Follow the prompts, and the **Uninstalling features** page appears and uninstallation progress is displayed.



