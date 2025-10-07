---
title: Download Document
description: The Download Document activity is used in a runbook to download a document from a Microsoft SharePoint document library.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 982e9a07-fd87-4d05-b486-ca9b5e91c2bb
author: Jeronika-MS
ms.author: v-gajeronika
---

# Download Document

The **Download Document** activity is used in a runbook to download a document from a Microsoft SharePoint document library.

The following tables list the required properties and Published Data for this activity.

## Download Document Required Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Action if Exists   | The action to take if the file already exists on the local computer.   | Overwrite<br>Rename<br>Skip |
| Destination Folder | The absolute path of the folder on the local computer where the file is to be downloaded. | String   |
| Document Library   | The name of the document library that contains the document to be downloaded.   | String   |
| ID   | The ID of the document to be downloaded.   | Integer   |

## Download Document Optional Properties

There are no optional properties for this runbook activity.

## Download Document Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Destination File Name | The file name of the downloaded file on the local computer. The name of the downloaded file can be different from the name of the attachment if the Rename option was applied in the **Action if Exists** property. | String   |
| Destination Folder   | The absolute path of the folder on the local computer where the file was downloaded.   | String   |
| Destination Path   | The absolute path of the downloaded file on the local computer.   | String   |
| Document ID   | The ID of the document that was downloaded.   | Integer   |
| Document Library   | The name of the document library that contained the document that was downloaded.   | String   |
| SharePoint Site   | The URL of the SharePoint site.   | String   |
