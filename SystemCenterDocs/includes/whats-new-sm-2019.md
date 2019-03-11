---
title:  include file
description: include file to describes the new features and other changes in System Center 2019 - Service Manager.
manager:  vvithal
ms.topic:  include
author:  JYOTHIRMAISURI
ms.author: v-jysur
ms.prod:  system-center
keywords:  
ms.date: 03/14/2019
ms.technology:  service-manager
ms.assetid:  11e4f7ef-cca9-4125-ab47-95dd19333dd9
---

## New features in SM 2019
See the following sections for information about the new features/features updated in SM 2019.

## Support to SQL 2017
SM 2019 supports new installation of SQL Server 2017.
[Learn more](../scsm/system-requirements.md)

##	Improvement in Active Directory Connector
The Active Directory (AD) connector has been improvised to synchronize with a specific domain controller. You may now, specify the domain controller in the LDAP query of the Active Directory connector.

##	Improved UI Responsiveness
The user interface is made responsive by addressing memory leak problems.

## Enable Service Logon
In earlier releases, during the setup of Service Manager Management Server and Service Manager Data Warehouse Management Server, various credentials are asked for SM accounts. These accounts had been interactive (accounts having **Allow log on locally** (SetInteractiveLogonRight) permission).

With SM 2019, we have enabled *Service Logon* type to make Service Manager more secure, and the default logon type is set to *Service Logon*. For information on how to grant service logon permissions to the Run As accounts, see [enable service logon feature](./systemcenterdocs/scom/enable-service-logon.md).

## Bug fixes
This release of System Center Service Manager contains all the bug fixes shipped until the [Update Rollup 5 of SCSM 2016](https://support.microsoft.com/help/4093685/update-rollup-5-for-system-center-2016-service-manager).  

> [!NOTE]

> The following feature was introduced in Service Manager 1807, enhanced in 2019.

## Support to SQL 2017 feature pack

You can upgrade SQL server 2016 to SQL 2017.
[Learn more](../scsm/system-requirements.md)

> [!NOTE]

> The following feature was introduced in Service Manager 1801, included in 2019.

## Support to enhanced evaluation experience

SM supports an enhanced experience for evaluating Service Manager and activating the product for retail use.  

The evaluation version of Service Manager can be installed and used for 180 days. in SM 2016, after an evaluation version is installed, there was no option to view the remaining days for the evaluation period. With Service Manager 1801 and later, you can view the information about the evaluation period, and accordingly activate your SM. [Learn more](../scsm/sm-license.md)
