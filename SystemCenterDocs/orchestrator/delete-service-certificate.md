---
title: Delete Service Certificate
description: The Delete Service Certificate activity is used in a runbook to delete a service certificate from the certificate store of a cloud service.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: f6aeb60a-85bb-49ea-9fd3-ca8704ce7225
author: jyothisuri
ms.author: jsuri
monikerRange: '<=sc-orch-2019'
---

# Delete Service Certificate

The **Delete Service Certificate** activity is used in a runbook to delete a service certificate from the certificate store of a cloud service. It's part of the **Azure Certificates** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

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

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
