---
title: Manage and run DPM jobs
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b45c90ea-f6f8-4a1b-9d26-59944103f461
---
# Manage and run DPM jobs
This section describes how to work with DPM jobs, as follows:

-   [Work with jobs](../Topic/Work-with-jobs.md)—Describes how to work with jobs, including viewing jobs, retrying and canceling jobs, checking job status, specifying how jobs are displayed, and searching for jobs.

-   [Modify the schedule for protection jobs with Windows PowerShell](../Topic/Modify-the-schedule-for-protection-jobs-with-Windows-PowerShell.md)—Describes how to retrieve, set, or delete the schedule for protection jobs \(catalog pruning and detailed inventory\) using Windows PowerShell. This setting can only be configured with PowerShell.

-   [Modify the schedule for maintenance jobs with Windows PowerShell](../Topic/Modify-the-schedule-for-maintenance-jobs-with-Windows-PowerShell.md)—Describes how to retrieve, set, or delete the schedule for maintenance jobs using Windows PowerShell. This setting can only be configured with PowerShell.

## DPM jobs
The following table summarizes the types of jobs that DPM performs.

|Job type|Description|
|------------|---------------|
|Replica creation|Occurs when an initial replica of a data source selected for protection is being created in [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)].|
|Consistency check|Occurs when the replica in [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] is being checked for consistency with the data source on the protected computer. [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] fixes any issues that are found.|
|Synchronization|Files: Occurs when the replica in [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] is being updated with the changes from the protected computer.<br /><br />Applications: Occurs when the recovery point creation job synchronizes and creates a recovery point.|
|Recovery point|Occurs when a recovery point of a replica is being created in [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)].|
|Disk recovery|Occurs when data is in the process of being recovered from a disk\-based recovery point.|
|Tape erase data|Occurs when data on a selected tape is erased.|
|Drive cleaning|Occurs when a tape drive is cleaned.|
|Detailed inventory|Occurs when the administrator runs a detailed inventory on a tape.|
|Fast inventory|Occurs when the administrator runs a fast inventory on a tape.|
|Tape verification|Occurs when a selected tape is verified.|
|Data copy|Occurs when selected data is copied.|
|Tape backup|Occurs when a selected tape is backed up.|
|Tape recovery|Occurs when data on a tape is recovered.|
|Copy data \- tape|Occurs when data from a tape is copied to disk or to another tape.|
|Recoverable items recatalog|Occurs when a tape from another [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server is being recataloged.|
|Tape recatalog|Occurs when a tape is recataloged.|
|Library rescan|Occurs when a library is rescanned.|
|SharePointCatalogTaskType|Occurs when running a scheduled SharePoint backup.|
|SharePointExportAndImport|Occurs when a SharePoint item\-level recovery is performed.|
|StagingAreaRestore|Occurs when recovering files or applications from any folder that is located in a [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server to a protected computer.|

