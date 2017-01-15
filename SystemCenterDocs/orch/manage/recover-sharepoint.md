---
title: Recover SharePoint
description: The Recover SharePoint activity is used in a runbook that recovers a SharePoint farm (configuration and data) to its original location or to a network folder.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c551fe3-8577-4e26-93ad-caf3f1a8a912
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Recover SharePoint

Applies To: System Center 2016 - Orchestrator

The Recover SharePoint activity is used in a runbook that recovers a SharePoint farm (configuration and data) to its original location or to a network folder.

Be aware that the term Network Folder is used in this integration pack in the same way that it is used in the Data Protection Manager user interface. Choosing Network Folder recovers to a local path on a production server. Therefore, the selection of Network Folder requires the name of a production server and a local path on that production server.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Recover SharePoint Required Properties

| Element   | Sample value   |
|--------------------|------------------------------------------------------------------------------------|
| Data Source ID   | The unique identifier (GUID) of the SharePoint Farm to be recovered   |
| Recovery Type   | Recover to Original Instance, orRecover to Network Folder   |
| Recovery Source ID | The unique identifier (GUID) of the SharePoint Farm backup up point to be restored |

## Recover SharePoint Optional Properties

| Element   | Sample value   |
|--------------------|------------------------------------------------------------------------------------|
| Target Location   | The target location for the recoveryRequired when Recovery Type is Recover to Network Folder.   |
| Target Server Name | The name of the target server for the recovery Rrequired when Recovery Type is Recover to Network Folder. |

## Recover SharePoint Published Data

| Element   | Sample value   |
|--------------------|------------------------------------------------------------------------------------|
| DataSourceId   | The unique identifier (GUID) of the SharePoint Farm to be recovered   |
| EndTime   | The end time of the recovery, format as 0001-01-01T00:00:00   |
| JobCategory   | The job category   |
| JobDefinitionId   | The unique identifier (GUID) of the job definition   |
| JobId   | The unique identifier (GUID) of the job   |
| ProtectedGroupId   | The unique identifier (GUID) of the protection group   |
| RecoverySourceId   | The unique identifier (GUID) of the SharePoint Farm backup up to be restored   |
| RecoveryType   | Recover to Original Instance, Recover to Network Folder, or Recover to Original Server with DB Rename |
| RetryAttemptNumber | The number of recovery retries attempted   |
| StartTime   | The start time of the recovery, format as 0001-01-01T00:00:00   |
| Status   | Status   |
| TargetLocation   | The target location for the recovery   |
| TargetServer   | The name of the target server for the recovery   |
