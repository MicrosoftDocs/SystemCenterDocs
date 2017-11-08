---
title: Create Affinity Group
description: The Create Affinity Group activity creates a new affinity group for the specified subscription.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: c361dda5-c55c-4743-8053-1bdf57667fa3
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Create Affinity Group

The **Create Affinity Group** activity creates a new affinity group for the specified subscription. It is part of the **Azure Cloud Services** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Create Affinity Group Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Affinity Group Name | A name for the affinity group that is unique to the subscription.  | String   |
| Label   | A friendly name for the affinity group.   | String   |
| Description   | A description for the affinity group.   | String   |
| Location   | The data center location where the affinity group will be created. | String   |

## Create Affinity Group Optional Properties

There are no optional properties for this runbook activity.

## Create Affinity Group Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Affinity Group Name | A name for the affinity group that is unique to the subscription.  | String   |
| Label   | A friendly name for the affinity group.   | String   |
| Description   | A description for the affinity group.   | String   |
| Location   | The data center location where the affinity group will be created. | String   |

## See Also

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
