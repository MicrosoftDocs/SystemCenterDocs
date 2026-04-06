---
title: Update Storage Account
description: The Update Storage Account activity updates the label, the description, and enables or disables the geo-replication status for a storage account in Microsoft Azure.
ms.custom: engagement-fy23, UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: cd7df37b-59f1-4e8f-ae04-7008c2806618
author: Jeronika-MS
ms.author: v-gajeronika
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# Update Storage Account

The **Update Storage Account** activity updates the label, the description, and enables or disables the geo-replication status for a storage account in Microsoft Azure. It's part of the **Azure Storage** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Update Storage Account Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Storage Account Name   | The name of the storage account.   | String   |
| Label   | A label for the storage account.   | String   |
| Description   | A description for the storage account.   | String   |
| Geographic Replication Enabled | Enables or disables geo-replication on the specified storage account. | True, False   |

## Update Storage Account Optional Properties

There are no optional properties for this runbook activity.

## Update Storage Account Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Storage Account Name   | The name of the storage account.   | String   |
| Label   | A label for the storage account.   | String   |
| Description   | A description for the storage account.   | String   |
| Geographic Replication Enabled | Enables or disables geo-replication on the specified storage account. | Boolean   |
| Request ID   | The unique identifier of the request to Microsoft Azure.   | String   |

## Other Resources

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
