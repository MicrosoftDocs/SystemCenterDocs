---
title: Upgrading to Service Provider Foundation for System Center 2012 R2
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8b8719fb-6d30-47db-8fde-a9f185648b47
author:bwren
manager:cfreemanwa
---
# Upgrading to Service Provider Foundation for System Center 2012 R2
[!INCLUDE[sc2012r2_1](../../om/manage/includes/sc2012r2_1_md.md)]Service Provider Foundation is supported only on the Windows ServerÂ® 2012 R2 operating system. Before upgrading, review [System Requirements for Service Provider Foundation 2012 R2](http://go.microsoft.com/fwlink/p/?LinkId=310174). Use the following procedure to upgrade a single or multiple installations of Service Provider Foundation.  
  
## Recommended upgrade procedure  
Because upgrading requires a newer operating system, you will need to uninstall  [!INCLUDE[sc2012sp1_long](../../om/manage/includes/sc2012sp1_long_md.md)]Service Provider Foundation, upgrade the operating system and other prerequisites, and then install [!INCLUDE[sc2012r2_1](../../om/manage/includes/sc2012r2_1_md.md)]Service Provider Foundation.  
  
The following procedure describes preserving important configuration information.  
  
#### To upgrade to [!INCLUDE[sc2012r2_1](../../om/manage/includes/sc2012r2_1_md.md)]Service Provider Foundation  
  
1.  If you implemented usage metering or any other fabric management, we recommend you copy a web.config file to preserve important Operations Manager Data Warehouse \(OMDW\) settings; otherwise, skip this step.  
  
    Copy the following file to another location. This file is removed when you uninstall any version of Service Provider Foundation.  
  
    **C:\\inetpub\\SPF\\Usage\\web.config**  
  
    [!INCLUDE[sc2012r2_1](../../om/manage/includes/sc2012r2_1_md.md)]Service Provider Foundation stores OMDW connection strings in the  Service Provider Foundation database. They were previously stored in web.config files in IIS. You must add these settings to the database after installation, as described in [Configure Usage Metering in Service Provider Foundation](../../spf/Deploy/Configure-Usage-Metering-in-Service-Provider-Foundation.md).  
  
2.  Uninstall Service Provider Foundation[!INCLUDE[sc2012sp1_short](../../om/manage/includes/sc2012sp1_short_md.md)] and the [!INCLUDE[vmm12sp1_med](../../om/manage/includes/vmm12sp1_med_md.md)] Console.  
  
    From **Control Panel**, in **Programs**, click **Uninstall a program**. Then under **Name**, right\-click **System Center 2012 Service Pack 1 Service Provider Foundation**, and then click **Uninstall**. Do the same for **Microsoft 2012 System Center Virtual Machine Manager Console**.  
  
    Uninstalling Service Provider Foundation does not uninstall the database \(SPFDB\) in SQL Server.  
  
3.  Upgrade the operating system to Windows Server 2012 R2.  
  
4.  Install [!INCLUDE[vmmblue_1](../../om/manage/includes/vmmblue_1_md.md)] Console for minimal requirements. However, you will need access to a full [!INCLUDE[vmmblue_2](../../om/manage/includes/vmmblue_2_md.md)] server to provide services to create fabric and provide services to tenants.  
  
5.  Install Service Provider FoundationService Provider Foundation.  
  
    You can specify the name of the SQL Server that has the Service Provider Foundation database on the **Configure the database server** page of the setup wizard. For more information, see [How to Install Service Provider Foundation 2012 R2](http://go.microsoft.com/fwlink/p/?LinkId=310176).  
  
## See Also  
[Deploying Service Provider Foundation](../../spf/Deploy/Deploying-Service-Provider-Foundation.md)  
[System Requirements for Service Provider Foundation for System Center 2012 R2](assetId:///f7c87718-29bb-4fdd-8e2d-82c81936b346)  
[How to Install Service Provider Foundation for System Center 2012 R2](../../spf/Deploy/How-to-Install-Service-Provider-Foundation-for-System-Center-2012-R2.md)  
  
