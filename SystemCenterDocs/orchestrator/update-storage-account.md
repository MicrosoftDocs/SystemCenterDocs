---
title: Update Storage Account
description: The Update Storage Account activity updates the label, the description, and enables or disables the geo-replication status for a storage account in Windows Azure.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: cd7df37b-59f1-4e8f-ae04-7008c2806618
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Update Storage Account

Applies To: System Center 2016 - Orchestrator

The **Update Storage Account** activity updates the label, the description, and enables or disables the geo-replication status for a storage account in Windows Azure. It is part of the **Azure Storage** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

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
| Request ID   | The unique identifier of the request to Windows Azure.   | String   |

## See Also


## Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

