---
title: Delete Document
description: The Delete Document activity is used in a runbook to delete a document from a Microsoft SharePoint document library.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d59d0cc-f027-419b-89e3-50163c66fc8d
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Delete Document

Applies To: System Center 2016 - Orchestrator

The **Delete Document** activity is used in a runbook to delete a document from a Microsoft SharePoint document library.

The following tables list the required properties and Published Data for this activity.

## Delete Document Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Document Library | The name of the document library that contains the document to be deleted. | String   |
| Document ID   | The ID of the document to be deleted.   | Integer   |

## Delete Document Optional Properties

There are no optional properties for this runbook activity.

## Delete Document Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Document Library | The name of the document library that contained the document that was deleted. | String   |
| Document ID   | The ID of the document that was deleted.   | Integer   |
| SharePoint Site  | The URL of the SharePoint site.   | String   |

## See Also


#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

