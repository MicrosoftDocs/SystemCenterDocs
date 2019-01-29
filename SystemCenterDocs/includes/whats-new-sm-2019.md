---
title:  include file
description: include file to describes the new features and other changes in System Center 2019 - Service Manager.
manager:  vvithal
ms.topic:  include
author:  JYOTHIRMAISURI
ms.author: v-jysur
ms.prod:  system-center
keywords:  
ms.date: 01/21/2019
ms.technology:  service-manager
ms.assetid:  11e4f7ef-cca9-4125-ab47-95dd19333dd9
---

## What's new in System Center 2019 - Service Manager
The following sections summarize the new features released in SM 2019.

## Support to enhanced evaluation experience
SM 2019 supports an enhanced experience for evaluating Service Manager and activating the product for retail use.  

The evaluation version of Service Manager can be installed and used for 180 days. In SM 2016, after an evaluation version is installed, there was no option to view the remaining days for the evaluation period. In Service Manager 2019, you can view the information about the evaluation period, and accordingly activate your SM. [Learn more](../scsm/sm-license.md)

## Support to SQL 2017
SM 2019 supports SQL Server 2017 fresh installation.
[Learn more](../scsm/system-requirements.md)

## Support to TLS 1.2
To ensure secure communication, SM 2019 supports Transport Layer Security (TLS) 1.2. For information about how to set up, configure and run your environment to use TLS 1.2, [Read this article](https://support.microsoft.com/help/4051111/tls-1-2-protocol-support-deployment-guide-for-system-center-2016).

##	Improvement in Active Directory Connector
The Active Directory (AD) connector has been improvised to synchronize with a specific domain controller. You may specify the Domain Controller in the LDAP query of the Active Directory connector.

##	Improved UI Responsiveness
The user interface has been made more responsive by addressing memory leak problems.

## Enable Service Logon
During the setup of Service Manager Management Server and Service Manager Data Warehouse Management Server, various credentials are asked for SCSM accounts. These accounts had been interactive (accounts having **Allow log on locally** (SetInteractiveLogonRight) permission) until now.

With SM 2019, we have enabled *Service Logon* type to make SCSM more secure, and default logon type has been set to Service Logon. For information on how to grant service logon privileges to the accounts, see this article.

## Bug fixes
This release of System Center Service Manager contains all the bug fixes shipped until the [Update Rollup 5 of SCSM 2016](https://support.microsoft.com/help/4093685/update-rollup-5-for-system-center-2016-service-manager).  
