---
title: Delete Blob
description: The Delete Blob marks the specified blob or snapshot for deletion.
ms.custom: na
ms.date: 05/07/2019
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: d22e65e3-fc99-4dfa-aaf4-c8d2796e678d
author: rayne-wiselman
ms.author: raynew
manager: carmonm
robots: noindex
---
# Delete Blob

The **Delete Blob** marks the specified blob or snapshot for deletion. It is part of the **Azure Storage** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Delete Blob Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Storage Account Name | The name of the storage account. | String   |
| Container Name   | The name of the container.   | String   |
| Blob Name   | The name of the blob.   | String   |

## Delete Blob Optional Properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Primary Key | The primary key associated with the storage account. | String   |

## Delete Blob Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Storage Account Name | The name of the storage account. | String   |
| Container Name   | The name of the container.   | String   |
| Blob Name   | The name of the blob.   | String   |

## See Also

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
