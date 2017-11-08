---
title: Create Container
description: The Create Container activity creates a new container under the specified account.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: e58ceb1a-56fe-4675-95e5-a7f8187198ce
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Create Container

The **Create Container** activity creates a new container under the specified account. It is part of the **Azure Storage** category activity.

>[!NOTE]
>Currently, this activity will not fail if a container already exists with the same name as the container to create. No new container will be created, but the activity will succeed in Orchestrator.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

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

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
