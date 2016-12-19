---
title: Regenerate Storage Account Key
description: The Regenerate Storage Account Key activity regenerates the primary or secondary access key for the specified storage account.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1483a1dd-43fb-446f-a7e6-a18f6760b7a6
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Regenerate Storage Account Key
==============================

Applies To: System Center 2016 - Orchestrator

The **Regenerate Storage Account Key** activity regenerates the primary or secondary access key for the specified storage account. It is part of the **Azure Storage** category activity.

| Note   |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Using this activity will publish the new storage account key to the Orchestrator databus. If you chose to use this activity, make sure to appropriately protect the key after regeneration. |

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

Regenerate Storage Account Key Required Properties
--------------------------------------------------

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Storage Account Name | The name of the storage account.   | String   |
| Key Type   | Specifies which key to regenerate. | Primary, Secondary |

Regenerate Storage Account Key Optional Properties
--------------------------------------------------

There are no optional properties for this runbook activity.

Regenerate Storage Account Key Published Data
---------------------------------------------

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Primary Key   | The primary access key for the storage account.   | String   |
| Secondary Key   | The secondary access key for the storage account. | String   |
| Storage Account Name | The name of the storage account.   | String   |

See Also
--------

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

