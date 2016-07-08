---
title: Upgrading System Center 2012 - Service Manager to System Center 2012 SP1
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae385dce-3613-47b5-88a4-1b3148f2cce1
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Upgrading System Center 2012 - Service Manager to System Center 2012 SP1
This guide will show you how to upgrade from [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] to [!INCLUDE[smshort12](../../../sm/deploy/deploy-guide/includes/smshort12_md.md)] in [!INCLUDE[sc2012sp1_long](../../../sm/deploy/upgrade/includes/sc2012sp1_long_md.md)].  
  
> [!WARNING]  
>  If you are planning to upgrade two or more System Center components, it is imperative that you first consult the guide [Upgrade Sequencing for System Center 2012 SP1](http://go.microsoft.com/fwlink/p/?LinkId=268417). The order in which you perform component upgrades is important. Failure to follow the correct upgrade sequence might result in component failure for which no recovery options exist. The affected System Center components are:  
>   
>  1.  [!INCLUDE[orchshort](../../../sm/deploy/upgrade/includes/orchshort_md.md)]  
> 2.  [!INCLUDE[smshort12](../../../sm/deploy/deploy-guide/includes/smshort12_md.md)]  
> 3.  [!INCLUDE[dpm2012sp1long](../../../sm/deploy/upgrade/includes/dpm2012sp1long_md.md)]  
> 4.  [!INCLUDE[om12short](../../../sm/deploy/upgrade/includes/om12short_md.md)]  
> 5.  [!INCLUDE[cmshort](../../../sm/deploy/upgrade/includes/cmshort_md.md)]  
> 6.  [!INCLUDE[vmm12sp1_med](../../../sm/deploy/upgrade/includes/vmm12sp1_med_md.md)]  
> 7.  [!INCLUDE[conceroshort](../../../sm/deploy/upgrade/includes/conceroshort_md.md)]  
  
 You can only upgrade to [!INCLUDE[sc2012sp1_long](../../../sm/deploy/upgrade/includes/sc2012sp1_long_md.md)] from System Center 2012 – Service Manager \(version 7.5.1561.0.0\)  
  
> [!IMPORTANT]  
>  It is assumed in this guide that you are performing an *upgrade* to [!INCLUDE[sc2012sp1_long](../../../sm/deploy/upgrade/includes/sc2012sp1_long_md.md)]. For information about installing [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] on a computer where no previous version of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] exists, see the [Deploying  System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209670).  
  
## Upgrade topics  
  
-   [Upgrade Planning for System Center 2012 SP1 \- Service Manager](../../../sm/deploy/upgrade/Upgrade-Planning-for-System-Center-2012-SP1---Service-Manager.md)  
  
     Describes factors that you must consider before you start the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] upgrade.  
  
-   [Setting Up a Service Manager 2012 Lab Environment with Production Data](../../../sm/deploy/upgrade/Setting-Up-a-Service-Manager-2012-Lab-Environment-with-Production-Data.md)  
  
     Describes how to setup [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] in a lab environment using production data.  
  
-   [Upgrade to System Center 2012 SP1 \- Service Manager](../../../sm/deploy/upgrade/Upgrade-to-System-Center-2012-SP1---Service-Manager.md)  
  
     Describes the steps that you must take to upgrade System Center 2012 to [!INCLUDE[sc2012sp1_short](../../../sm/deploy/upgrade/includes/sc2012sp1_short_md.md)].  
  
-   [After Upgrading to System Center 2012 SP1 \- Service Manager](../../../sm/deploy/upgrade/After-Upgrading-to-System-Center-2012-SP1---Service-Manager.md)  
  
     Describes the steps that you must take after you have applied the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] upgrade.  
  
-   [Failed Upgrade in System Center 2012 SP1 \- Service Manager](../../../sm/deploy/upgrade/Failed-Upgrade-in-System-Center-2012-SP1---Service-Manager.md)  
  
     Describes the steps you can take if an upgrade fails.  
  
## Downloadable Documentation  
 You can download a [copy of this technical documentation from the Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=246620).  Always use the TechNet library for the most up\-to\-date information.