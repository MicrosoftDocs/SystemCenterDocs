---
title: Get List Items
description: The Get List Items activity is used in a runbook to retrieve data about the items in a Microsoft SharePoint list.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99b3f71f-f993-4501-a726-71bb399bd815
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Get List Items

Applies To: System Center 2016 - Orchestrator

The **Get List Items** activity is used in a runbook to retrieve data about the items in a Microsoft SharePoint list.

The following tables list the filters, required and optional properties, and Published Data for this activity. Additional filters and Published Data are generated, which are based on the SharePoint list that is retrieved when you define the activity.

## Get List Items Required Properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| List Name   | The name of the SharePoint list to be searched. | String   |

## Get List Items Optional Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Ascending   | A Boolean value that indicates whether to retrieve the list items in ascending order. Used in conjunction with the optional properties Maximum Items and Order By. | True<br>False   |
| Maximum Items | The maximum number of items to select. Used in conjunction with the optional properties Ascending and Order By.   | Integer   |
| Order By   | The order of the retrieved items. Used in conjunction with the optional properties Ascending and Maximum Items.   | String   |

## Get List Items Filters

| **Element** | **Description**   | **Valid values**   |
|:---|:---|:---|
| Created   | The date and time when the item was created.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than |
| Created By  | The name of the user who created the item.   | Equals<br>Does not equal   |
| ID   | The ID of the list item.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than |
| Modified   | The date and time when the item was last modified. | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than |
| Modified By | The name of the user who last modified the item.   | Equals<br>Does not equal   |

## Get List Items Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Created   | The date and time when the item was created.   | Date/Time   |
| Created By   | The name of the user who created the item.   | String   |
| ID   | The ID of the list item.   | Integer   |
| Item Count   | The number of items that were retrieved.   | Integer   |
| List Name   | The name of the SharePoint list that contains the items that were retrieved. | String   |
| Modified   | The date and time when the item was last modified.   | Date/Time   |
| Modified By   | The name of the user who last modified the item.   | String   |
| SharePoint Site | The URL of the SharePoint site.   | String   |

## See Also


#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

