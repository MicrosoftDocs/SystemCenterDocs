---
title: Glossary for Opalis Integration Server 6.3
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b2826e5-da62-4cdd-87f3-eef89ecac651
---
# Glossary for Opalis Integration Server 6.3
The following table lists Opalis Integration Server 6.3 terms and the [!INCLUDE[orchshort](./Token/orchshort_md.md)] terms that replace them. A brief definition is included for each term.

|Opalis Integration Server 6.3 term|[!INCLUDE[orchlong](./Token/orchlong_md.md)] term|Definition|
|--------------------------------------|------------------------------------------------------|--------------|
|Action server|runbook server|A runbook server is a computer that receives an instance of a runbook and runs the sequence of activities. Runbook servers communicate directly with the orchestration database; they do not require a management server to run runbooks.|
|Client|Runbook Designer|See definition for Opalis client.|
|custom start|initialize data|The initial runbook activity defined in a runbook to provide user\-defined input parameters for the runbook.|
|datastore|orchestration database|The orchestration database is a SQL Server database containing configuration information, runbooks, and logs for [!INCLUDE[orchshort](./Token/orchshort_md.md)].|
|foundation object|standard activity|The set of runbook activities available in a default installation. This includes monitors, tasks, and all runbook controls.|
|object|activity|The tasks used to create a runbook.|
|Object palette|Activities pane|The **Activities** pane is located in the tasks pane in the Runbook Designer. Collections of activities are grouped by function or integration pack.|
|Opalis client|Runbook Designer|An application used to create, modify, and deploy runbooks.|
|Operator console|Orchestration console|The interface that enables a user to see available runbooks, the real\-time status of jobs and running instances, view their status, and start or stop runbooks, jobs, or instances.|
|Policy|runbook|A runbook is a collection of activities that orchestrates actions, events, and tasks.|
|Policy folder|runbook folder|A folder that contains one or more runbooks.|
|policy module|job process|A request to run a specific runbook that is waiting for assignment to a runbook server for processing.|
|Policy Testing Console|Runbook Tester|The tool used by Runbook Designers to test policies before deployment.|
|publish policy data|Published Data|Published Data is a runbook activity used to publish data from the runbook back to a calling \(parent\) runbook.|
|request|job|A job is a request to deploy and run a runbook on a runbook server. Jobs are stored in the orchestration  database queue.|
|trigger policy|Invoke Runbook|An **Invoke Runbook** activity calls another runbook from within a runbook. The **Invoke Runbook** activity can optionally wait for the called runbook to finish before proceeding. Data is returned from the invoked runbook by using the **Returned Data** activity. It is equivalent to the function call found in many programming languages.|
|workflow control|runbook control|A collection of standard activities that manage how runbook logic behaves.|


