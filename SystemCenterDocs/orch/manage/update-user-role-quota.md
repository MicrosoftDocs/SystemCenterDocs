---
title: Update User Role Quota
description: Updates the quotas for a certain user role and cloud.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 253dbe66-1fdd-4160-a664-0cf34e712e03
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Update User Role Quota

Applies To: System Center 2016 - Orchestrator

Updates the quotas for a certain user role and cloud.

Updates User Role Quota Required Properties
---
# ----------------------------------------

| Element   | Description   | Valid Values |
|:---|:---|:---|
| User Role Name | The user role name to update   |   |
| Cloud Name   | The name of the cloud to which the quota 
Applies |   |
| Level   | The level of the user role quota   |   |

## Updates User Role Quota Optional Properties

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Max Custom Quota   | Enter maximum value for custom property. |   |
| Max Memory in MBs  | Maximum memory   |   |
| Max Storage in GBs | Maximum storage space   |   |
| Max Virtual CPUs   | Maximum number of virtual CPUs   |   |
| Max VMs   | Maximum number of virtual machiens   |   |

Updates User Role Quota Published Data
---
# -----------------------------------

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Cloud Name   | The name of the cloud to which the quota 
Applies |   |
| Level   | The level of the user role quota   |   |
| Max Virtual CPUs   | Maximum number of virtual CPUs   |   |
| Max VMs   | Maximum number of virtual machiens   |   |
| Max Memory in MBs  | Maximum memory   |   |
| Max Storage in GBs | Maximum storage space   |   |
| Max Custom   |   |   |
