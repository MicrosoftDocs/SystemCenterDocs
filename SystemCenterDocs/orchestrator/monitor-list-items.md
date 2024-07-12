---
title: Monitor List Items
description: The Monitor List Items activity is used in a runbook to monitor a Microsoft SharePoint list for new and/or modified items.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/09/2023
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c4769c4-94a8-48a2-90d2-37e558a92b78
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
robots: noindex
---
# Monitor List Items



The **Monitor List Items** activity is used in a runbook to monitor a Microsoft SharePoint list for new and/or modified items.

The following tables list the filters, required properties, and Published Data for this activity. Additional filters and Published Data are generated, which are based on the SharePoint list that is retrieved when you define the activity.

## Monitor List Items required properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| List Name   | The name of the SharePoint list to be monitored.   | String   |
| Monitor New Items   | A Boolean value that indicates whether to monitor the list for new items.   | True<br>False   |
| Monitor Modified Items | A Boolean value that indicates whether to monitor the list for modified items.   | True<br>False   |
| Monitor Interval   | The number of seconds that the monitor waits between subsequent monitoring sessions. | Integer   |

## Monitor List Items filters

| **Element** | **Description**   | **Valid values**   |
|:---|:---|:---|
| Created   | The date and time when the item was created.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than |
| Created By  | The name of the user who created the item.   | Equals<br>Does not equal   |
| ID   | The ID of the list item.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than |
| Modified   | The date and time when the item was last modified. | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than |
| Modified By | The name of the user who last modified the item.   | Equals<br>Does not equal   |

## Monitor List Items published data

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
