---
title:  include file
description: include file to describe the new features and other changes in System Center 2019 - Service Manager.
ms.topic:  include
author: jyothisuri
ms.author: jsuri
ms.service:  system-center
keywords:  
ms.date: 10/04/2023
ms.subservice: service-manager
ms.assetid:  11e4f7ef-cca9-4125-ab47-95dd19333dd9
---

## New features in SM 2019
See the following sections for information about the new features/features updated in Service Manager (SM) 2019.

## Support to SQL Server 2017
SM 2019 supports new installation of SQL Server 2017.
[Learn more](../scsm/system-requirements.md).

### Support for SQL Server 2019 CU8 and later

Service Manager supports SQL Server 2019 with Cumulative Update 8 (CU8) or later, as detailed [here](/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server).

>[!NOTE]
> - Service Manager 2019 supports SQL 2019 with CU8 or later; however, it doesn't support SQL 2019 RTM.
> - Use ODBC 17.3 to 17.10.4.1, and MSOLEDBSQL 18.2 to 18.6.6.


##	Improvement in Active Directory Connector
The Active Directory (AD) connector has been improvised to synchronize with a specific domain controller. You may now specify the domain controller in the LDAP query of the Active Directory connector.

##	Improved UI Responsiveness
The user interface is made responsive by addressing memory leak problems.

## Enable Service Logon
In earlier releases, during the setup of Service Manager Management Server and Service Manager Data Warehouse Management Server, various credentials are asked for SM accounts. These accounts had been interactive (accounts having **Allow log on locally** (SetInteractiveLogonRight) permission).

With SM 2019, we've enabled *Service Logon* type to make Service Manager more secure, and the default logon type is set to *Service Logon*. For information on how to grant service logon permissions to the Run As accounts, see enable service logon feature. [Learn more](../scsm/enable-service-log-on-sm.md).

## Bug fixes
This release of System Center Service Manager contains all the bug fixes shipped until the [Update Rollup 5 of SCSM 2016](https://support.microsoft.com/help/4093685/update-rollup-5-for-system-center-2016-service-manager).  

> [!NOTE]
> The following feature was introduced in Service Manager 1807, enhanced in 2019.

## Support to SQL 2017 feature pack

You can upgrade SQL server 2016 to SQL 2017.
[Learn more](../scsm/system-requirements.md).

> [!NOTE]
> The following feature was introduced in Service Manager 1801, included in 2019.

## Support to enhanced evaluation experience

SM supports an enhanced experience for evaluating Service Manager and activating the product for retail use.  

The evaluation version of Service Manager can be installed and used for 180 days. In SM 2016, after an evaluation version is installed, there was no option to view the remaining days for the evaluation period. With Service Manager 1801 and later, you can view the information about the evaluation period, and accordingly activate your SM. [Learn more](../scsm/sm-license.md).

## New features in Service Manager UR2

The following new feature is supported with Service Manager Update Rollup 2.

### Support for SQL 2019 CU8 or later

Service Manager UR2 supports SQL Server 2019 with Cumulative Update 8 (CU8) or later, as detailed [here](/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server).

This support is applicable for Service Manager 2019.

>[!NOTE]
> - Service Manager 2019 doesn't support SQL 2019 RTM, and supports SQL 2019 with CU8 or later.
> - Use ODBC 17.3 to 17.10.4.1, and MSOLEDBSQL 18.2 to 18.6.6.
