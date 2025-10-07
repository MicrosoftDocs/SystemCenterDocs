---
title: Get Operation Status
description: The Get Operation Status activity is used to get the status of the specified operation.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 08/07/2025
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 12a83835-4c84-4474-a8e0-df70d88e2818
author: Jeronika-MS
ms.author: v-gajeronika
monikerRange: '<=sc-orch-2019'
---

# Get Operation Status

The **Get Operation Status** activity is used to get the status of the specified operation. After calling another activity with 'Wait for Completion' set to false, you can use the Get Operation Status activity to determine whether the operation requested by that activity has succeeded, failed, or is still in progress. Get Operation Status is part of the Azure Deployments category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Get Operation Status Required Properties

| **Element** | **Description**   | **Valid Values** |
|:---|:---|:---|
| Request ID  | The request ID of an asynchronous request made using another Windows Azure Integration pack activity. | String   |

## Get Operation Status Optional Properties

There are no optional properties for this activity.

## Get Operation Status Published Data

| **Element**   | **Description**   | **Value Type** |
|:---|:---|:---|
| Request ID   | The request ID of the asynchronous request made using another Windows Azure Integration pack activity. | String   |
| Status   | The status of the asynchronous request. The valid values are InProgress, Succeeded, and Failed.   | String   |
| Error Code   | The management service error code returned if the asynchronous request failed.   | String   |
| Error Message | The management service error message returned if the asynchronous request failed.   | String   |
