---
title: Get DPM Server Capacity
description: The Get DPM Server Capacity activity is used in a runbook that queries a Data Protection Manager server for its available free storage capacity.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: be555ca0-71d1-4de6-ad5f-b1d2089ad958
author: rayne-wiselman
ms.author: raynew
manager: carmonm
---

# Get DPM Server Capacity

The Get DPM Server Capacity activity is used in a runbook that queries a Data Protection Manager server for its available free storage capacity. This information helps you determine the placement of backup data.

The Data Protection Manager server's storage pool returns capacity information in raw gigabytes (GB). For example, the value returned might be "120716263424". This data value requires additional calculation using standard activities such as Run .Net Script to perform real-world capacity checks. Typically, Data Protection Manager needs two to three times the storage space used by the primary data.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Get DPM Server Required Properties

| Element | Sample Value   |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------|
| Name   | The name of the Data Protection Manager connection to use for this activity, which also specifies the server to query for available capacity |

## Get DPM Server Published Data

| Element   | Sample Value   |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------|
| DPMServerName   | The name of the Data Protection Manager server queried   |
| TotalCapacityBytes   | The total capacity of the Data Protection Manager server in bytes   |
| TotalCapacityGB   | The total capacity of the Data Protection Manager server in GB   |
| UnallocatedSpaceBytes | The total amount of unallocated disk space on the Data Protection Manager server in bytes   |
| UnallocatedSpaceGB   | The total amount of unallocated disk space on the Data Protection Manager server in GB   |
| UsedSpaceBytes   | The total amount of currently used disk space on the Data Protection Manager server in bytes |
| UsedSpaceGB   | The total amount of currently used disk space on the Data Protection Manager server in GB   |
