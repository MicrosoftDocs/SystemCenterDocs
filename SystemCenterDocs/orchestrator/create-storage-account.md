---
title: Create Storage Account
description: The Create Storage Account activity creates a new storage account in Azure.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 365-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: d77c39e2-e0bb-4259-8072-803361ad4211
author: Jeronika-MS
ms.author: v-gajeronika
monikerRange: '<=sc-orch-2019'
---
# Create Storage Account

The **Create Storage Account** activity creates a new storage account in Azure. It's part of the **Azure Storage** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Create Storage Account Required Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Storage Account Name   | A name for the storage account that is unique within Azure.   | String   |
| Label   | A label for the storage account.   | String   |
| Description   | A description for the storage account.   | String   |
| Location/Affinity Group   | Whether to create the storage account in a certain location or affinity group.   | Location, Affinity Group |
| Location/Affinity Group Value | The location where the storage account will be created, or the name of an existing affinity group associated with the subscription. | String   |
| Wait for Completion   | Whether to wait for this operation to complete in Azure before moving on to the next activity.   | True, False   |

## Create Storage Account Optional Properties

There are no optional properties for this runbook activity.

## Create Storage Account Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Storage Account Name   | A name for the storage account that is unique within Azure.   | String   |
| Label   | A label for the storage account.   | String   |
| Description   | A description for the storage account.   | String   |
| Location/Affinity Group   | Whether to create the storage account in a certain location or affinity group.   | String   |
| Location/Affinity Group Value | The location where the storage account will be created, or the name of an existing affinity group associated with the subscription. | String   |
| Wait for Completion   | Whether to wait for this operation to complete in Azure before moving on to the next activity.   | Boolean   |
| Request ID   | The unique identifier of the request to Azure.   | String   |

## See Also

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
