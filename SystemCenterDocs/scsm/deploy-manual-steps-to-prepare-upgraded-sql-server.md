---
title: Manual steps to prepare upgraded SQL Server
description: After upgrade from SQL Server 2012 to SQL 2016, you must manually copy the Microsoft.EnterpriseManagement.Reporting.Code.dll file.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd84d763-c42d-4e53-9803-4786ef182ec6
---

# Manual steps to prepare upgraded SQL Server

>Applies To: System Center 2016 - Service Manager

If you upgrade SQL Server 2012 to SQL 2016 after Service Manager 2016 installation, you must manually copy the Microsoft.EnterpriseManagement.Reporting.Code.dll file in order for SQL Server Reporting Services \(SSRS\) to function properly.  

## Copy the Microsoft.EnterpriseManagement.Reporting.Code.dll file  

1.  On the computer that is hosting SSRS, open an instance of Windows Explorer.  

2.  Open \<InstallationDrive\>:\\Program Files\\Microsoft SQL Server\\MSRS13.MSSQLSERVER\\Reporting Services\\ReportServer\\bin and copy the Microsoft.EnterpriseManagement.Reporting.Code.dll file from the Prerequisites folder on your Service Manager installation media folder.
