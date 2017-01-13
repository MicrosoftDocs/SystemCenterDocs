---
title: Remove VM Endpoint
description: The Remove VM Endpoint activity removes an external endpoint from the specified virtual machine.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1102ac6c-cbce-4ad6-b36d-7085c3c4c3b7
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Remove VM Endpoint

Applies To: System Center 2016 - Orchestrator

The **Remove VM Endpoint** activity removes an external endpoint from the specified virtual machine. It is part of the **Azure Virtual Machines** category activity.

| Note   |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| This activity will retrieve the current endpoints for a virtual machine from Windows Azure, and then make a request to Windows Azure to update the endpoints for the virtual machine to be all the retrieved endpoints, except the endpoint removed using this activity. Because the activity requires two calls to Windows Azure, it is possible to experience concurrency issues when another process modifies the endpoints after this activity retrieves them, but before this activity submits the updated endpoints. |

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Remove VM Endpoint Required Properties

| **Element**   | **Description**   | **Valid Values** |
|:---|:---|:---|
| Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| Deployment Name   | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Endpoint Name   | Specifies the name of the external endpoint.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity. | True, False   |

## Remove VM Endpoint Optional Properties

There are no optional properties for this activity.

## Remove VM Endpoint Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| Deployment Name   | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Endpoint Name   | Specifies the name of the external endpoint.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity. | Boolean   |
| Request ID   | The unique identifier of the request to Windows Azure.   | String   |


