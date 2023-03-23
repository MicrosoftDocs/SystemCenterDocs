---
title: Update User Role Quota
description: Updates the quotas for a certain user role and cloud.
ms.custom: UpdateFrequency3
ms.date: 12/02/2016
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 253dbe66-1fdd-4160-a664-0cf34e712e03
author: jyothisuri
ms.author: jsuri
manager: mkluck
robots: noindex
---
# Update User Role Quota

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

Updates the quotas for a certain user role and cloud.

## Update User Role Quota Required Properties

| Element   | Description   
|:---|:---|
| User Role Name | The user role name to update   |   
| Cloud Name   | The name of the cloud to which the quota applies |   
| Level   | The level of the user role quota   |   

## Update User Role Quota Optional Properties

| Element   | Description   |
|:---|:---|
| Max Custom Quota   | Enter maximum value for custom property |   
| Max Memory in MBs  | Maximum memory   |   
| Max Storage in GBs | Maximum storage space   |   
| Max Virtual CPUs   | Maximum number of virtual CPUs   |   
| Max VMs   | Maximum number of virtual machines   |   

## Update User Role Quota Published Data

| Element   | Description   |
|:---|:---|
| Cloud Name   | The name of the cloud to which the quota applies |   
| Level   | The level of the user role quota   |   
| Max Virtual CPUs   | Maximum number of virtual CPUs   |   
| Max VMs   | Maximum number of virtual machines   |   
| Max Memory in MBs  | Maximum memory   |   
| Max Storage in GBs | Maximum storage space   |   
| Max Custom   |   |
