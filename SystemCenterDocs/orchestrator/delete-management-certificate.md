---
title: Delete Management Certificate
description: The Delete Management Certificate activity is used in a runbook to delete a certificate from the list of management certificates.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 653f1f13-751b-48aa-b5aa-ad3ac5ddbaa8
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
---
# Delete Management Certificate

The **Delete Management Certificate** activity is used in a runbook to delete a certificate from the list of management certificates. It's part of the **Azure Certificates** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Delete Management Certificate Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Certificate File Path | The path to the management certificate file. | String   |
| Certificate File Type | The type of the management certificate file. | CER, PFX   |

## Delete Management Certificate Optional Properties

There are no optional properties for this runbook activity.

## Delete Management Certificate Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Request ID   | The unique identifier of the request to Azure. | String   |
| Certificate File Path | The path to the management certificate file.   | String   |
| Certificate File Type | The type of the management certificate file.   | String   |

## See Also

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
