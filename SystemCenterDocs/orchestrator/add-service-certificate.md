---
title: Add Service Certificate
description: The Add Service Certificate activity is used in a runbook to add a certificate to a cloud service.
ms.custom: UpdateFrequency2
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 5c12e8ec-fdc2-40c9-b217-5f598f9b93ad
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
---
# Add Service Certificate

The **Add Service Certificate** activity is used in a runbook to add a certificate to a cloud service. It's part of the **Azure Certificates** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Add Service Certificate Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Certificate File Path | The path to the certificate file.   | String   |
| Service Name   | The name of the Windows Azure cloud service. | String   |
| PFX File Password   | The certificate password.   | String   |

## Add Service Certificate Optional Properties

There are no optional properties for this runbook activity.

## Add Service Certificate Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Request ID   | The unique identifier of the request to Windows Azure. | String   |
| Certificate File Path | The path to the certificate file.   | String   |
| Service Name   | The name of the Windows Azure cloud service.   | String   |

## Next steps

[Using Runbooks in System Center 2016 - Orchestrator](design-and-build-runbooks.md)
