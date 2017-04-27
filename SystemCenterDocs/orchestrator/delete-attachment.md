---
title: Delete Attachment
description: The Delete Attachment activity is used in a runbook to delete an attachment from a Microsoft SharePoint list item.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 01589057-32ee-4de2-8148-59eacc1586a4
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Delete Attachment

Applies To: System Center 2016 - Orchestrator

The **Delete Attachment** activity is used in a runbook to delete an attachment from a Microsoft SharePoint list item.

The following tables list the required properties and Published Data for this activity.

## Delete Attachment Required Properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Attachment  | The file name and file name extension of the attachment to be deleted. | String   |
| ID   | The ID of the list item to be updated.   | Integer   |
| List Name   | The name of the SharePoint list that contains the item to be updated.  | String   |

## Delete Attachment Optional Properties

There are no optional properties for this runbook activity.

## Delete Attachment Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Attachment   | The file name and file name extension of the attachment that was deleted. | String   |
| ID   | The ID of the list item that was updated.   | Integer   |
| List Name   | The name of the SharePoint list that contains the item that was updated.  | String   |
| SharePoint Site | The URL of the SharePoint site.   | String   |

## See Also


[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
