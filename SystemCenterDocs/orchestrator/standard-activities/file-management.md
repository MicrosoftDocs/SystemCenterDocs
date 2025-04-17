---
title: File Management
description: This article provides information on the various File Management activities.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 04/16/2025
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d491e346-f43e-4958-85cc-169305fc471e
caps.latest.revision: 8
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
---
# File Management

This article provides information on the various File Management activities.

The following table provides a brief description of tasks you can accomplish when using each File Management activity: 

|Tasks|File management activities|  
|-----------|--------------------------------|  
|Compress files into zip archives|[Compress File](compress-file.md)|  
|Copy files from one directory to another|[Copy File](copy-file.md)|  
|Create new folders|[Create Folder](create-folder.md)|  
|Decompress files contained in a zip archive file|[Decompress File](decompress-file.md)|  
|Delete files|[Delete File](delete-file.md)|  
|Delete a folder, sub-folder, or the entire folder tree of a directory|[Delete Folder](delete-folder.md)|  
|Verify that a file exists|[Get File Status](get-file-status.md)|  
|Invoke a runbook when files in folders and sub-folder change|[Monitor File](monitor-file.md)|  
|Invoke a runbook when a folder or files within a folder change|[Monitor Folder](monitor-folder.md)|  
|Move a file from one directory to another|[Move File](move-file.md)|  
|Move a folder and its sub-folders from one directory to another|[Move Folder](move-folder.md)|  
|Decrypt a file or an entire folder tree|[PGP Decrypt File](pgp-decrypt-file.md)|  
|Encrypt a file or an entire folder tree|[PGP Encrypt File](pgp-encrypt-file.md)|  
|Print text files|[Print File](print-file.md)|  
|Rename files|[Rename File](rename-file.md)|  

> [!CAUTION]
> If the permissions on the Orchestrator installation path are changed and the activity’s Security Credentials has a custom user account that doesn't include **Read/Execute** permissions to **ExecutionData.dll** on the Runbook server, the activity will fail.
