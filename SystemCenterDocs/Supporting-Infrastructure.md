---
title: Supporting Infrastructure
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cfbb9154-2a9d-468b-b305-3e6a18534661
---
# Supporting Infrastructure
This section addresses prerequisites and issues involving Active Directory Domain Services \(AD DS\) and Domain Name System \(DNS\) that you need to be aware of before initiating your [!INCLUDE[om12long](Token/om12long_md.md)] installation.

## Active Directory Domain Services
[!INCLUDE[om12long](Token/om12long_md.md)] relies on AD DS for a number of services, including definition of security principles, rights assignment, authentication, and authorization. [!INCLUDE[om12short](Token/om12short_md.md)] queries AD DS when performing computer and service discovery and can use AD DS for storing and distributing agent configuration information. For [!INCLUDE[om12short](Token/om12short_md.md)] to function properly, AD DS and its supporting service, DNS, need to be healthy and at certain minimum configuration levels. In addition, certain domain naming conventions must be followed.

### Domain Space Naming
An [!INCLUDE[om12short](Token/om12short_md.md)] management group cannot be installed into a root Active Directory domain that has a flat DNS namespace. However, you can install the management group into child domains of the root domain. For example, you have a root domain that has a DNS name of "Woodgrove".  Because this root domain has a flat DNS namespace, you cannot install an [!INCLUDE[om12short](Token/om12short_md.md)] management group into the Woodgrove domain. But, if the Woodgrove domain has a child domain with a DNS name of "National", the fully qualified domain name of the child domain would be national.woodgrove. For more information about configuring Windows for domains with single\-label DNS names, see [Information about configuring Active Directory domains by using single\-label DNS names](http://go.microsoft.com/fwlink/p/?LinkID=160783).

### Domain Functional Level
Windows Server Active Directory can operate at different functional levels. These levels are distinguished by the version of the Windows Server operating system that is permitted on the domain controllers present in the domain. [!INCLUDE[om12long](Token/om12long_md.md)] requires that the domain functional level be Windows 2000 native, Windows Server 2003 interim, Windows Server 2003, or Windows Server 2008. The domain functional level of Windows Server 2008 R2 is also supported \(for the SP1 version of [!INCLUDE[om12long](Token/om12long_md.md)], Windows Server 2008 R2 SP1 and Windows Server 2012 are supported\). For [!INCLUDE[om12long](Token/om12long_md.md)] to function properly, you must check the domain functional level and raise it to the appropriate version. To do this, see [Raise the Domain Functional Level](http://go.microsoft.com/fwlink/p/?LinkId=232554).

> [!NOTE]
> Ensure that you exercise due caution prior to raising a domain's functional level because it cannot be reversed, and if there are any down\-level domain controllers, their function will be impacted.

### Forest Functional Level
The forest functional level is similar to the domain functional level in that it sets a minimum domain controller operating system level across the whole forest. After it is set, domain controllers with down\-level operating systems from lower functional levels cannot be introduced into the forest. [!INCLUDE[om12short](Token/om12short_md.md)] does not have a forest functional level requirement; however, if the forest functional level is left at the default Windows 2000 level, there may be domains in your forest that won't meet the minimum domain functional level requirement.

## DNS
DNS must be installed and in a healthy state to support AD DS. Beyond the reliance of [!INCLUDE[om12short](Token/om12short_md.md)] on AD DS, there are no specific DNS requirements.

## See Also
[Environmental Prerequisites for Operations Manager for System Center 2012](assetId:///95d59f73-5aa9-4616-b98c-30680406959a)


