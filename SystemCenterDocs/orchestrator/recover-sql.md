---
title: Recover SQL
description: The Recover SQL activity is used in a runbook that recovers a SQL database to its original location or to a network folder.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 03/04/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5ca6e7f3-d484-4311-a712-78daacfba9ba
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
robots: noindex
---
# Recover SQL

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The Recover SQL activity is used in a runbook that recovers a SQL database to its original location or to a network folder.

The term *Network Folder* is used in this integration pack in the same way that it's used in the Data Protection Manager user interface. Choosing Network Folder recovers to a local path on a production server. Therefore, the selection of Network Folder requires the name of a production server and a local path on that production server.

Also, recovery to any SQL Instance isn't a supported activity for this integration pack because Data Protection Manager doesn't support this scenario through its PowerShell API.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Recover SQL required properties

| Element   | Sample value   |
|--------------------|------------------------------------------------------------------------------------|
| Data Source ID   | The unique identifier (GUID) of the SQL database to be recovered   |
| Recovery Type   | Recover to Original Instance, or Recover to Network Folder   |
| Recovery Source ID | The unique identifier (GUID) of the SQL database backup up point to be restored |

## Recover SQL optional properties

| Element   | Sample value   |
|--------------------|------------------------------------------------------------------------------------|
| Copy Log Files   | True or False   |
| Database State   | Leave database operational or leave database non-operational but able to restore additional transaction logs   |
| Log File Copy Location | The location where the log files will be copied, if specified   |
| Restore Security   | Apply security settings of the destination computer or apply the security settings of the recovery point version |
| Target Location   | The target location for the recovery   |
| Target Server Name   | The name of the target server for the recovery   |

## Recover SQL published data

| Element   | Sample value   |
|--------------------|------------------------------------------------------------------------------------|
| EndTime   | The end time of the recovery, format as 0001-01-01T00:00:00   |
| JobCategory   | The job category   |
| JobDefinitionId   | The unique identifier (GUID) of the job definition   |
| JobID   | The unique identifier (GUID) of the job   |
| RetryAttemptNumber | The number of recovery retries attempted   |
| StartTime   | The start time of the recovery, format as 0001-01-01T00:00:00 |
| Status   | Status   |
