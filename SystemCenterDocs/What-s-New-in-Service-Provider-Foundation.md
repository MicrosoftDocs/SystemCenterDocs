---
title: What&#39;s New in Service Provider Foundation
ms.custom: na
ms.prod: system-center-2012-sp1
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed01f5d9-391d-439e-916d-3fa25ad941dd
---
# What&#39;s New in Service Provider Foundation
This topic summarizes the main new features and capabilities in [!INCLUDE[spflong](./Token/spflong_md.md)], after its first release with [!INCLUDE[orchshort](./Token/orchshort_md.md)] in [!INCLUDE[spfshort](./Token/spfshort_md.md)][!INCLUDE[sc2012sp1_short](./Token/sc2012sp1_short_md.md)]. The current version is [!INCLUDE[spfshort](./Token/spfshort_md.md)][!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)].

## New server and stamp capabilities
The following table lists the server types that are now available for the `Server` object, and you can add one or more of them to a `Stamp` object using the Windows PowerShell cmdlets or the Administration web service.

|Server type|Enumeration Value|
|---------------|---------------------|
|VMM|0|
|OM|1|
|DPM|2|
|OMDW|3|
|RDGateway|4|
|Orchestrator|5|
|None|6|

For more information. see [Post-Installation Tasks for Service Provider Foundation](./Post-Installation-Tasks-for-Service-Provider-Foundation.md).

## Gallery item management
Gallery items are virtual machine roles that hosting service providers can use to provide offerings to their tenants. For more information, see [Importing Gallery Items in Service Provider Foundation](./Importing-Gallery-Items-in-Service-Provider-Foundation.md).

## Automation support
You can configure the Service Management Automation web service to use [!INCLUDE[spfshort](./Token/spfshort_md.md)]. For more information, see "Connecting to the Service Management Automation web service" in [Manage Web Services and Connections in Service Provider Foundation](./Manage-Web-Services-and-Connections-in-Service-Provider-Foundation.md) and [How to Automate a Runbook from Service Provider Foundation](./How-to-Automate-a-Runbook-from-Service-Provider-Foundation.md).

## The Usage web service
[!INCLUDE[spfshort](./Token/spfshort_md.md)] now provides the Usage web service for portals and billing providers to monitor tenant usage data. For more information, see the "Usage web service" section in [Manage Web Services and Connections in Service Provider Foundation](./Manage-Web-Services-and-Connections-in-Service-Provider-Foundation.md) and [Usage Metering in Service Provider Foundation](./Usage-Metering-in-Service-Provider-Foundation.md).

## Developer resources
See the [Service Provider Foundation Developer's Guide](http://go.microsoft.com/fwlink/p/?LinkID=263700) for API reference topics and guidance for programming using the [!INCLUDE[spfshort](./Token/spfshort_md.md)] web services, including the following:

-   [Windows Azure Pack Virtual Machine Roles Tenant API](http://msdn.microsoft.com/library/dn502556.aspx)

-   [Virtual Machine Management](http://msdn.microsoft.com/library/jj643294.aspx)

-   [Tenants and Users](http://msdn.microsoft.com/library/dn458381.aspx)

## Other changes
The following features and enhancements were made to [!INCLUDE[spfshort](./Token/spfshort_md.md)]:

-   HTTP is no longer supported; all web requests must use HTTPS to ensure greater security with the secure sockets layer \(SSL\).

-   When you install [!INCLUDE[spfshort](./Token/spfshort_md.md)], you now have the option to automatically generate a self\-signed certificate for use in a non\-production environment. For more information, see [How to Install Service Provider Foundation for System Center 2012 R2](./How-to-Install-Service-Provider-Foundation-for-System-Center-2012-R2.md).

-   For more efficient administration, some configurations that were in Web.config files are now stored in the SPFDB database.

## See Also
[Service Provider Foundation](./Service-Provider-Foundation.md)


