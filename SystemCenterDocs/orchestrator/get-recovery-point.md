---
title: Get Recovery Point
description: The Get Recovery Point activity is used in a runbook that queries a data source for all its associated recovery points or only the most recent recovery point.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 2cddc23c-c3b6-4cd7-be8c-446fb557e24b
author: cfreemanwa
ms.author: raynew
manager: carmonm
---

# Get Recovery Point

Applies To: System Center 2016 - Orchestrator

The Get Recovery Point activity is used in a runbook that queries a data source for all its associated recovery points or only the most recent recovery point.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Get Recovery Point Required Properties

| Element   | Sample Value   |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Selection   | Options are:Latest- the most recent recovery point associated with the data sourceAll - a list of all the data points associated with the data source (can return multiple values) |
| Data Source ID | The unique identifier (GUID) of the data source for the recovery point, which can be obtained via the Get Data Source activity.   |

## Get Recovery Point Filters

| Element   | Sample Value   |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AllMediaCatalogued   | True or False   |
| ComponentName   | The component name   |
| ComponentType   | The component type   |
| DestinationForAlternateRecovery   | The alternate recovery destination   |
| DestinationForRestore   | The destination for the restore   |
| HasFastRecoveryMarker   | True or False   |
| IsIncremental   | True or False   |
| InOnlineRecatalogueNeeded   | True or False   |
| IsRecoverable   | True or False   |
| IsValidForSearchResult   | True or False   |
| IsValidRecoverySource   | True or False   |
| Logical Path   | The logical path   |
| ParentName   | The parent name   |
| RecoverableObjectID   | The unique identifier (GUID) of the object that is eligible for recovery   |
| RecoverySourceID   | The unique identifier (GUID) of the source object for the recovery   |
| ReferentialRecoverySourceID   | The unique identifier (GUID) of the Referential Recovery Source   |
| RepresentedPointInTime   | The date and time of the represented point in time, in the format as 0001-01-01T00:00:00 |
| ROCatalogStatus   | RO Catalog Status   |
| Size   | Size   |
| SupportsAlternateLocationRecovery | True or False   |
| UserFriendlyName   | The friendly name   |
| UtcRepresentedPointInTime   | The universal coordinated time of the represented point in time   |
| WriterID   | The unique identifier (GUID) for the writer   |

## Get Recovery Point Published Data

| Element   | Sample Value   |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AllMediaCatalogued   | True or False   |
| ComponentName   | The component name   |
| ComponentType   | The component type   |
| DataSourceID   | The unique identifier (GUID) of the data source for the recovery point   |
| DestinationForAlternateRecovery   | The destination for alternate recovery   |
| DestinationForRestore   | The destination for the restore   |
| HasFastRecoveryMarker   | True or False   |
| IsIncremental   | True or False   |
| InOnlineRecatalogueNeeded   | True or False   |
| IsRecoverable   | True or False   |
| IsValidForSearchResult   | True or False   |
| IsValidRecoverySource   | True or False   |
| Logical Path   | The logical path   |
| ParentName   | The parent name   |
| RecoverableObjectID   | The unique identifier (GUID) of the object that is eligible for recovery   |
| RecoverySourceID   | The unique identifier (GUID) of the source object for the recovery   |
| ReferentialRecoverySourceID   | The unique identifier (GUID) of the Referential Recovery Source   |
| RepresentedPointInTime   | The date and time of the represented point in time, format as 0001-01-01T00:00:00 |
| ROCatalogStatus   | RO Catalog Status   |
| Selection   | Latest or All   |
| Size   | Size   |
| SupportsAlternateLocationRecovery | True or False   |
| UserFriendlyName   | The friendly name   |
| UtcRepresentedPointInTime   | The universal coordinated time of the represented point in time   |
| WriterID   | The unique identifier (GUID) for the writer   |
