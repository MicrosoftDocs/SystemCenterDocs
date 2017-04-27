---
title: How to Configure Runbook Throttling
description: Describes how to change the maximum number of runbooks that can be simultaneously run in System Center 2016 - Orchestrator.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dfa35522-ed49-4239-94b3-affe2a853420
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
---

# How to Configure Runbook Throttling

> Applies To: System Center 2016 - Orchestrator

By default, each runbook server is configured to simultaneously run a maximum of 50 runbooks. You can change this number by using the Runbook Server Runbook Throttling tool. In most cases, you can keep this default setting, but you should consider the resource requirements of the runbooks on a particular server when considering whether to change it. If the server has a number of runbooks with high resource requirements, you might run fewer runbooks simultaneously on the runbook server. If they are simple runbooks with minimal requirements, you might consider increasing the number of simultaneously run runbooks.  

## To configure the maximum number of runbooks that a runbook server processes  

1.  Navigate to the folder where by default the Runbook Server Runbook Throttling tool is stored: **<System Drive>:\\Program Files \(x86\)\\Microsoft System Center 2016\\Orchestrator\\Management Server**.  

2.  Type one of the following commands:  

    -   To apply the change to one runbook server:  

        **aspt <RunbookServerName> <MaximumRunningRunbooks>.**  

        For example, to set the maximum number of runbooks that RunbookServer1 runs to 40:  

        **aspt RunbookServer1 40**  

    -   To apply the change to all runbook servers:  

        **aspt \* <MaximumRunningRunbooks>.**  

        For example, to set the maximum number of runbooks that all runbook servers run to 40:  

        **aspt \* 40**  

3.  Restart the **Orchestrator Runbook Service**.  

## Next steps
[Administering System Center 2016 - Orchestrator](../orch/manage/administering-orchestrator.md)  
