---
title: Recover SQL
description: The Recover SQL activity is used in a runbook that recovers a SQL database to its original location or to a network folder.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5ca6e7f3-d484-4311-a712-78daacfba9ba
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Recover SQL

Applies To: System Center 2016 - Orchestrator

The Recover SQL activity is used in a runbook that recovers a SQL database to its original location or to a network folder.

Be aware that the term Network Folder is used in this integration pack in the same way that it is used in the Data Protection Manager user interface. Choosing Network Folder recovers to a local path on a production server. Therefore, the selection of Network Folder requires the name of a production server and a local path on that production server.

Also be aware that recovery to any SQL Instance is not a supported activity for this integration pack because Data Protection Manager does not support this scenario through its PowerShell API.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Recover SQL Required Properties

|   |   |
|--------------------|---------------------------------------------------------------------------------|
| Element   | Sample value   |
| Data Source ID   | The unique identifier (GUID) of the SQL database to be recovered   |
| Recovery Type   | Recover to Original Instance, or Recover to Network Folder   |
| Recovery Source ID | The unique identifier (GUID) of the SQL database backup up point to be restored |

## Recover SQL Optional Properties

|   |   |
|------------------------|------------------------------------------------------------------------------------------------------------------|
| Element   | Sample value   |
| Copy Log Files   | True or False   |
| Database State   | Leave database operational or leave database non-operational but able to restore additional transaction logs   |
| Log File Copy Location | The location where the log files will be copied, if specified   |
| Restore Security   | Apply security settings of the destination computer or apply the security settings of the recovery point version |
| Target Location   | The target location for the recovery   |
| Target Server Name   | The name of the target server for the recovery   |

## Recover SQL Published Data

|   |   |
|--------------------|---------------------------------------------------------------|
| Element   | Sample value   |
| EndTime   | The end time of the recovery, format as 0001-01-01T00:00:00   |
| JobCategory   | The job category   |
| JobDefinitionId   | The unique identifier (GUID) of the job definition   |
| JobID   | The unique identifier (GUID) of the job   |
| RetryAttemptNumber | The number of recovery retries attempted   |
| StartTime   | The start time of the recovery, format as 0001-01-01T00:00:00 |
| Status   | Status   |
