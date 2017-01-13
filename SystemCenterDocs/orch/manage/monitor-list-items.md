---
title: Monitor List Items
description: The Monitor List Items activity is used in a runbook to monitor a Microsoft SharePoint list for new and/or modified items.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c4769c4-94a8-48a2-90d2-37e558a92b78
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Monitor List Items

Applies To: System Center 2016 - Orchestrator

The **Monitor List Items** activity is used in a runbook to monitor a Microsoft SharePoint list for new and/or modified items.

The following tables list the filters, required properties, and Published Data for this activity. Additional filters and Published Data are generated, which are based on the SharePoint list that is retrieved when you define the activity.

## Monitor List Items Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| List Name   | The name of the SharePoint list to be monitored.   | String   |
| Monitor New Items   | A Boolean value that indicates whether to monitor the list for new items.   | True<br>False   |
| Monitor Modified Items | A Boolean value that indicates whether to monitor the list for modified items.   | True<br>False   |
| Monitor Interval   | The number of seconds that the monitor waits between subsequent monitoring sessions. | Integer   |

## Montior List Items Filters

| **Element** | **Description**   | **Valid values**   |
|:---|:---|:---|
| Created   | The date and time when the item was created.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than |
| Created By  | The name of the user who created the item.   | Equals<br>Does not equal   |
| ID   | The ID of the list item.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than |
| Modified   | The date and time when the item was last modified. | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than |
| Modified By | The name of the user who last modified the item.   | Equals<br>Does not equal   |

## Monitor List Items Published Data

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

