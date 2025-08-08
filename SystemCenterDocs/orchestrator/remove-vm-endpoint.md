---
title: Remove VM Endpoint
description: The Remove VM Endpoint activity removes an external endpoint from the specified virtual machine.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 1102ac6c-cbce-4ad6-b36d-7085c3c4c3b7
author: jyothisuri
ms.author: jsuri
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# Remove VM Endpoint

The **Remove VM Endpoint** activity removes an external endpoint from the specified virtual machine. It's part of the **Azure Virtual Machines** category activity.

>[!NOTE]
>This activity will retrieve the current endpoints for a virtual machine from Windows Azure, and then make a request to Windows Azure to update the endpoints for the virtual machine to be all the retrieved endpoints except the endpoint removed using this activity. Because the activity requires two calls to Windows Azure, it's possible to experience concurrency issues when another process modifies the endpoints after this activity retrieves them, but before this activity submits the updated endpoints.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Remove VM Endpoint required properties

| **Element**   | **Description**   | **Valid Values** |
|:---|:---|:---|
| Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| Deployment Name   | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Endpoint Name   | Specifies the name of the external endpoint.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity. | True, False   |

## Remove VM Endpoint optional properties

There are no optional properties for this activity.

## Remove VM Endpoint published data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| Deployment Name   | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Endpoint Name   | Specifies the name of the external endpoint.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity. | Boolean   |
| Request ID   | The unique identifier of the request to Windows Azure.   | String   |
