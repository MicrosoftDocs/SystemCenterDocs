---
title: Monitoring recovery jobs
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 62005362-fe4e-4e2d-aa83-eeeae12becab
---
# Monitoring recovery jobs
You can use the DPM Self\-Service Recovery Tool \(SSRT\) console to monitor recovery jobs for SQL Server databases configured by your DPM administrator.

## Viewing recovery job status
Recovery jobs for SQL Server databases are displayed in the **Jobs** list view in the DPM SSRT console. The following table provides the possible types of recovery job status that you might see in the **Jobs** list view in the DPM SSRT console.

|**Recovery Job Status**|**Description**|
|---------------------------|-------------------|
|**In Progress**|The recovery job is still in progress. For more information about the recovery job in progress, double\-click the recovery job.|
|**Completed**|The recovery job was completed successfully.|
|**Failed**|The recovery job was canceled or failed.|

To find operational details such as **Status description**, **elapsed time**, and  **data transferred** for any recovery job, double\-click the recovery job.

## Rerunning a failed recovery job
You can rerun a failed recovery job from the DPM SSRT console. To rerun a failed recovery job, select the recovery job and then click **Rerun**.

> [!NOTE]
> To be able to rerun a recovery job started by a different user, you must have permission both to recover the database and to recover to the location it was being recovered to. If you do not have these permissions, you cannot rerun the recovery job.

## Stopping a recovery job
To stop a recovery job that is in progress, select the recovery job and then click **Stop**.

