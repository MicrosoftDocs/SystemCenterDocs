---
title: Query List
description: The Query List activity is used in a runbook to retrieve data about the items in a Microsoft SharePoint list by using Collaborative Application Markup Language (CAML).
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 157c07bc-10eb-4c38-ba66-472f1736d3d6
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Query List

The **Query List** activity is used in a runbook to retrieve data about the items in a Microsoft SharePoint list by using a [Collaborative Application Markup Language (CAML)](https://msdn.microsoft.com/library/ms467521.aspx) that you specify.

The following tables list the required properties and Published Data for this activity. Additional Published Data is generated, which is based on the SharePoint list that is retrieved when you define the activity.

## Query List required properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| List Name   | The name of the SharePoint list to be searched.   | String   |
| CAML Query  | A CAML query to determine which items to select.<br> **Important** Do not enclose the CAML XML in &lt;Query&gt;&lt;/Query&gt; tags. | String   |

## Query List optional properties

There are no optional properties for this runbook activity.

## Query List published data

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
