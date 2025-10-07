---
title:  include file
description: include file to describe the new features and other changes in System Center 1807 - Service Manager.
ms.topic:  include
author: Jeronika-MS
ms.author: v-gajeronika
ms.service:  system-center
keywords:  
ms.date: 07/24/2018
ms.subservice:  service-manager
ms.assetid:  89743b74-65f9-4eac-8fcc-6a0cf43819d9
---

## What's new in System Center 1807 - Service Manager
The following new feature is included in SM 1807.

>[!NOTE]
> To view the bugs fixed and the installation instructions for SM 1807, see [KB article 4338239](https://support.microsoft.com/help/4338239).

## Support to SQL 2017 feature pack

SM 1807 supports SQL 2017. You can upgrade SQL server 2016 to SQL 2017.
[Learn more](../scsm/system-requirements.md)

> [!NOTE]
> - With SM 1807, SQL 2017 is supported only if it's upgraded from SQL 2016. Fresh installation of SQL 2017 with SM 1807 isn't supported. Users with 1801 deployment and SQL 2016 need to apply SM 1807 and then upgrade to SQL 2017.
> - Upgrade process to SQL 2017 uninstalls the reporting services; ensure to migrate the required reports such as backup reporting DB and encryption keys.
