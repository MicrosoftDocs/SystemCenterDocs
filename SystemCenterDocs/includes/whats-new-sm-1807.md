---
title:  include file
description: include file to describes the new features and other changes in System Center 1807 - Service Manager.
manager:  vvithal
ms.topic:  include
author:  JYOTHIRMAISURI
ms.author: v-jysur
ms.prod:  system-center-2016
keywords:  
ms.date: 07/24/2018
ms.technology:  service-manager
ms.assetid:  89743b74-65f9-4eac-8fcc-6a0cf43819d9
---

## What's new in System Center 1807 - Service Manager
The following new feature is included in SM 1807.

## Support to SQL 2017 feature pack

SM 1807 supports SQL 2017. You can upgrade SQL server 2016 to SQL 2017.
[Learn more](system-reqs-sm-1807.md#upgrade-to-sql-1807)

> [!NOTE]

> - With SM 1807, SQL 2017 is supported only if it is upgraded from SQL 2016. Fresh installation of SQL 2017 with SM 1807 is not supported. Users with 1801 deployment and SQL 2016 needs to apply SM 1807 and then upgrade to SQL 2017.

> - Upgrade process to SQL 2017 uninstalls the reporting services, ensure to migrate required reports such as backup reporting DB and encryption keys.
