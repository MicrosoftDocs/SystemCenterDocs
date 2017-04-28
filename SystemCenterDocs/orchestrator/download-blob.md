---
title: Download Blob
description: The Download Blob activity downloads a blob from the system.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: a6e1b38f-d31a-45da-9f00-dc1ee232da42
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
---

# Download Blob

Applies To: System Center 2016 - Orchestrator

The **Download Blob** activity downloads a blob from the system. It is part of the **Azure Storage** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Download Blob Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Storage Account Name  | The name of the storage account.   | String   |
| Container Name   | The name of the container.   | String   |
| Blob Name   | The name of the blob.   | String   |
| Download to File Path | The location to save the downloaded blob. | String   |

## Download Blob Optional Properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Primary Key | The primary key associated with the storage account. | String   |

## Download Blob Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Storage Account Name  | The name of the storage account.   | String   |
| Container Name   | The name of the container.   | String   |
| Blob Name   | The name of the blob.   | String   |
| Download to File Path | The location to save the downloaded blob. | String   |
