---
title: Create Container
description: The Create Container activity creates a new container under the specified account.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: e58ceb1a-56fe-4675-95e5-a7f8187198ce
author: Jeronika-MS
ms.author: v-gajeronika
monikerRange: '<=sc-orch-2019'
---
# Create Container

The **Create Container** activity creates a new container under the specified account. It's part of the **Azure Storage** category activity.

>[!NOTE]
>Currently, this activity won't fail if a container already exists with the same name as the container to create. No new container will be created, but the activity will succeed in Orchestrator.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Create Container Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Storage Account Name | The name of the storage account. | String   |
| Container Name   | A name for the container.   | String   |

## Create Container Optional Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Primary Key   | The primary key associated with the storage account.   | String   |
| Metadata   | Metadata to associate with the container. Should be in the format "Name1:Value1,Name2:Value2" | String   |
| Public Access Level | Specifies whether data in the container may be accessed publicly and the level of access.   | Off, Container, Blob |

## Create Container Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Container Name   | The name of the container.   | String   |
| Container Url   | The absolute URI to the container.   | String   |
| ETag   | The entity tag for the container.   | String   |
| Last Modified Time (UTC) | Returns the date and time the container was last modified.   | Datetime   |
| Metadata   | Metadata associated with the container in the format "Name1:Value1,Name2:Value2"   | String   |
| Public Access Level   | Specifies whether data in the container may be accessed publicly and the level of access. | String   |
| Storage Account Name   | The name of the storage account.   | String   |

## See Also

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
