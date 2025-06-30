---
title: Upload Document
description: The Upload Document activity is used in a runbook to upload a document to a Microsoft SharePoint document library.
ms.custom: 3
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 0259e54f-d6ba-4e2e-92a9-c3d27102bf88
author: jyothisuri
ms.author: jsuri
robots: noindex
---
# Upload Document

The **Upload Document** activity is used in a runbook to upload a document to a Microsoft SharePoint document library.

The following tables list the optional and required properties and Published Data for this activity.

## Upload Document Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Document Library | The name of the SharePoint document library to which the file is to be uploaded. | String   |
| Source File   | The absolute path of the file on the local computer to be uploaded.   | String   |

## Upload Document Optional Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Document Folder | The document library relative path of the child folder to which the file is to be uploaded. If this property isn't defined, the file is uploaded to the document library's root folder. | String   |
| Title   | The title to assign to the document.   | String   |

## Upload Document Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Document Library | The name of the SharePoint document library to which the file was uploaded.   | String   |
| SharePoint Site  | The URL of the SharePoint site.   | String   |
| Document ID   | The ID of the uploaded document.   | Integer   |
| Source File   | The absolute path of the uploaded file on the local computer.   | String   |
| Document Folder  | The document library relative path of the child folder to which the file was uploaded. | String   |
| Title   | The title that was assigned to the document.   | String   |

## Other Resources

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
