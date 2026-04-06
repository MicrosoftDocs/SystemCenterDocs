---
title: Delete Item
description: The Delete Item activity is used in a runbook to delete the existing appointments, contact groups, email messages, and task items.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 2ae557bc-f457-4ae5-b542-b7f7fca66f8f
author: Jeronika-MS
ms.author: v-gajeronika
---
# Delete Item

The Delete Item activity is used in a runbook to delete the existing appointments, contact groups, email messages, and task items.

The following tables list the required properties and published data for this activity.

## Delete Item Required Properties

| **Element** | **Description**   | **Valid values**   |
|:---|:---|:---|
| ID   | The ID of the item to be deleted | String   |
| Mode   | The delete mode   | Hard Delete<br>Soft Delete<br>Move to Deleted Items |

## Delete Item Published Data

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| ID   | The ID of the item to be deleted   | String   |
| Mode   | The delete mode   | String   |
| Domain   | Domain the Exchange server belongs to   | String   |
| Exchange Server Address | Address of the Exchange server   | String   |
| Timeout (seconds)   | Timeout value for the Exchange server connection   | Number   |
| Use Autodiscover   | Whether or not to use Autodiscover to check for changes | Boolean   |
| User Name   | Username used to connect to the Exchange server   | String   |

## See Also

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md) <br> <br>
