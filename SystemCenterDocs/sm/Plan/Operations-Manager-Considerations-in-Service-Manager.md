---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Operations Manager Considerations in Service Manager
ms.technology:  service-manager
ms.assetid:  0eb44190-b525-410a-a105-47355f2fccdd
---

# Operations Manager Considerations in Service Manager

>Applies To: System Center 2016 Technical Preview - Service Manager

This topic contains information to be aware of when you are combining Operations Manager and Service Manager.

## Management Group Names Must be Unique
When you deploy both a Service Manager and data warehouse management server, you are asked to provide a management group name. You are also asked to provide a management group name when you deploy Operations Manager. The management group names that you use for the Service Manager management group, the data warehouse management group, and the Operations Manager management group must be unique.

> [!IMPORTANT]
> If Operations Manager and Service Manager share the same management group name, you will have to reinstall the Service Manager management server. Because it is not possible to rename a management group, you will either have to completely reinstall Service Manager with a different management group name or choose not to manage your Service Manager installation with Operations Manager.

## Database Collations
You must use the same supported language collations if you intend to import data from Operations Manager into Service Manager. However, this is true only for the OperationsManager database in Operations Manager and the SM DWStagingAndConfig database when you create an Operations Manager Data Source for the data warehouse. Specifically, this appears in the Service Manager console as a Data Warehouse Data Source. This does not affect either the System Center Operations Manager to System Center Service Manager Configuration Item connector or the System Center Operations Manager to System Center Service Manager Alert Incident connector.

For more information about the SQL Server collation setting that might impact installation requirements in System Center 2012 Service Pack 1 (SP1) when you use Operations Manager and Service Manager, see [Clarification on SQL Server Collation Requirements for System Center 2012](http://blogs.technet.com/b/servicemanager/archive/2012/05/24/clarification-on-sql-server-collation-requirements-for-system-center-2012.aspx).

> [!NOTE]
> If you have databases with collations that do not match, then you cannot use the Operations Manager to Service Manager data warehouse connector which imports alerts from the OperationsManager database  in Operations Manager to the Service Manager DWStagingAndConfig database.



