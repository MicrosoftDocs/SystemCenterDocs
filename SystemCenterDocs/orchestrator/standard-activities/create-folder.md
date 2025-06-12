---
title: Create Folder activity
description: This article describes the Create Folder activity that creates a new folder on the local file system
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 8fdf738a-6dc7-4173-a940-406d9cb81729
caps.latest.revision: 12
author: jyothisuri
ms.author: jsuri
---
# Create folder activity

The Create Folder activity creates a new folder on the local file system or a network location specified using a UNC path. Use the Create Folder activity to create folders dynamically with names that represent the context in which they were created. For example, on August 25, you can create `"C:\backupfolderAug25"`.  

## Configure the Create Folder Activity

 Before you configure the Create Folder activity, you need to know the name of the folder that you're creating.  

 Use the following information to configure the Create Folder activity.  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Folder path|The path of the folder that was created.|
