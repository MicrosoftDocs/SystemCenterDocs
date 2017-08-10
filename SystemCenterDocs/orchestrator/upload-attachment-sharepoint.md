---
title: Upload Attachment
description: The Upload Attachment activity is used in a runbook to attach a file to a Microsoft SharePoint list item.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 7b6d6bc5-6de0-4207-9f5e-b5405913f293
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Upload Attachment

Applies To: System Center 2016 - Orchestrator

The **Upload Attachment** activity is used in a runbook to attach a file to a Microsoft SharePoint list item.

The following tables list the required properties and Published Data for this activity.

## Upload Attachment Required Properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| ID   | The ID of the list item to be uploaded.   | Integer   |
| List Name   | The name of the SharePoint list that contains the item to be uploaded. | String   |
| Source File | The absolute path of the file on the local computer to be uploaded.   | String   |

## Upload Attachment Optional Properties

There are no optional properties for this runbook activity.

## Upload Attachment Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| ID   | The ID of the list item that was uploaded.   | Integer   |
| SharePoint List | The name of the SharePoint list that contains the uploaded item.   | String   |
| SharePoint Site | The URL of the SharePoint site.   | String   |
| Source File   | The absolute path of the file on the local machine to be uploaded. | String   |

## See Also


## Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

