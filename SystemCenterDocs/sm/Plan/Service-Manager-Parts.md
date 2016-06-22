---
title: Service Manager Parts
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b8d8f830-a235-409e-a31c-be40f215a5ad
---
# Service Manager Parts
There are six major parts of a System Center 2016 Technical Preview - Service Manager installation, as described in the following table.

###

|System Center 2016 Technical Preview - Service Manager part|Description|
|----------------------------------------------------------------------|---------------|
|System Center 2016 Technical Preview - Service Manager management server|Contains the main software part of a System Center 2016 Technical Preview - Service Manager installation. You can use the  System Center 2016 Technical Preview - Service Manager management server to manage incidents, changes, users, and tasks.|
|System Center 2016 Technical Preview - Service Manager database|The database that contains  System Center 2016 Technical Preview - Service Manager configuration items (CI) from the IT Enterprise; work items, such as incidents, change requests, and the configuration for the product itself. This is the System Center 2016 Technical Preview - Service Manager implementation of a Configuration Management Database (CMDB).|
|Data warehouse management server|The computer that hosts the server piece of the data warehouse.|
|Data warehouse databases|Databases that provide long-term storage of the business data that System Center 2016 Technical Preview - Service Manager generates. These databases are also used for reporting.|
|Service Manager console|The user interface (UI) piece that is used by both the help desk analyst and the help desk administrator to perform System Center 2016 Technical Preview - Service Manager functions, such as incidents, changes, and tasks. This part is installed automatically when you deploy a  System Center 2016 Technical Preview - Service Manager management server. In addition, you can manually install the Service Manager console as a stand-alone part on a computer.|
|Self-Service Portal|A web-based interface into System Center 2016 Technical Preview - Service Manager.|

> [!IMPORTANT]
> All computers that host any part of System Center 2016 Technical Preview - Service Manager must be domain joined.


