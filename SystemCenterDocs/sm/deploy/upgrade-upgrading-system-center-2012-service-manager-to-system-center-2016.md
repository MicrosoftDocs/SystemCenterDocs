---
title: Upgrading System Center 2012 R2 - Service Manager to System Center 2016
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae385dce-3613-47b5-88a4-1b3148f2cce1
---

# Upgrading System Center 2012 R2 - Service Manager to System Center 2016

>Applies To: System Center 2016 - Service Manager

This guide will show you how to upgrade from System Center 2012 R2 - Service Manager to Service Manager in System Center 2016.  

> [!WARNING]  
>  If you are planning to upgrade two or more System Center components, it is imperative that you first consult the guide [Upgrade Sequencing for System Center](http://go.microsoft.com/fwlink/p/?LinkId=268417). The order in which you perform component upgrades is important. Failure to follow the correct upgrade sequence might result in component failure for which no recovery options exist. The affected System Center components are:  
>   
> 1.  Orchestrator  
> 2.  Service Manager  
> 3.  Data Protection Manager  
> 4.  Operations Manager  
> 5.  Configuration Manager  
> 6.  Virtual Machine Manager  
> 7.  App Controller  

 You can only upgrade to System Center 2016 from System Center 2012 R2 - Service Manager \(version 7.5.1561.0.0\)  

> [!IMPORTANT]  
>  It is assumed in this guide that you are performing an *upgrade* to System Center 2012 R2. For information about installing System Center 2016 - Service Manager on a computer where no previous version of Service Manager exists, see the [Deploying System Center 2016 - Service Manager](deploy-deploying-system-center-2016-service-manager.md).  


## Recommendations for Upgrading to Service Manager 2016

- Refer to [System Requirements for System Center](../../system-requirements/system-requirements.md)
- Upgrade Service Manager 2012 R2 to Service Manger 2016 first, then upgrade your operating system to Windows Server 2016.
- The order that you upgrade SQL Server and the server operating system should not matter.
- For Service Manager data warehouse database restoration, the Reporting database also needs to be restored **after** you install the data warehouse.
- Use the published information for the order of System Center components as well as Service Manager components.
- Do not mix Service Manager 2016 and Service Manager 2012 R2 with different Service Manager components - all should use the same version. For example, both the Self Service portal and the Service Manager management server  should use the same version.
- You can only use the Service Manager 2012 R2 old or new portal with Service Manager 2012 R2. You cannot use the Self Service portal in Service Manager 2016 with Service Manager 2012 R2.
- When upgrading from Service Manager 2012 R2 to Service Manager 2016, you should not enable or disable the Active Directory group expansion for any of the Active Directory connectors.

    In other words, if it is off, let it remain off and if it is on, let it remain on until the connector runs for the first time. See the screenshot below. This applies only to the first time that the Active Directory connector runs after you upgrade. You can change your preferences for Active Directory group expansion workflow after the first time that the Active Directory connector sync completes.

    ![Active Directory Connector wizard](../media/sm-adconnector01.png)
