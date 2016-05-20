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
The [!INCLUDE[sma_1](Token/sma_1_md.md)] web service endpoint enables you to automate IT administration and business processes by using Windows PowerShell workflow\-based runbooks in [!INCLUDE[katal_1](Token/katal_1_md.md)].

Use the following information to install and configure the [!INCLUDE[sma_2](Token/sma_2_md.md)] runbook worker in [!INCLUDE[katal_2](Token/katal_2_md.md)]. Before installing or uninstalling an [!INCLUDE[sma_2](Token/sma_2_md.md)] runbook worker, ensure that you have stopped the Runbook Worker service \(rbsvc\) on the computer where the runbook worker is installed. For instructions on how to avoid any data loss when removing a runbook worker, including Windows PowerShell cmdlets and scripting help for this operation, see the [overview of runbook worker deployments](http://go.microsoft.com/fwlink/?LinkId=301478).

You can also install the [!INCLUDE[sma_1](Token/sma_1_md.md)] components by using an unattended installation. For more information, see [Install Service Management Automation from a Command Prompt](http://go.microsoft.com/fwlink/p/?LinkId=313193).

## Install a runbook worker
The [!INCLUDE[sma_1](Token/sma_1_md.md)] runbook worker provides the functionality to run [!INCLUDE[sma_2](Token/sma_2_md.md)] runbooks. The [!INCLUDE[sma_1](Token/sma_1_md.md)] runbook worker can be installed from the [!INCLUDE[orchblue_1](Token/orchblue_1_md.md)] installation software. Install the runbook worker on a physical or virtual machine that has access to the same SQL Server instance that the [!INCLUDE[sma_1](Token/sma_1_md.md)] web service is using.

#### To install the runbook worker

1.  In the folder where you downloaded the [!INCLUDE[orchblue_1](Token/orchblue_1_md.md)] installation software, click Setup to start the Setup wizard.

2.  Under **Service Management**, click **Runbook Worker**, and then click **Install**.

3.  Follow the instructions in the Setup wizard.

After the installation is complete, use administrative credentials to configure [!INCLUDE[sma_2](Token/sma_2_md.md)] in the [!INCLUDE[katal_2](Token/katal_2_md.md)][!INCLUDE[katal_portal](Token/katal_portal_md.md)].


