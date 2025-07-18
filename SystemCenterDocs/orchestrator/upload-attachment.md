---
title: Upload Attachment
description: The Upload Attachment activity is used to upload a file to an existing Service Manager object.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 144e95f1-392f-473b-a504-0b763e78f9df
author: jyothisuri
ms.author: jsuri
robots: noindex
---
# Upload Attachment

The Upload Attachment activity is used to upload a file to an existing Service Manager object.

The following published data elements are specific to Upload Attachment. Additional published data is generated based on the Class that you select when you define the activity. For a list of the data elements published by each Class, see [Service Manager Published Data](service-manager-published-data.md).

## Upload Attachment Published Data

| Element  |Description   |
|---------------------------|---------------------------------------------------------------------|
| System Center Object GUID | The unique identifier (GUID) of the single attachment to be updated |
| Number of Objects   | The number of files successfully uploaded by Upload Attachment   |

## Configuring the Upload Attachment Activity Workflow for File Attachments

The Upload Attachment activity is dependent on other activities for the data that it requires.

For file attachments, the following activities will usually precede the Upload Attachment activity in a workflow:

-   A parent record must exist. For example, you could use Create Change with Template or Get Object to get the Object Guid of a parent record where the attachment is to be uploaded.
-   Use Get File Status to get information about the file to be uploaded. This activity retrieves the data needed to attach the file to the Service Manager object.
-   Use Create Related Object to create a File Attachment related to the parent record. This activity creates the File Attachment object where the attachment is to be uploaded. There are several critical fields that must be correctly populated in order for the attachment to behave correctly in Service Manager

## Configure the Upload Attachment Activity Workflow for Knowledge Articles

The Upload Attachment activity is dependent on other activities for the data that it requires. For knowledge articles, the following activities usually precede the Upload Attachment activity in a workflow:

-   A parent record must exist. For example, you could use Create Change with Template or Get Object to get an Object Guid of a parent record where the article is to be uploaded.
-   Use Get File Status to get information about the knowledge article to be uploaded. This activity retrieves the data needed to attach the knowledge article to the Service Manager object.
-   Use Create Object to create a knowledge article. This activity creates the knowledge article object where the article is to be uploaded.
