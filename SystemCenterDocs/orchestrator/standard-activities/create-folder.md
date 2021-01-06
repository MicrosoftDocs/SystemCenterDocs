---
title: "Create Folder | Microsoft Docs"
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
ms.assetid: 8fdf738a-6dc7-4173-a940-406d9cb81729
caps.latest.revision: 12
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Create Folder

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support, we recommend you to [upgrade to Orchestrator 2019](https://docs.microsoft.com/system-center/orchestrator/).

::: moniker-end

The Create Folder activity creates a new folder on the local file system or a network location specified using a UNC path. Use the Create Folder activity to create folders dynamically with names that represent the context in which they were created. For example, on August 25 you can create `"C:\backupfolderAug25"`.  

## Configuring the Create Folder Activity  
 Before you configure the Create Folder activity, you need to know the name of the folder that you are creating.  

 Use the following information to configure the Create Folder activity.  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Folder path|The path of the folder that was created.|
