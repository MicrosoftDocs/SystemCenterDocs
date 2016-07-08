---
title: Manual Steps to Prepare Upgraded SQL Server
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd84d763-c42d-4e53-9803-4786ef182ec6
 

















---
# Manual Steps to Prepare Upgraded SQL Server
If you upgrade SQL Server 2008 R2 to SQL 2012 after Service Manager SP1 installation, you must manually copy the Microsoft.EnterpriseManagement.Reporting.Code.dll file in order for SQL Server Reporting Services \(SSRS\) to function properly.  
  
### To copy the Microsoft.EnterpriseManagement.Reporting.Code.dll file  
  
1.  On the computer that is hosting SSRS, open an instance of Windows Explorer.  
  
2.  Open \<InstallationDrive\>:\\Program Files\\Microsoft SQL Server\\MSRS11.MSSQLSERVER\\Reporting Services\\ReportServer\\bin and copy the Microsoft.EnterpriseManagement.Reporting.Code.dll file from the Prerequisites folder on your Service Manager installation media folder.
