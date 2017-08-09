---
title: Check Cloud Service Name Availability
description: The Check Cloud Service Name Availability activity checks to see if the specified cloud service name is available, or if it has already been taken.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: b4f862ca-5918-4f0a-9031-973cce272d68
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Check Cloud Service Name Availability

Applies To: System Center 2016 - Orchestrator

The **Check Cloud Service Name Availability** activity checks to see if the specified cloud service name is available, or if it has already been taken. It is part of the **Azure Cloud Services** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Check Cloud Service Name Availability Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Desired DNS Prefix | The DNS prefix name to check for availability. | String   |

## Check Cloud Service Name Availability Optional Properties

There are no optional properties for this runbook activity.

## Check Cloud Service Name Availability Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Desired DNS Prefix | The DNS prefix name to check for availability. | String   |
| Name Available   | Whether the DNS prefix is available.   | Boolean   |

## See Also

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
