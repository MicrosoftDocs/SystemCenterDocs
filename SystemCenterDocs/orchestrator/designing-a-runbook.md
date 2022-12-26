---
title: Designing a Runbook
description: Describes how to design a new runbook for System Center 2016 - Orchestrator.
ms.custom: na
ms.date: 04/25/2017
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0af32cb-3faf-4f13-b9eb-eadc10effe1b
author: jyothisuri
ms.author: jsuri
manager: evansma
---

# Designing a Runbook

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

When you plan a new runbook, you should start with a defined process that you want to automate. This process determines your choice of runbook activities. Specifically, determine the following:  

-   When and how often is the runbook going to run?  
-   What steps make up the workflow?  
-   What activities reflect the steps in my workflow?  
-   What type of data is required to begin the workflow?  
-   What data are generated from each activity?  
-   What results are produced at the end of the workflow?  
-   How are the runbook results reported?  

Consider the following points as you design your runbook:  

1.  Failure and Warning links \- It's important to handle all results from an activity. An activity provides a default success string, but doesn't provide a default failure case. Consider if you should reverse an activity or write the result to a log file.  

2.  Replace the default strings \- When you look at the workflow in a runbook, the labels should identify what the individual activities are doing. Rename links and activities labels to a descriptive name.  

3.  Link colors \- Change the color of your links when there's a condition or branch. It's common to use GREEN as success and RED for warning or failed. You should use standard associations, but not use too many colors or you lose their descriptive purpose.  

4.  Limit the number of activities per runbook \- Too many activities in a single runbook make it difficult to administer and troubleshoot. Consider splitting a runbook into several subtasks and create child runbooks for each of those subtasks. You can invoke the child runbooks from a parent runbook. You can reuse these child runbooks in other workflows.  

5.  Runbook logs \- By default, logging options are disabled for runbooks. When you enable&nbsp;logging, the data significantly increases the size of your database. As an alternative, you can log to an external system or file.  

## Next steps
[Build and test a runbook](./design-and-build-runbooks.md).
