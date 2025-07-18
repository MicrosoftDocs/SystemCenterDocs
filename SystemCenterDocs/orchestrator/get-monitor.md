---
title: Get Monitor
description: The Get Monitor activity is used in a runbook to retrieve monitoring activities from Operations Manager that match the criteria that you specify.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 04/07/2025
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 196b2938-3b17-4ab8-bfe9-3f5fb17ba159
author: jyothisuri
ms.author: jsuri
---

# Get Monitor

In this article, you will learn about Get Monitor activity. The Get Monitor activity is used in a runbook to retrieve monitoring activities from Operations Manager that match the criteria that you specify. For example, you can use the Get Monitor activity to retrieve a message and replicate the information to a trouble ticketing system.

The following tables list the filters, properties, and published data for this activity. The activity publishes all the data from the required and optional properties into published data.

## Get Monitor filters

The table list the elements data for this activity:

| Element   | Description   |
|-----------------------------|-----------------------------------------------------------------------------------------------------------|
| AvailabilityLastModified   | The date and time that the availability of the monitor was last changed.   |
| DisplayName   | The display name of the Operations Manager monitoring object.   |
| FullName   | The full name of the Operations Manager monitoring object.   |
| HealthState   | The current health state of the Operations Manager monitoring object.   |
| Id   | The unique ID of the Operations Manager monitoring object.   |
| InMaintenanceMode   | Indicates whether the Operations Manager monitoring object is in maintenance mode.   |
| IsAvailable   | Indicates whether the Operations Manager monitoring object is available to perform a monitoring operation. |
| LastModified   | The date and time that the Operations Manager monitoring object was last modified.   |
| MaintenanceModeLastModified | The date and time that the monitor maintenance mode was last changed.   |
| Name   | The name of the Operations Manager monitoring object.   |
| Path   | The path to the Operations Manager monitoring object.   |
| StateLastModified   | The date and time that the alert state was last changed.   |

## Get Monitor Published Data

The table list the elements data for this activity:

| Element   | Description   |
|---------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| AvailabilityLastModified   | The date and time that the availability of the monitor was last changed.   |
| Connection   | The connection string to the Operations Manager server that you're using.   |
| DisplayName   | The display name of the Operations Manager monitoring object.   |
| Domain   | The domain from which the alert came.   |
| FullName   | The full name of the Operations Manager monitoring object.   |
| HealthState   | The current health state of the Operations Manager monitoring object.   |
| Id   | The unique ID of the Operations Manager monitoring object.   |
| InMaintenanceMode   | Indicates whether the Operations Manager monitoring object is in maintenance mode.   |
| IsAvailable   | Indicates whether the Operations Manager monitoring object is available to perform a monitoring operation. |
| IsManaged   | Indicates whether the Operations Manager monitoring object is managed.   |
| LastModified   | The date and time that the Operations Manager monitoring object was last modified.   |
| LeastDerivedNonAbstractingMonitoringClassId | The globally unique ID for the least derived nonabstract monitoring class.   |
| MaintenanceModeLastModified   | The date and time that the monitor maintenance mode was last changed.   |
| ManagementGroup   | The Management Group to which the Operations Manager monitoring object belongs.   |
| ManagementGroupId   | The unique ID of the Management Group.   |
| MonitorCount   | The number of Operations Manager monitoring objects that met the filter criteria.   |
| Name   | The name of the Operations Manager monitoring object.   |
| Path   | The path to the Operations Manager monitoring object.   |
| Server   | The name of the Operations Manager server.   |
| StateLastModified   | The time that the alert state was last changed.   |
| Username   | The user name that was used to access the Operations Manager server.   |

