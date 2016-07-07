---
title: Account Used for Running Setup
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45dff8a2-a4d5-4314-8385-c5037870ae0f
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Account Used for Running Setup
This topic describes the permissions that you need when you are installing a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server and [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] databases and when you are registering the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management group with the data warehouse management group in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)].  
  
> [!NOTE]  
>  The account that you use to run Setup is automatically made an administrator in [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
## Service Manager Management Server  
 You need the following permissions when you are installing a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server:  
  
-   Local administrator on the computer that you run Setup on  
  
-   Local administrator on the computer that will host the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database if it is on a remote computer  
  
-   Logged\-on user must be a domain account  
  
-   The Sysadmin SQL Server role on the SQL Server instance where the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database is being created  
  
## Service Manager Console  
 You need the following permissions when you are installing the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]:  
  
-   Local administrator on the computer that you run Setup on  
  
## Data Warehouse Management Server  
 You need the following permissions when you are installing the data warehouse management server:  
  
-   Local administrator on the computer that you run Setup on  
  
-   Local administrator on the computer that will host the data warehouse database if it is on a remote computer  
  
-   Logged\-in user must be a domain account  
  
-   The Content Manager role in SQL Server Reporting Services \(SSRS\) at the site level \(root\)  
  
-   The Sysadmin SQL Server role on the SQL Server instance where the data warehouse database is being created  
  
## SQL Server Reporting Services  
 You need the following permissions when you are installing SSRS:  
  
-   Permissions to place a binary file into the \\Program Files\\Microsoft SQL Server\\\<Instance Name\>\\Reporting Services\\ReportServer\\Bin folder on the computer hosting the data warehouse management server  
  
## Registering Service Manager with the Data Warehouse  
 You need the following permissions when you are registering [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] with the data warehouse:  
  
-   The Sysadmin or security admin SQL Server role on the instance that is hosting the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database  
  
-   The Sysadmin or security admin SQL Server role on the instance that is hosting the data warehouse database  
  
-   Membership in the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Administrators user role on the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server  
  
-   Membership in the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Administrators user role on the data warehouse management server