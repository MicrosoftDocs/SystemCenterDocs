---
title: Monitoring Activities
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5dd7238-924b-4de9-9a4a-044c432750f6
author: cfreemanwa
ms.author: cfreeman
ms.date: 10/12/2016
manager: cfreeman
---
# Monitoring Activities

> Apples To: System Center 2016 - Orchestrator

Monitoring activities are a specialized group of activities that are triggered by a state or event of a task outside of a runbook. For example, a monitor can wait for a particular event to occur in an event log, check the IP status of a certain computer, or run repeatedly on a predefined schedule.  

An Orchestrator activity cannot trigger a monitoring activity. A monitoring activity is a start condition within a runbook. The Monitor Folder activity waits for the files within a specified folder to change. When a file changes, the Monitor Folder activity triggers the next activity in the runbook workflow.  

Runbooks that start with a monitoring activity load the monitoring activity and wait for the trigger condition to occur. When the monitor activity detects the trigger condition, a runbook instance is created to run the remaining activities. The monitor continues to run and waits for the trigger event to reoccur. Runbooks that start with monitors continue to run until you stop them from the Runbook Designer or the Orchestration console.  
