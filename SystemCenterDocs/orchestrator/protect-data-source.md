---
title: Protect Data Source
description: The Protect Data Source activity is used to protect a workload by adding a data source to an existing protection group.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/09/2023
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: acf1e7a8-72d6-4d46-be36-830d0e6c6a37
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
robots: noindex
---
# Protect Data Source

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The Protect Data Source activity is used to protect a workload by adding a data source to an existing protection group. A protection group is a named entity that holds the backup policy for a workload.

>[!IMPORTANT]
>We recommend that protection groups contain only data sources of the same type.

The following items apply to the Replica Creation Method for this release:

-   The Replica Creation Method value of Now isn't supported in this release of the integration pack because Data Protection Manager has no reliable way to determine the progress and status of replica creation, other than in the user interface.
-   If you select the Replica Creation Method value of Later, the optional property Replica Creation Time is a required property.
-   If you select the Replica Creation Method value of Manual, the replica creation can be forced by using the Create Recovery Point activity. The Data Protection Manager user interface will display this as a consistency check job.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Protect Data Source required properties

| Element   | Sample value   |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| Replica Creation Method | Later or Manual   |
| Data Source ID   | The unique identifier (GUID) of the data source for the recovery point, which can be obtained via the Get Data Source activity |
| Protection Group   | The name of the protection group to which the workload will be added   |
| Replica Creation Time   | The date and time of the replica creation, Format as 0001-01-01T00:00:00. Required if Replica Creation method is set to Later. |

## Protect Data Source published data

| Element   | Sample value   |
|------------------|--------------------------------------------------------------------------|
| DataSourceID   | The unique identifier (GUID) of the data source for the recovery point   |
| Protection Group | The name of the protection group to which to add the workload   |
| Replication Time | The date and time of the replica creation, format as 0001-01-01T00:00:00 |
| Replication Type | The replication type   |
