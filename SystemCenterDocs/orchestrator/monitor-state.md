---
title: Monitor State
description: The Monitor State activity monitors the state of an Operations Manager object that you specify.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/09/2023
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47d10330-5980-44f7-a11c-23cc04636ddc
author: jyothisuri
ms.author: jsuri
manager: mkluck
robots: noindex
---
# Monitor State

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The Monitor State activity monitors the state of an Operations Manager object that you specify. For example, you can use the Monitor State activity to trigger a corrective runbook when an object with a Warning or Critical state is detected.

The following tables list the properties and published data for this activity. The activity publishes all the data from the properties into published data.

## Monitor State required properties

| Element   | Description   | Valid Values   | Lookup |
|:---|:---|:---|:---|
| Connection | The connection string to the Operations Manager server that you're using | String   | Yes   |
| Object   | The name of the Operations Manager object to be monitored   | String   | Yes   |
| State   | The health state of the Operations Manager monitoring object   | CriticalHealthyUninitializedWarning | Yes   |

## Monitor State published data

| Element   | Description   |
|-------------------|---------------------------------------------------------------|
| AvailabilityLastModified   | The last date and time that the availability of the monitor was changed   |
| Connection   | The connection string to the Operations Manager server that you're using   |
| DisplayName   | The display name of the Operations Manager monitoring object   |
| Domain   | The domain that the alert came from   |
| FullName   | The full name of the Operations Manager monitoring object   |
| HealthState   | The current health state of the Operations Manager monitoring object   |
| Id   | The unique ID of the Operations Manager monitoring object   |
| InMaintenanceMode   | Indicates whether the Operations Manager monitoring object is in maintenance mode   |
| IsAvailable   | Indicates whether the Operations Manager monitoring object is available to perform a monitoring operation |
| IsManaged   | Indicates whether the Operations Manager monitoring object is managed   |
| LastModified   | The date and time that the Operations Manager monitoring object was last modified   |
| LeastDerivedNonAbstractingMonitoringClassId | The globally unique ID for the least derived non-abstract monitoring class   |
| MaintenanceModeLastModified   | The date and time that the maintenance mode was last changed   |
| ManagementGroup   | The Management Group that the Operations Manager monitoring object belongs to   |
| ManagementGroupId   | The unique ID of the Management Group   |
| Name   | The name of the Operations Manager monitoring object   |
| Path   | The path to the Operations Manager monitoring object   |
| Server   | The name of the Operations Manager server   |
| StateLastModified   | The date and time that the Operations Manager monitoring object state was last changed   |
| Username   | The username that was used to access the Operations Manager server   |
