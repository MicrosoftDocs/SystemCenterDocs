---
ms.assetid: 74af9f14-35b0-4b87-87ca-980d9b9031b0
title: Active Directory and DNS Planning
description:
author: mgoedtel
manager: cfreemanwa
ms.date: 10/12/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Active Directory and DNS Planning

>Applies To: System Center 2016 - Operations Manager

This section addresses Active Directory Domain Services (AD DS) and Domain Name System (DNS) requirements that you need to be aware of when planning your System Center 2012 – Operations Manager design.

## Active Directory Domain Services

System Center 2016 – Operations Manager relies on AD DS for a number of services, including definition of security principles, rights assignment, authentication, and authorization. Operations Manager queries AD DS when performing computer and service discovery and can use AD DS for storing and distributing agent configuration information. For Operations Manager to function properly, AD DS and its supporting service, DNS, need to be healthy and at certain minimum configuration levels. In addition, certain domain naming conventions must be followed.

### Domain space naming

An Operations Manager management group cannot be installed into a root Active Directory domain that has a flat DNS namespace. However, you can install the management group into child domains of the root domain. For example, you have a root domain that has a DNS name of "Woodgrove". Because this root domain has a flat DNS namespace, you cannot install an Operations Manager management group into the Woodgrove domain. But, if the Woodgrove domain has a child domain with a DNS name of "National", the fully qualified domain name of the child domain would be national.woodgrove. For more information about configuring Windows for domains with single-label DNS names, see Information about configuring Active Directory domains by using single-label DNS names.

### Domain functional level

Windows Server Active Directory can operate at different functional levels. These levels are distinguished by the version of the Windows Server operating system that is permitted on the domain controllers present in the domain. System Center 2016 – Operations Manager requires that the domain functional level be Windows 2000 native, Windows Server 2003 interim, Windows Server 2003, or Windows Server 2008. The domain functional level of Windows Server 2008 R2, Windows Server 2008 R2 SP1 and Windows Server 2012 are supported. For System Center 2016 – Operations Manager to function properly, you must check the domain functional level and raise it to the appropriate version. To do this, see Raise the Domain Functional Level.

> [!NOTE] 
> Ensure that you exercise due caution prior to raising a domain's functional level because it cannot be reversed, and if there are any down-level domain controllers, their function will be impacted.

### Forest functional level

The forest functional level is similar to the domain functional level in that it sets a minimum domain controller operating system level across the whole forest. After it is set, domain controllers with down-level operating systems from lower functional levels cannot be introduced into the forest. Operations Manager does not have a forest functional level requirement; however, if the forest functional level is left at the default Windows 2000 level, there may be domains in your forest that won't meet the minimum domain functional level requirement.

## DNS

DNS must be installed and in a healthy state to support AD DS. Beyond the reliance of Operations Manager on AD DS, there are no specific DNS requirements
