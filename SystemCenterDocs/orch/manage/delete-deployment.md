---
title: Delete Deployment
description: The Delete Deployment activity deletes the specified deployment.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40e827f1-2dfa-4a05-81c8-e23bfd8643ec
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Delete Deployment
=================

Applies To: System Center 2016 - Orchestrator

The **Delete Deployment** activity deletes the specified deployment. It is part of the **Azure Deployments** category activity.

| Important   |
|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| The delete deployment activity will delete all roles under the deployment. This includes the deletion of any virtual machines under the deployment. |

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

Delete Deployment Required Properties
-------------------------------------

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Service DNS Prefix  | The DNS prefix name of the Windows Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot of the deployment.   | Staging, Production |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity. | True, False   |

Delete Deployment Optional Properties
-------------------------------------

There are no optional properties for this runbook activity.

Delete Deployment Published Data
--------------------------------

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Request ID   | The unique identifier of the request to Windows Azure.   | String   |
| Service DNS Prefix  | The DNS prefix name of the Windows Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot of the deployment.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity. | Boolean   |

See Also
--------

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

