---
title: Delete List Item
description: The Delete List Item activity is used in a runbook to delete an item from a Microsoft SharePoint list.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cd54565-fcd1-4326-bb0d-be17d0dd1356
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Delete List Item
================

Applies To: System Center 2016 - Orchestrator

The **Delete List Item** activity is used in a runbook to delete an item from a Microsoft SharePoint list.

The following tables list the required properties and published data for this activity.

Delete List Item Required Properties
------------------------------------

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| ID   | The ID of the list item to be deleted.   | Integer   |
| List Name   | The name of the SharePoint list that contains the item to be deleted. | String   |

Delete List Item Optional Properties
------------------------------------

There are no optional properties for this runbook activity.

Delete List Item Published Data
-------------------------------

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| ID   | The ID of the list item that was deleted.   | Integer   |
| List Name   | The name of the SharePoint list that contained the item that was deleted. | String   |
| SharePoint Site | The URL of the SharePoint site.   | String   |

See Also
--------

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

