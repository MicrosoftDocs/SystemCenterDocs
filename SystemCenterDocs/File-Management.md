---
title: File Management
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d491e346-f43e-4958-85cc-169305fc471e
---
# File Management
The following table provides a brief description of tasks you can accomplish when using each File Management activity.

|Tasks|File Management Activities|
|---------|------------------------------|
|Compress files into zip archives.|[Compress File](../Topic/Compress-File.md)|
|Copy files from one directory to another.|[Copy File](../Topic/Copy-File.md)|
|Create new folders.|[Create Folder](../Topic/Create-Folder.md)|
|Decompress files contained in a zip archive file.|[Decompress File](../Topic/Decompress-File.md)|
|Delete files.|[Delete File](../Topic/Delete-File.md)|
|Delete a folder, sub\-folder, or the entire folder tree of a directory.|[Delete Folder](../Topic/Delete-Folder.md)|
|Verify that a file exists.|[Get File Status](../Topic/Get-File-Status.md)|
|Invoke a runbook when files in folders and sub\-folder change.|[Monitor File](../Topic/Monitor-File.md)|
|Invoke a runbook when a folder or files within a folder change.|[Monitor Folder](../Topic/Monitor-Folder.md)|
|Move a file from one directory to another.|[Move File](../Topic/Move-File.md)|
|Move a folder and its sub\-folders from one directory to another.|[Move Folder](../Topic/Move-Folder.md)|
|Decrypt a file or an entire folder tree.|[PGP Decrypt File](../Topic/PGP-Decrypt-File.md)|
|Encrypt a file or an entire folder tree.|[PGP Encrypt File](../Topic/PGP-Encrypt-File.md)|
|Print text files.|[Print File](../Topic/Print-File.md)|
|Rename files.|[Rename File](../Topic/Rename-File.md)|

> [!CAUTION]
> If permissions on the [!INCLUDE[orchshort](../Token/orchshort_md.md)] installation path are changed and the activity’s Security Credentials has a custom user account that does not include **Read\/Execute** permissions to **ExecutionData.dll** on the Runbook server, the activity will fail.

