---
title: Text File Management
description: This article provides information about the tasks that you can do using text file management activities.  
ms.custom: ""
ms.date: "05/13/2016"
ms.prod: system-center
ms.reviewer: ""
ms.suite: ""
ms.technology: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center 2012 SP1 - Orchestrator"
  - "System Center 2012 - Orchestrator"
  - "System Center 2012 R2 Orchestrator"
ms.assetid: 59a60b8a-2fb3-4dc9-9d3a-06cfd66db866
caps.latest.revision: 7
author: "jyothisuri"
ms.author: "jsuri"
manager: "evansma"
---
# Text File Management

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support. We recommend you to [upgrade to Orchestrator 2019](../index.yml).

::: moniker-end

The following table provides a brief description of tasks you can accomplish when using each Text File Management activity.  

> [!CAUTION]
> If permissions on the installation path are changed and the activity’s Security Credentials has a custom user account that doesn't include **Read/Execute** permissions to **ExecutionData.dll** on the Runbook server, the activity will fail.  

|Tasks|Text File Management Activities|  
|-----------|-------------------------------------|  
|Append a line of text into a text file.|[Append Line](append-line.md)|  
|Delete lines from a text file.|[Delete Line](delete-line.md)|  
|Find lines in a text file.|[Find Text](find-text.md)|  
|Get multiple lines from a text file.|[Get Lines](get-lines.md)|  
|Insert lines into a text file on a line number you specify.|[Insert Line](insert-line.md)|  
|Read lines from a text file.|[Read Line](read-line.md)|  
|Search for and replaces text in a file.|[Search and Replace Text](search-and-replace-text.md)|