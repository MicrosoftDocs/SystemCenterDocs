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
There are six major parts of a [!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)] installation, as described in the following table.

###

|[!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)] part|Description|
|----------------------------------------------------------------------|---------------|
|[!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)] management server|Contains the main software part of a [!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)] installation. You can use the  [!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)] management server to manage incidents, changes, users, and tasks.|
|[!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)] database|The database that contains  [!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)] configuration items \(CI\) from the IT Enterprise; work items, such as incidents, change requests, and the configuration for the product itself. This is the [!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)] implementation of a Configuration Management Database \(CMDB\).|
|Data warehouse management server|The computer that hosts the server piece of the data warehouse.|
|Data warehouse databases|Databases that provide long\-term storage of the business data that [!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)] generates. These databases are also used for reporting.|
|[!INCLUDE[smcons](../Token/smcons_md.md)]|The user interface \(UI\) piece that is used by both the help desk analyst and the help desk administrator to perform [!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)] functions, such as incidents, changes, and tasks. This part is installed automatically when you deploy a  [!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)] management server. In addition, you can manually install the [!INCLUDE[smcons](../Token/smcons_md.md)] as a stand\-alone part on a computer.|
|[!INCLUDE[smssp](../Token/smssp_md.md)]|A web\-based interface into [!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)].|

> [!IMPORTANT]
> All computers that host any part of [!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)] must be domain joined.

