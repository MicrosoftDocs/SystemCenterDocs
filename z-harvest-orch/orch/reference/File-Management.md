---
title: File Management
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d491e346-f43e-4958-85cc-169305fc471e
author:bwren
manager:cfreemanwa
---
# File Management
The following table provides a brief description of tasks you can accomplish when using each File Management activity.  
  
|Tasks|File Management Activities|  
|---------|------------------------------|  
|Compress files into zip archives.|[Compress File](../../orch/reference/Compress-File.md)|  
|Copy files from one directory to another.|[Copy File](../../orch/reference/Copy-File.md)|  
|Create new folders.|[Create Folder](../../orch/reference/Create-Folder.md)|  
|Decompress files contained in a zip archive file.|[Decompress File](../../orch/reference/Decompress-File.md)|  
|Delete files.|[Delete File](../../orch/reference/Delete-File.md)|  
|Delete a folder, sub\-folder, or the entire folder tree of a directory.|[Delete Folder](../../orch/reference/Delete-Folder.md)|  
|Verify that a file exists.|[Get File Status](../../orch/reference/Get-File-Status.md)|  
|Invoke a runbook when files in folders and sub\-folder change.|[Monitor File](../../orch/reference/Monitor-File.md)|  
|Invoke a runbook when a folder or files within a folder change.|[Monitor Folder](../../orch/reference/Monitor-Folder.md)|  
|Move a file from one directory to another.|[Move File](../../orch/reference/Move-File.md)|  
|Move a folder and its sub\-folders from one directory to another.|[Move Folder](../../orch/reference/Move-Folder.md)|  
|Decrypt a file or an entire folder tree.|[PGP Decrypt File](../../orch/reference/PGP-Decrypt-File.md)|  
|Encrypt a file or an entire folder tree.|[PGP Encrypt File](../../orch/reference/PGP-Encrypt-File.md)|  
|Print text files.|[Print File](../../orch/reference/Print-File.md)|  
|Rename files.|[Rename File](../../orch/reference/Rename-File.md)|  
  
> [!CAUTION]  
> If permissions on the [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] installation path are changed and the activity's Security Credentials has a custom user account that does not include **Read\/Execute** permissions to **ExecutionData.dll** on the Runbook server, the activity will fail.  
  
