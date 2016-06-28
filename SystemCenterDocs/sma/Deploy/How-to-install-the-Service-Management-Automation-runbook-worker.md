---
title: How to install the Service Management Automation runbook worker
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3586c160-4e4d-4a08-9e30-13cdd49e8a01
---
# How to install the Service Management Automation runbook worker

>Applies To: Windows Azure Pack for Windows Server, System Center 2012 R2 Orchestrator

The Service Management Automation web service endpoint enables you to automate IT administration and business processes by using Windows PowerShell workflow-based runbooks in Windows Azure Pack for Windows Server.

Use the following information to install and configure the Automation runbook worker in Windows Azure Pack. Before installing or uninstalling an Automation runbook worker, ensure that you have stopped the Runbook Worker service (rbsvc) on the computer where the runbook worker is installed. For instructions on how to avoid any data loss when removing a runbook worker, including Windows PowerShell cmdlets and scripting help for this operation, see the [overview of runbook worker deployments](http://go.microsoft.com/fwlink/?LinkId=301478).

You can also install the Service Management Automation components by using an unattended installation. For more information, see [Install Service Management Automation from a Command Prompt](http://go.microsoft.com/fwlink/p/?LinkId=313193).

## Install a runbook worker
The Service Management Automation runbook worker provides the functionality to run Automation runbooks. The Service Management Automation runbook worker can be installed from the System Center 2012 R2 Orchestrator installation software. Install the runbook worker on a physical or virtual machine that has access to the same SQL Server instance that the Service Management Automation web service is using.

#### To install the runbook worker

1.  In the folder where you downloaded the System Center 2012 R2 Orchestrator installation software, click Setup to start the Setup wizard.

2.  Under **Service Management**, click **Runbook Worker**, and then click **Install**.

3.  Follow the instructions in the Setup wizard.

After the installation is complete, use administrative credentials to configure Automation in the Windows Azure Packmanagement portal.



