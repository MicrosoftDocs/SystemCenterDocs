---
title: Add VM Endpoint
description: The Add VM Endpoint activity adds an external endpoint to the specified virtual machine.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: b6ddabeb-d6fb-4f7f-9b8e-afe7f88b01ba
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Add VM Endpoint

The **Add VM Endpoint** activity adds an external endpoint to the specified virtual machine. It is part of the **Azure Virtual Machines** category activity.

>[!NOTE]
>This activity will retrieve the current endpoints for a virtual machine from Azure, and then make a request to Azure to update the endpoints for the virtual machine to be all the retrieved endpoints, as well as the endpoint added using this activity. Because the activity requires two calls to Azure, it is possible to experience concurrency issues when another process modifies the endpoints after this activity retrieves them, but before this activity submits the updated endpoints. |

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Add VM Endpoint Required Properties

| **Element**   | **Description**   | **Valid Values** |
|:---|:---|:---|
| Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| Deployment Name   | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Endpoint Local Port  | Specifies the internal port on which the virtual machine is listening to serve the endpoint.   | Integer   |
| Endpoint Name   | Specifies the name for the external endpoint.   | String   |
| Endpoint Public Port | Specifies the external port to use for the endpoint.   | Integer   |
| Endpoint Protocol   | Specifies the transport protocol for the endpoint.   | TCP, UDP   |
| Wait for Completion  | Whether to wait for this operation to complete in Azure before moving on to the next activity. | True, False   |

## Add VM Endpoint Optional Properties

There are no optional properties for this activity.

## Add VM Endpoint Published Data

| **Element**   | **Description**   | **Valuestype** |
|:---|:---|:---|
| Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| Deployment Name   | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Endpoint Local Port  | Specifies the internal port on which the virtual machine is listening to serve the endpoint.   | Integer   |
| Endpoint Name   | Specifies the name for the external endpoint.   | String   |
| Endpoint Public Port | Specifies the external port to use for the endpoint.   | Integer   |
| Endpoint Protocol   | Specifies the transport protocol for the endpoint.   | String   |
| Wait for Completion  | Whether to wait for this operation to complete in Azure before moving on to the next activity. | Boolean   |
| Request ID   | The unique identifier of the request to Azure.   | String   |
