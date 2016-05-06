---
title: About Reimporting Previously Removed Management Packs
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1fb98a73-5130-4d1e-934b-94607b9c0d57
---
# About Reimporting Previously Removed Management Packs
During development and testing of management packs that contain reports that access data warehouse information, you might need to remove the management packs and then reimport them later. However, after a management pack is uninstalled from the data warehouse, if the new management pack contains the same dimension, fact, or cube name with a schema that is different from the original, you must delete the dimension or fact table from the DWRepository and DWDataMart databases manually and also delete any referencing cube from the SQL Server Analysis Services \(SSAS\) database.

In addition, if a dimension or fact is already referenced by an existing data cube, you must also delete the management pack that contains the data cube and the data cube itself before uninstalling the new management pack. Because Service Manager does not remove the dimension or fact table from the DataSourceView and because dimensions are not removed from SSAS database, you must manually delete information that a data cube references. In this situation, you should use SQL Server Management Studio to remove any custom data cube that you created with the management pack from the DWASDatabase before you reregister or reinstall an updated management pack.

In general, you should avoid having the same dimension, fact, and cube name in differing schemas. [!INCLUDE[smshort](../Token/smshort_md.md)] does not support this condition.

