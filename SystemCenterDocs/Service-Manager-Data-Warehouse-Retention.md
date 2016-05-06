---
title: Service Manager Data Warehouse Retention
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b8678e2d-8c8c-40b4-a18f-b5495ad7a4cd
---
# Service Manager Data Warehouse Retention
By default, data is stored in the data warehouse for 3 years for fact tables and for an unlimited period for dimension and outrigger tables. However, you can modify the retention period if you want to retain data longer or groom it out more aggressively.

## Fact Table Retention Settings
There are 2 two types of retention settings in the data warehouse:

-   Global \- The global retention period for all fact tables in the database is set to 3 years by default, which any subsequently created fact tables use as their default retention setting.

-   Individual Fact – The granular retention period for each individual fact table, uses the global setting of 3 years, unless you modify them individually.

**Global**:
The default global retention period for data stored in the Service Manager data warehouse is 3 years, so all fact tables use 3 years as the default retention setting. Any subsequently\-created fact tables use this setting when created for their individual retention setting.

**Individual Fact Tables**:
Individual fact tables inherit the global retention value when created, or you can customize them to a value that differs from the default global setting. You can configure the default individual fact tables that were created during installation, individually with a specific retention value as needed.

#### To view the retention period for default tables or specific tables

1.  Use the **Get\-SCDWRetentionPeriod** PowerShell cmdlet to get the retention period for either a specific fact table within a specific data warehouse database or the default for fact tables within the database. See [Get\-SCDWRetentionPeriod](https://technet.microsoft.com/en-us/library/hh541718(v=sc.20).aspx) for detailed descriptions of available parameters and example usage.

#### To set the retention period for default tables or specific tables

1.  Use the **Set\-SCDWRetentionPeriod** PowerShell cmdlet to set the retention period for either a specific fact table within a specific data warehouse database or the default for fact tables within the database. See [Set\-SCDWRetentionPeriod](https://technet.microsoft.com/en-us/library/hh541725(v=sc.20).aspx) for detailed descriptions of available parameters and example usage.

