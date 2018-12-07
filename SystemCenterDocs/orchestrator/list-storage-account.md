---
title: List Storage Account
description: The List Storage Account activity lists the storage accounts available under the current subscription.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 919aaeea-c0f3-43a9-a772-beabd4d9d209
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# List Storage Account

The **List Storage Account** activity lists the storage accounts available under the current subscription. It is part of the **Azure Storage** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

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
| Location   | The geo-location specified when the storage account was created. This property is only returned if the storage account is not associated with an affinity group. | String   |
| Storage Account Name | The name of the storage account.   | String   |
| Service URL   | The Service Management API request URI used to perform requests against the storage account.   | String   |
| Status   | The status of the storage account at the time the operation was called.   | String   |
