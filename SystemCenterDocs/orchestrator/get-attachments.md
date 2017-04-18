---
title: Get Attachments
description: The Get Attachments activity is used in a runbook to retrieve details from the attachments of a list item.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0efdc1f0-978a-46e8-b229-36b9663b4475
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Get Attachments

Applies To: System Center 2016 - Orchestrator

The **Get Attachments** activity is used in a runbook to retrieve details from the attachments of a list item.

The following tables list the filters, required properties, and Published Data for this activity.

## Get Attachments Required Properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| ID   | The ID of the list item to be searched.   | Integer   |
| List Name   | The name of the SharePoint list that contains the item to be queried. | String   |

## Get Attachments Filters

| **Element** | **Description**   | **Valid values**   |
|:---|:---|:---|
| Author   | The name of the user who created the attachment.   | Equals<br>Does not equal<br>Contains<br>Starts with   |
| Created   | The date and time when the attachment was created.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than |
| Modified   | The date and time when the attachment was last modified. | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than |
| Name   | The file name and extension of the attachment.   | Equals<br>Does not equal<br>Contains<br>Starts with   |
| Title   | The title of the attachment.   | Equals<br>Does not equal<br>Contains<br>Starts with   |
| URL Path   | The server relative path of the attachment.   | Equals<br>Does not equal   |

## Get Attachments Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Attachment Count | The number of attachments that were retrieved.   | Integer   |
| Author   | The name of the user who created the attachment.   | String   |
| Created   | The date and time when the attachment was created.   | Date/Time   |
| ID   | The ID of the list item that contains the attachments.   | String   |
| List Name   | The name of the SharePoint list that contains the items that were retrieved. | String   |
| Modified   | The date and time when the attachment was last modified.   | Date/Time   |
| Name   | The file name and extension of the attachment file.   | String   |
| SharePoint Site  | The URL of the SharePoint site.   | String   |
| Title   | The title of the attachment.   | String   |
| URL Path   | The server relative path of the attachment.   | String   |

## See Also


#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

