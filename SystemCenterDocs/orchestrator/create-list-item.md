---
title: Create List Item
description: The Create List Item activity is used in a runbook to create a new item in a SharePoint list.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 79ca0e5d-9350-43e3-95a0-bdb0f7714cdc
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Create List Item

Applies To: System Center 2016 - Orchestrator

The **Create List Item** activity is used in a runbook to create a new item in a SharePoint list.

The following tables list the required properties and Published Data for this activity. Additional required and optional properties are generated, which are based on the SharePoint list that is retrieved when you define the activity.

## Create List Item Required Properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| List Name   | The name of the SharePoint list to contain the new item. | String   |

## Create List Item Optional Properties

There are no optional properties for this runbook activity.

## Create List Item Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| ID   | The ID of the list item that was created.   | Integer   |
| List Name   | The name of the SharePoint list that contains the item that was created. | String   |
| SharePoint Site | The URL of the SharePoint site.   | String   |

>[!Tip]
> You can use comma-separated values to specify input values for multi-choice properties.

## See Also

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
