---
title: Add Management Certificate
description: The Add Management Certificate activity is used in a runbook to add a certificate to the list of management certificates.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e63b5b72-d93e-44af-b021-5854baa4da27
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Add Management Certificate
==========================

Applies To: System Center 2016 - Orchestrator

The **Add Management Certificate** activity is used in a runbook to add a certificate to the list of management certificates. It is part of the **Azure Certificates** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

Add Management Certificate Required Properties
----------------------------------------------

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Certificate File Path | The path to the management certificate file. | String   |
| Certificate File Type | The type of the management certificate file. | CER, PFX   |

Add Management Certificate Optional Properties
----------------------------------------------

There are no optional properties for this runbook activity.

Add Management Certificate Published Data
-----------------------------------------

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Request ID   | The unique identifier of the request to Windows Azure. | String   |
| Certificate File Path | The path to the management certificate file.   | String   |
| Certificate File Type | The type of the management certificate file.   | String   |

See Also
--------

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

