---
title: List Storage Account
description: The List Storage Account activity lists the storage accounts available under the current subscription.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 919aaeea-c0f3-43a9-a772-beabd4d9d209
author: Jeronika-MS
ms.author: v-gajeronika
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# List Storage Account

The **List Storage Account** activity lists the storage accounts available under the current subscription. It's part of the **Azure Storage** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## List Storage Account required properties

There are no required properties for this runbook activity.

## List Storage Account optional properties

There are no optional properties for this runbook activity.

## List Storage Account published data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Affinity Group   | The affinity group with which this storage account is associated.   | String   |
| Description   | A description for the storage account.   | String   |
| Label   | A label for the storage account.   | String   |
| Location   | The geo-location specified when the storage account was created. This property is only returned if the storage account isn't associated with an affinity group. | String   |
| Storage Account Name | The name of the storage account.   | String   |
| Service URL   | The Service Management API request URI used to perform requests against the storage account.   | String   |
| Status   | The status of the storage account at the time the operation was called.   | String   |
