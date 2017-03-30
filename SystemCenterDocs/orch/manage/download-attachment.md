---
title: Download Attachment
description: The Download Attachment activity is used in a runbook to download an attachment from a Microsoft SharePoint list item.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: db57641c-d761-4391-ba2f-871bdea9ce1a
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Download Attachment

Applies To: System Center 2016 - Orchestrator

The **Download Attachment** activity is used in a runbook to download an attachment from a Microsoft SharePoint list item.

The following tables list the required properties and Published Data for this activity.

## Download Attachment Required Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Action if Exists   | The action to take if the file already exists on the local computer.   | Overwrite<br>Rename<br>Skip |
| Attachment   | The file name and file name extension of the attachment to be downloaded.   | String   |
| Destination Folder | The absolute path of the folder on the local computer where the file is to be downloaded. | String   |
| ID   | The ID of the list item that contains the attachment to be downloaded.   | Integer   |
| List Name   | The name of the SharePoint list that contains the item.   | String   |

## Download Attachment Optional Properties

There are no optional properties for this runbook activity.

## Download Attachment Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Attachment   | The file name and file name extension of the file that was downloaded.   | String   |
| Destination File Name | The file name of the downloaded file on the local computer. The name of the downloaded file can be different from the name of the attachment if the Rename option was applied using the **Action If Exists** property. | String   |
| Destination Folder   | The absolute path of the folder on the local computer where the attachment was be downloaded.   | String   |
| Destination Path   | The absolute path of the downloaded file on the local computer.   | String   |
| ID   | The ID of the list item that contains the attachment that was downloaded.   | Integer   |
| List Name   | The name of the SharePoint list that contains the item.   | String   |
| SharePoint Site   | The URL of the SharePoint site.   | String   |

## See Also


#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

