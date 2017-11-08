---
title: Move Or Copy Item
description: The Move Or Copy Item activity is used in a runbook to move or copy an item to another folder.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 3cd9da10-0931-4029-b313-7860eda9ba27
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Move Or Copy Item

The Move Or Copy Item activity is used in a runbook to move or copy an item to another folder. This activity supports all item types.

The following tables list the required properties and published data for this activity.

## Move Or Copy Item required properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| ID   | The ID of the item to be moved or copied   | String   |
| Copy   | Indicates whether the item is to be copied to the new location | True<br>False   |
| Destination Folder | The folder that the item will be moved to   | String   |

## Move Or Copy Item published data

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| ID   | The new ID of the item that is moved or copied   | String   |
| Copy   | Indicates whether the item is to be copied to the new location  | Boolean   |
| Destination Folder   | The folder that the item will be moved to   | String   |
| Domain   | The domain that the Exchange server belongs to   | String   |
| Exchange Server Address | The address of the Exchange server   | String   |
| Timeout (seconds)   | Connection timeout threshold   | Number   |
| Use Autodiscover   | Indicates whether or not the Autodiscover service is being used | Boolean   |
| User Name   | User name to be used to connect to Exchange server   | String   |
