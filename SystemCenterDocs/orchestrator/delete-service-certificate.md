---
title: Delete Service Certificate
description: The Delete Service Certificate activity is used in a runbook delete a service certificate from the certificate store of a cloud service.
ms.custom: na
ms.date: 05/07/2019
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: f6aeb60a-85bb-49ea-9fd3-ca8704ce7225
author: rayne-wiselman
ms.author: raynew
manager: carmonm
robots: noindex
---
# Delete Service Certificate

The **Delete Service Certificate** activity is used in a runbook delete a service certificate from the certificate store of a cloud service. It is part of the **Azure Certificates** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Delete Service Certificate Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Certificate File Path | The path to the certificate file.   | String   |
| Service Name   | The name of the Azure cloud service. | String   |
| PFX Password   | The type of the management certificate file. | CER, PFX   |

## Delete Service Certificate Optional Properties

There are no optional properties for this runbook activity.

## Delete Service Certificate Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Request ID   | The unique identifier of the request to Azure. | String   |
| Certificate File Path | The path to the certificate file.   | String   |
| Service Name   | The name of the Azure cloud service.   | String   |

## See Also

[Using Runbooks in System Center - Orchestrator](https://technet.microsoft.com/library/hh403791.aspx)
