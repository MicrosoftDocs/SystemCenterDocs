---
title: "File Management | Microsoft Docs"
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
ms.assetid: d491e346-f43e-4958-85cc-169305fc471e
caps.latest.revision: 8
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# File Management

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support, we recommend you to [upgrade to Orchestrator 2019](https://docs.microsoft.com/system-center/orchestrator/?view=sc-orch-2019).

::: moniker-end

The following table provides a brief description of tasks you can accomplish when using each File Management activity.  

|Tasks|File Management Activities|  
|-----------|--------------------------------|  
|Compress files into zip archives.|[Compress File](compress-file.md)|  
|Copy files from one directory to another.|[Copy File](copy-file.md)|  
|Create new folders.|[Create Folder](create-folder.md)|  
|Decompress files contained in a zip archive file.|[Decompress File](decompress-file.md)|  
|Delete files.|[Delete File](delete-file.md)|  
|Delete a folder, sub-folder, or the entire folder tree of a directory.|[Delete Folder](delete-folder.md)|  
|Verify that a file exists.|[Get File Status](get-file-status.md)|  
|Invoke a runbook when files in folders and sub-folder change.|[Monitor File](monitor-file.md)|  
|Invoke a runbook when a folder or files within a folder change.|[Monitor Folder](monitor-folder.md)|  
|Move a file from one directory to another.|[Move File](move-file.md)|  
|Move a folder and its sub-folders from one directory to another.|[Move Folder](move-folder.md)|  
|Decrypt a file or an entire folder tree.|[PGP Decrypt File](pgp-decrypt-file.md)|  
|Encrypt a file or an entire folder tree.|[PGP Encrypt File](pgp-encrypt-file.md)|  
|Print text files.|[Print File](print-file.md)|  
|Rename files.|[Rename File](rename-file.md)|  

> [!CAUTION]
>  If permissions on the Orchestrator installation path are changed, and the activity’s Security Credentials has a custom user account that does not include **Read/Execute** permissions to **ExecutionData.dll** on the Runbook server, the activity will fail.
