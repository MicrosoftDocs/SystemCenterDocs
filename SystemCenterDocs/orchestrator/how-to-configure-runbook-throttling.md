---
title: How to Configure Runbook Throttling
description: Describes how to change the maximum number of runbooks that can be simultaneously run in System Center - Orchestrator.
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dfa35522-ed49-4239-94b3-affe2a853420
author: jyothisuri
ms.author: jsuri
ms.custom: engagement-fy23
---

# Configure runbook throttling

You can adjust the number of runbooks that are run concurrently on a runbook server. Reducing the number is known as **runbook throttling**. By default, each runbook server is configured to simultaneously run a maximum of 50 runbooks. You can change this number by using the Runbook Server Runbook Throttling tool. In most cases, you can keep this default setting, but you should consider the resource requirements of the runbooks on a particular server when considering whether to change it. If the server has many runbooks with high resource requirements, you might run fewer runbooks simultaneously on the runbook server. If they're simple runbooks with minimal requirements, you might consider increasing the number of simultaneously run runbooks.  

## Configure the maximum number of runbooks that a runbook server processes  

Follow these steps to configure the maximum number of runbooks that a runbook server processes:

::: moniker range="<=sc-orch-2019"
1.  Navigate to the folder whereby default the Runbook Server Runbook Throttling tool is stored: `C:\Program Files (x86)\Microsoft System Center\Orchestrator\Management Server`.  
::: moniker-end

::: moniker range=">=sc-orch-2022"
1.  Navigate to the folder whereby default the Runbook Server Runbook Throttling tool is stored: `C:\Program Files\Microsoft System Center\Orchestrator\Management Server`.  
::: moniker-end

2. Enter one of the following commands:  

    - To apply the change to one runbook server:  

        `aspt <RunbookServerName> <MaximumRunningRunbooks>.`

        For example, to set the maximum number of runbooks that RunbookServer1 runs to 40:  

        `aspt RunbookServer1 40`

    - To apply the change to all runbook servers:  

        `aspt * <MaximumRunningRunbooks>.`  

        For example, to set the maximum number of runbooks that all runbook servers run to 40:  

        `aspt * 40`  

3. Restart the **Orchestrator Runbook Service**.  

## Next steps

Learn more about optimizing Orchestrator performance at [Database sizing and performance](database-sizing-and-performance.md).  
