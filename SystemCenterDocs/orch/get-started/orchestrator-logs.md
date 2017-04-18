---
title: Orchestrator Logs
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c06b17d-fd0d-4a98-8013-f5e5954606ed
ms.author: cfreeman
ms.date: 10/12/2016
author: cfreemanwa
manager: cfreeman
---
# Orchestrator Logs

> Applies To: System Center 2016 - Orchestrator

This section provides information on common troubleshooting issues and the available tools that can assist in identifying root problems.  

## Log files  
In Orchestrator, different logs are available that provide information about Orchestrator runbooks and servers. The following table lists the available types of log files, with links to the appropriate sections that describe the logs in more detail.  

|Log File Topic or Section|Contents|Where data is stored|Where data is viewed|  
|-----------------------------|------------|------------------------|------------------------|  
|[Real time log](../get-started/runbook-logs.md#RealTimeLog) section in Runbook Logs.|Live information about a running runbook instance|Orchestration database|**Log** tab in Runbook Designer|  
|[Historic Log](../get-started/runbook-logs.md#HistoryLog) section in Runbook Logs.|Historical information about instances of a runbook|Orchestration database|**Log History** tab in Runbook Designer|  
|[Runbook Audit History](../get-started/runbook-logs.md#AuditHistory) section in Runbook Logs.|Audit information about changes to a runbook|Orchestration database|**Audit History** tab in Runbook Designer|  
|[Activity Events](../get-started/activity-events.md)|Status information about Orchestrator management server, runbook servers, and database|Orchestration database|**Events** tab in Runbook Designer|  
|[Audit Trail](../manage/audit-trail.md)|Interaction of a runbook with external tools and systems|Log files|Open files in text editor|  
|[Trace Logs](../deploy/trace-logs.md)|Troubleshooting information about the Orchestrator environment|Log files|Open files in text editor|  

## Other resources for this product  

-   [Using Runbooks in System Center 2016 - Orchestrator](../get-started/using-runbooks.md))  

-   [Designing a Runbook](../../orchestrator/designing-a-runbook.md)  

-   [Building a Runbook](../manage/building-a-runbook.md)  

-   [How to Test a Runbook](../manage/how-to-test-a-runbook.md)  
