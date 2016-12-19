---
title: Get Storage Account Keys
description: The Get Storage Account Keys activity returns the primary and secondary access keys for the specified storage account.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3d8d8e98-4d80-4a4e-af7f-07ab5e8d8d9c
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Get Storage Account Keys
========================

Applies To: System Center 2016 - Orchestrator

The **Get Storage Account Keys** activity returns the primary and secondary access keys for the specified storage account. It is part of the **Azure Storage** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

Get Storage Account Keys Required Properties
--------------------------------------------

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Storage Account Name | The name of the storage account. | String   |

Get Storage Account Keys Optional Properties
--------------------------------------------

There are no optional properties for this runbook activity.

Get Storage Account Keys Published Data
---------------------------------------

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Primary Key   | The primary access key for the storage account.   | String   |
| Secondary Key   | The secondary access key for the storage account. | String   |
| Storage Account Name | The name of the storage account.   | String   |

See Also
--------

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

