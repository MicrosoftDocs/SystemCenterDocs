---
title: List Cloud Service
description: The List Cloud Service activity lists the cloud services available under the current subscription.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 83b9212b-1329-4ecd-aacf-8329001dd3ad
author: rayne-wiselman
ms.author: raynew
manager: carmonm
robots: noindex
---
# List Cloud Service

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The **List Cloud Service** activity lists the cloud services available under the current subscription. It is part of the **Azure Cloud Services** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## List Cloud Service required properties

There are no required properties for this runbook activity.

## List Cloud Service optional properties

There are no optional properties for this runbook activity.

## List Cloud Service published data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Service URL   | The Service Management API request URI used to perform requests against the cloud service.   | String   |
| Service DNS Prefix | The DNS prefix name of the Windows Azure cloud service.   | String   |
| Affinity Group   | The affinity group with which this cloud service is associated.   | String   |
| Location   | The geo-location specified when the cloud service was created. This property is only returned if the cloud service is not associated with an affinity group. | String   |
| Status   | The status of the storage account at the time the operation was called.   | String   |
| Date Created   | The date that the cloud service was created.   | Datetime   |
| Date Last Modified | The date that the cloud service was last updated.   | Datetime   |
| Label   | A friendly name for the cloud service.   | String   |
| Description   | A description for the cloud service.   | String   |
