---
title: Delete Item
description: The Delete Item activity is used in a runbook to delete the existing appointments, contact groups, email messages, and task items.
ms.custom: UpdateFrequency2
ms.date: 05/07/2019
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ae557bc-f457-4ae5-b542-b7f7fca66f8f
author: jyothisuri
ms.author: jsuri
manager: mkluck
robots: noindex
---
# Delete Item

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

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
