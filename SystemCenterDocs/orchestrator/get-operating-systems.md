---
title: Get Operating Systems
description: The Get Operating Systems activity gets all Windows Azure operating systems.
ms.custom: UpdateFrequency3
ms.date: 04/27/2023
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99eae19a-b3e3-4188-82d6-6d25acb8abfe
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
monikerRange: '<=sc-orch-2019'
---

# Get Operating Systems

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The **Get Operating Systems** activity gets all Windows Azure operating systems. It's part of the **Azure Deployments** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Get Operating Systems Required Properties

There are no required properties for this runbook activity.

## Get Operating Systems Optional Properties

There are no optional properties for this runbook activity.

## Get Operating Systems Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Is Active   | Indicates whether this operating system version is currently active for running a service. If an operating system version is active, you can manually configure your service to run on that version.   | Boolean   |
| Is Default   | Indicates whether this operating system version is the default version for a service that has not otherwise specified a particular version. The default operating system version is applied to services that are configured for auto-upgrade. | Boolean   |
| Label   | The label of the operating system version.   | String   |
| OS Family Number  | The operating system family.   | Integer   |
| OS Version String | The operating system version.   | String   |
