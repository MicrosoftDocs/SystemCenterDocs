---
title: Get Documents
description: The Get Documents activity is used in a runbook to retrieve details about the documents in a Microsoft SharePoint document library.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 53456c0d-b7b8-4ef8-ad38-6b685dda54c6
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Get Documents
=============

Applies To: System Center 2016 - Orchestrator

The **Get Documents** activity is used in a runbook to retrieve details about the documents in a Microsoft SharePoint document library.

The following tables list the filters, required and optional properties, and Published Data for this activity. Additional filters and Published Data are generated, which are based on the SharePoint document library that is retrieved when you define the activity.

Get Documents Required Properties
---------------------------------

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Document Library | The name of the SharePoint document library to be searched. | String   |

Get Documents Optional Properties
---------------------------------

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Document Folder | The relative path of a child folder in the document library to refine the search.   | String   |
| Recursive   | A Boolean value that indicates whether to retrieve data from documents in all child folders. | True<br>False   |

Get Documents Filters
---------------------

| **Element** | **Description**   | **Valid values**   |
|:---|:---|:---|
| Created   | The date and time when the document was created.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than |
| Created By  | The name of the user who created the document.   | Equals<br>Does not equal   |
| ID   | The ID of the document.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than |
| Modified   | The date and time when the document was last modified. | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than |
| Modified By | The name of the user who last modified the document.   | Equals<br>Does not equal   |
| Title   | The title of the document.   | Equals<br>Does not equal<br>Contains<br>Starts with   |

Get Documents Published Data
----------------------------

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Created   | The date and time when the document was created.   | Date/Time   |
| Created By   | The name of the user who created the document.   | String   |
| Document Count   | The number of items that were retrieved.   | Integer   |
| Document Library | The name of the document library that contains the documents. | String   |
| ID   | The ID of the document.   | Integer   |
| Modified   | The date and time when the document was last modified.   | Date/Time   |
| Modified By   | The name of the user who last modified the document.   | String   |
| SharePoint Site  | The URL of the SharePoint site.   | String   |

See Also
--------

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

