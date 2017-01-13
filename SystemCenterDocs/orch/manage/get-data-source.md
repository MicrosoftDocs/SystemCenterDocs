---
title: Get Data Source
description: The Get Data Source activity retrieves information about Data Sources from either a production server (a computer that has the Data Protection Manager Protection Agent installed) or from a protection group (a named entity that holds the backup policy for a workload).
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 36855461-0113-451b-86f9-e10656fd8b15
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Get Data Source

Applies To: System Center 2016 - Orchestrator

The Get Data Source activity retrieves information about Data Sources from either a production server (a computer that has the Data Protection Manager Protection Agent installed) or from a protection group (a named entity that holds the backup policy for a workload). A data source is a workload that is currently protected or will be protected by Data Protection Manager. When the Get Data Source activity is used in a protection scenario, you select a production server which becomes the default. When this activity is used in a recovery scenario, you will select a protection group or the production server. You then filter the list of data sources obtained using your own custom criteria that result in the data source(s) that you want to use in your runbook.

The common filters for this activity are as follows:

-   Name contains or matches a pattern
-   Protected - True or False

This activity returns the Data Source ID (DataSourceId) which is used in all activities except Get DPM Server Capacity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

<br><br><strong>Important </strong><br>The Protect Data Source activity does not support adding the FileSystem datasource type to a DPM Protection Group. If you need to protect file system datasources, you must use the Run DPM PowerShell Script activity to add FileSystem datasource types to a protection group.<br><br>

## Get Data Source Required Properties

|   |   |
|----------------------|-----------------------------------------------------------------------------------|
| Element   | Sample Value   |
| Data Source Location | Production Server or Protection Group   |
| Name   | The name of the target for this activity (computer name or protection group name) |

## Get Data Source Filters

|   |   |
|------------------------------------------|---------------------------------------------------------------------------|
| Element   | Sample Value   |
| ActivelyProtectedByDatasourceId   | 00000000-0000-0000-0000-000000000000   |
| CanDbFilesBeRecoveredToAlternateLocation | True or False   |
| CloudReplicaAllocationRequired   | True or False   |
| CurrentlyProtected   | True or False   |
| CustomFormatOption   | True or False   |
| DatasourceId   | 00000000-0000-0000-0000-000000000000   |
| DatasourceName   | String   |
| DatasourceSize   | 4907335680   |
| DiskAllocation   | String   |
| DisplayPath   | String   |
| FirstAddedTime   | Format as 0001-01-01T00:00:00   |
| Id   | 00000000-0000-0000-0000-000000000000   |
| InactiveDiskAllocation   | -   |
| Instance   | The instance is a ServerName or SharePointFarm.   |
| IsAutoCCEnabled   | True or False   |
| IsAutoGrowEnabled   | True or False   |
| IsBatchableOnSizeInquiry   | True or False   |
| IsCloudProtectable   | True or False   |
| IsCollocateable   | True or False   |
| IsCollocated   | True or False   |
| IsCustomAllocation   | True or False   |
| IsDiskInactive   | True or False   |
| IsDPMDatabase   | True or False   |
| IsDPMDatasource   | True or False   |
| IsExternalDatasource   | True or False   |
| IsInstanceProtected   | True or False   |
| IsLocalDPMDatabase   | True or False   |
| IsMirroredDatabase   | True or False   |
| IsOnlineInactive   | True or False   |
| IsOwnerOfAssociatedReplica   | True or False   |
| IsPresentOnCloud   | True or False   |
| IsReferentialDatasource   | True or False   |
| IsTapeInactive   | True or False   |
| LastAddedToCurrentPG   | Format as 0001-01-01T00:00:00   |
| LatestRecoveryAllowed   | True or False   |
| LatestRecoveryPoint   | Format as 0001-01-01T00:00:00   |
| LogicalPath   | SERVERNAME\\LogicalName   |
| MinimumReplicaSizeAllowed   | 4907335680   |
| MirroredServerInstance   | (String)   |
| MirroredServerName   | (String)   |
| Name   | (String)   |
| NeedsDiskAllocationModification   | True or False   |
| NumberOfExcludedObjects   | 0   |
| NumberOfProtectedObjects   | 1   |
| OldestRecoveryPoint   | Format as 0001-01-01T00:00:00   |
| OptimizedSize   | 4907335680   |
| OptimizedSizeOnDC   | 4907335680   |
| OptimizedSizeOnReplica   | 4907335680   |
| PrimaryDPMDatasourceId   | 00000000-0000-0000-0000-000000000000   |
| PrincipalServerInstance   | (String)   |
| PrincipalServerName   | (String)   |
| ProductionServerName   | SERVERNAME.Contoso.com   |
| Protected   | True or False   |
| ProtectedOnCloud   | True or False   |
| ProtectionGroupId   | 00000000-0000-0000-0000-000000000000   |
| ProtectionGroupName   | Protection Group 1   |
| ReAllocationRequired   | True or False   |
| RecoveryRangeInDays   | 5   |
| ReferentialDatasourceId   | 00000000-0000-0000-0000-000000000000   |
| ReferentialProtectionGroupId   | 00000000-0000-0000-0000-000000000000   |
| ReplicaAssociationChanged   | True or False   |
| ReplicaPath   | \\\\?\\Volume{ed7580eb-ff2e-11e0-806b-00155d027435}\\   |
| ReplicaResizeRequired   | True or False   |
| ReplicaSize   | 4907335680   |
| ReplicaUsedSpace   | 4907335680   |
| RequiredReplicaSize   | 4907335680   |
| RequiredShadowCopyAreaSize   | 4907335680   |
| ShadowCopyAreaSize   | 4907335680   |
| ShadowCopySizeAfterMaxShrink   | 4907335680   |
| ShadowCopySizeAfterMinShrink   | 4907335680   |
| ShadowCopyUsedSpace   | 4907335680   |
| SourceDPMServer   | (String)   |
| SqlScratchSpace   | (String)   |
| StopSQLServiceForRecovery   | True or False   |
| SupportsIncremental   | True or False   |
| TotalRecoveryPoints   | 0   |
| Type   | Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.SQL.SQLObjectType |
| UnderActiveProtectionFromDPM   | True or False   |
| UnderActiveProtectionFromPS   | True or False   |
| UsnJournalLogSize   | 4907335680   |
