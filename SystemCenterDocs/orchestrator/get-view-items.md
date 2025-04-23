---
title: Get View Items
description: The Get View Items activity is used in a runbook to retrieve data about the items in a Microsoft SharePoint list by using one of the list's views.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 04/23/2025
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 08e35080-8778-4199-96c0-6522aa8d586a
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
---

# Get View Items

This article provides information about the **Get View Items** activity used in a runbook to retrieve data about the items in a Microsoft SharePoint list by using one of the list's views.

The following tables list the required properties and Published Data for this activity. Additional Published Data is generated, which is based on the SharePoint list that is retrieved when you define the activity.

## Get View Items Required Properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| List Name   | The name of the SharePoint list to be searched.   | String   |
| List View   | The name of the list view to determine which items to select. | String   |

## Get View Items Published Data

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
| View Name   | The name of the list view to determine which items to select.   | String   |
