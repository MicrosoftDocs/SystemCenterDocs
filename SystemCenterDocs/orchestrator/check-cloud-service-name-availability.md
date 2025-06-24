---
title: Check Cloud Service Name Availability
description: The Check Cloud Service Name Availability activity checks to see if the specified cloud service name is available, or if it has already been taken.
ms.custom: UpdateFrequency2
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: b4f862ca-5918-4f0a-9031-973cce272d68
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
---
# Check Cloud Service Name Availability

The **Check Cloud Service Name Availability** activity checks to see if the specified cloud service name is available, or if it has already been taken. It's part of the **Azure Cloud Services** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

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

## Next steps

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
