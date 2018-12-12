---
title: List Management Certificate
description: The List Management Certificate activity is used in a runbook to list basic information about all of the management certificates associated with the specified subscription.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: e62158f4-c8bd-4a51-ab8a-0deee62347fd
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# List Management Certificate

The **List Management Certificate** activity is used in a runbook to list basic information about all of the management certificates associated with the specified subscription. It is part of the **Azure Certificates** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## List Management Certificate required properties

There are no required properties for this runbook activity.

## List Management Certificate optional properties

There are no optional properties for this runbook activity.

## List Management Certificate published data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Management Certificate Public Data (base64) | A base64 representation of the data contained in the management certificate, in .cer format.   | String   |
| Management Certificate Public Key (base64)  | A base64 representation of the management certificate public key.   | String   |
| Management Certificate Time Created   | The time that the management certificate was created, in UTC.   | Datetime   |
| Management Certificate Thumbprint   | The X509 certificate thumb print property of the management certificate. This thumb print uniquely identifies the certificate. | String   |
