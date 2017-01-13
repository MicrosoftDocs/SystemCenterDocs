---
title: Recover VM
description: The Recover VM activity is used in a runbook that recovers a virtual machine from a specified point in time so that it can be restored to a server running Hyper-V or to a network folder.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5045f61c-65e8-4b45-a3d2-b4d87aab8384
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Recover VM

Applies To: System Center 2016 - Orchestrator

The Recover VM activity is used in a runbook that recovers a virtual machine from a specified point in time so that it can be restored to a server running Hyper-V or to a network folder.

Be aware that the term Network Folder is used in this integration pack in the same way that it is used in the Data Protection Manager user interface. Choosing Network Folder recovers to a local path on a production server. Therefore, the selection of Network Folder requires the name of a production server and a local path on that production server.

For example, you can use the Get Data Source activity to obtain the target virtual machine object so that it can be recovered. You can then use the Get Recovery Point activity to obtain the protected virtual machine's backup to be restored. Finally, the Recover VM activity can be used to recover the virtual machine to the specified server running Hyper-V, an alternate server running Hyper-V (as a disaster recovery scenario), or the cluster.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Recover VM Required Properties

|   |   |
|--------------------|--------------------------------------------------------------------------------------|
| Element   | Sample value   |
| Data Source ID   | The unique identifier (GUID) of the virtual machine to be recovered   |
| Recovery Type   | Recover to Original Instance, or Recover to Network Folder   |
| Recovery Source ID | The unique identifier (GUID) of the virtual machine's backup up point to be restored |

## Recover VM Optional Properties

|   |   |
|--------------------|------------------------------------------------|
| Element   | Sample value   |
| Target Location   | The target location for the recovery   |
| Target Server Name | The name of the target server for the recovery |

## Recover VM Published Data

|   |   |
|--------------------|---------------------------------------------------------------|
| Element   | Sample value   |
| EndTime   | The end time of the recovery, format as 0001-01-01T00:00:00   |
| JobCategory   | The job category   |
| JobDefinitionId   | The unique identifier (GUID) of the job definition   |
| JobID   | The unique identifier (GUID) of the job   |
| ProtectedGroupID   | The unique identifier (GUID) of the protection group   |
| RetryAttemptNumber | The number of recovery retries attempted   |
| StartTime   | The start time of the recovery, format as 0001-01-01T00:00:00 |
| Status   | Status   |
