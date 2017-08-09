---
title: Create Recovery Point
description: The Create Recovery Point activity is used to create a backup for a selected data source.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 178651bc-0edb-4046-8b64-4bbb2998408f
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Create Recovery Point

Applies To: System Center 2016 - Orchestrator

The Create Recovery Point activity is used to create a backup for a selected data source. This activity allows you to create a recovery point outside the Data Protection Manager scheduled interval as configured for a protection group. This activity can also be used to force creation of an initial replica. For more information, see Protect Data Source.

The behavior is synchronous - the activity will run for as long it takes for Data Protection Manager to complete the action.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Create Recovery Point Required Properties

| Element   | Sample Value   |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| DataSourceID | The unique identifier (GUID) of the data source for the recovery point. This ID can be obtained using the Get Data Source activity prior to this activity in the runbook and subscribing to the DataSourceId property in published data. |

## Create Recovery Point Published Data


| Element              | Sample Value   |
|-----------|-----------------------|
| AllMediaCatalogued   | True or False   |
| ComponentName   | The component name   |
| ComponentType   | The component type   |
| DataSourceID   | The unique identifier (GUID) of the data source for the recovery point   |
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
| RecoverableObjectID   | The identifier (integer) of the object that is eligible for recovery   |
| RecoverySourceID   | The unique identifier (GUID) of the source object for the recovery   |
| ReferentialRecoverySourceID   | The unique identifier (GUID) of the Referential Recovery Source   |
| RepresentedPointInTime   | The date and time of the represented point in time, in the format 0001-01-01T00:00:00   |
| ROCatalogStatus   | RO Catalog Status   |
| Size   | Size   |
| SupportsAlternateLocationRecovery | True or False   |
| UserFriendlyName   | The friendly name   |
| UtcRepresentedPointInTime   | The universal coordinated time of the represented point in time, format as 0001-01-01T00:00:00 |
| WriterID   | The unique identifier (GUID) for the writer   |
