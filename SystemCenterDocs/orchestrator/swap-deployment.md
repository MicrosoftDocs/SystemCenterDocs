---
title: Swap Deployment
description: The Swap Deployment activity initiates a virtual IP swap between the staging and production deployment environments for a service.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: addb97e7-9815-4690-861e-3a2f6153f4d4
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Swap Deployment

The **Swap Deployment** activity initiates a virtual IP swap between the staging and production deployment environments for a service. It is part of the **Azure Deployments** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Swap Deployment Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Service DNS Prefix  | The DNS prefix name of the Windows Azure cloud service.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity. | True, False   |

## Swap Deployment Optional Properties

There are no optional properties for this runbook activity.

## Swap Deployment Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Request ID   | The unique identifier of the request to Windows Azure.   | String   |
| Service DNS Prefix  | The DNS prefix name of the Windows Azure cloud service.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity. | Boolean   |

## See Also


## Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

