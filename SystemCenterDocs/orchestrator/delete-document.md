---
title: Delete Document
description: The Delete Document activity is used in a runbook to delete a document from a Microsoft SharePoint document library.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 7d59d0cc-f027-419b-89e3-50163c66fc8d
author: jyothisuri
ms.author: jsuri
---
# Delete Document

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

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
