---
title: Add Service Certificate
description: The Add Service Certificate activity is used in a runbook to add a certificate to a cloud service.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 5c12e8ec-fdc2-40c9-b217-5f598f9b93ad
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Add Service Certificate

Applies To: System Center 2016 - Orchestrator

The **Add Service Certificate** activity is used in a runbook to add a certificate to a cloud service. It is part of the **Azure Certificates** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

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

## See Also

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
