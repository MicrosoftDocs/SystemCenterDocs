---
title: List Service Certificate
description: The List Service Certificate activity is used in a runbook to list all of the service certificates associated with the specified cloud service.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: e538b939-e4f2-4092-b9c4-c1843e342149
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# List Service Certificate

The **List Service Certificate** activity is used in a runbook to list all of the service certificates associated with the specified cloud service. It is part of the **Azure Certificates** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## List Service Certificate required properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Service DNS Prefix | The DNS prefix name of the Windows Azure cloud service. | String   |

## List Service Certificate optional properties

There are no optional properties for this runbook activity.

## List Service Certificate published data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Service Certificate Public Data (base64) | A base64 representation of the data contained in the service certificate, in .cer format.   | String   |
| Service Certificate URL   | The Service Management API request URI used to perform Get Service Certificate requests against the certificate store.   | String   |
| Service Certificate Thumbprint   | The X509 certificate thumb print property of the service certificate. This thumb print uniquely identifies the certificate. | String   |
| Service Certificate Thumbprint Algorithm | The algorithm that was used to hash the service certificate. Currently SHA-1 is the only supported algorithm.   | String   |
| Service DNS Prefix   | The DNS prefix name of the Windows Azure cloud service.   | String   |
