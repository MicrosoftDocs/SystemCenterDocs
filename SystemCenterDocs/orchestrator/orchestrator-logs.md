---
title: Orchestrator logs
description: Provides information about common troubleshooting issues using log files.
ms.custom: UpdateFrequency3, engagment-fy24
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c06b17d-fd0d-4a98-8013-f5e5954606ed
ms.date: 11/09/2023
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
---
# Orchestrator logs

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

This article provides information on common troubleshooting issues and the available tools that can help identify the root problems.  

## Log files  
In Orchestrator, different logs are available that provide information about Orchestrator runbooks and servers. The following table lists the available types of log files, with links to the appropriate sections that describe the logs in more detail.  

|Log File Topic or Section|Contents|Where data is stored|Where data is viewed|  
|-----------------------------|------------|------------------------|------------------------|  
|[Real time log](design-and-build-runbooks.md) section in Runbook Logs.|Live information about a running runbook instance|Orchestration database|**Log** tab in Runbook Designer|  
|[Historic Log](design-and-build-runbooks.md) section in Runbook Logs.|Historical information about instances of a runbook|Orchestration database|**Log History** tab in Runbook Designer|  
|[Runbook Audit History](design-and-build-runbooks.md) section in Runbook Logs.|Audit information about changes to a runbook|Orchestration database|**Audit History** tab in Runbook Designer|  
|[Activity Events](activity-events.md)|Status information about Orchestrator management server, runbook servers, and database|Orchestration database|**Events** tab in Runbook Designer|  
|[Audit Trail](track-runbooks-audit-trail.md)|Interaction of a runbook with external tools and systems|Log files|Open files in text editor|  
|[Trace Logs](~/orchestrator/design-and-build-runbooks.md)|Troubleshooting information about the Orchestrator environment|Log files|Open files in text editor|  
