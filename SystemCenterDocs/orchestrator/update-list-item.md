---
title: Update List Item
description: The Update List Item activity is used in a runbook to update an item in a Microsoft SharePoint list.
ms.custom: na
ms.date: 05/07/2019
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 7c9627b5-2136-407f-a2c9-2be38f3415ba
author: jyothisuri
ms.author: jsuri
manager: evansma
robots: noindex
---
# Update List Item

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The **Update List Item** activity is used in a runbook to update an item in a Microsoft SharePoint list.

The following tables list the required properties and Published Data for this activity. Additional optional properties are generated, which are based on the SharePoint list that is retrieved when you define the activity.

## Update List Item Required Properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| ID   | The ID of the list item to be updated.   | Integer   |
| List Name   | The name of the SharePoint list that contains the item to be updated. | String   |

## Update List Item Optional Properties

There are no optional properties for this runbook activity.

## Update List Item Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| ID   | The ID of the updated list item.   | Integer   |
| SharePoint List | The name of the SharePoint list that contains the updated item. | String   |
| SharePoint Site | The URL of the SharePoint site.   | String   |

>[!TIP]
>You can use comma-separated values to specify input values for multi-choice fields.

## Other Resources

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
