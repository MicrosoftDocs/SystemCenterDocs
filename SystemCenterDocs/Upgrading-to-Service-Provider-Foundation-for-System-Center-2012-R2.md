---
title: Upgrading to Service Provider Foundation for System Center 2012 R2
ms.custom: na
ms.prod: system-center-2012-sp1
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8b8719fb-6d30-47db-8fde-a9f185648b47
---
# Upgrading to Service Provider Foundation for System Center 2012 R2
[!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)][!INCLUDE[spflong](./Token/spflong_md.md)] is supported only on the [!INCLUDE[winblue_server_1](./Token/winblue_server_1_md.md)] operating system. Before upgrading, review [System Requirements for Service Provider Foundation 2012 R2](http://go.microsoft.com/fwlink/p/?LinkId=310174). Use the following procedure to upgrade a single or multiple installations of [!INCLUDE[spfshort](./Token/spfshort_md.md)].

## Recommended upgrade procedure
Because upgrading requires a newer operating system, you will need to uninstall  [!INCLUDE[sc2012sp1_long](./Token/sc2012sp1_long_md.md)][!INCLUDE[spfshort](./Token/spfshort_md.md)], upgrade the operating system and other prerequisites, and then install [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)][!INCLUDE[spfshort](./Token/spfshort_md.md)].

The following procedure describes preserving important configuration information.

#### To upgrade to [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)][!INCLUDE[spfshort](./Token/spfshort_md.md)]

1.  If you implemented usage metering or any other fabric management, we recommend you copy a web.config file to preserve important Operations Manager Data Warehouse \(OMDW\) settings; otherwise, skip this step.

    Copy the following file to another location. This file is removed when you uninstall any version of [!INCLUDE[spfshort](./Token/spfshort_md.md)].

    **C:\\inetpub\\SPF\\Usage\\web.config**

    [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)][!INCLUDE[spfshort](./Token/spfshort_md.md)] stores OMDW connection strings in the  [!INCLUDE[spfshort](./Token/spfshort_md.md)] database. They were previously stored in web.config files in IIS. You must add these settings to the database after installation, as described in [Configure Usage Metering in Service Provider Foundation](./Configure-Usage-Metering-in-Service-Provider-Foundation.md).

2.  Uninstall [!INCLUDE[spfshort](./Token/spfshort_md.md)][!INCLUDE[sc2012sp1_short](./Token/sc2012sp1_short_md.md)] and the [!INCLUDE[vmm12sp1_med](./Token/vmm12sp1_med_md.md)] Console.

    From **Control Panel**, in **Programs**, click **Uninstall a program**. Then under **Name**, right\-click **System Center 2012 Service Pack 1 Service Provider Foundation**, and then click **Uninstall**. Do the same for **Microsoft 2012 System Center Virtual Machine Manager Console**.

    Uninstalling [!INCLUDE[spfshort](./Token/spfshort_md.md)] does not uninstall the database \(SPFDB\) in SQL Server.

3.  Upgrade the operating system to [!INCLUDE[winblue_server_2](./Token/winblue_server_2_md.md)].

4.  Install [!INCLUDE[vmmblue_1](./Token/vmmblue_1_md.md)] Console for minimal requirements. However, you will need access to a full [!INCLUDE[vmmblue_2](./Token/vmmblue_2_md.md)] server to provide services to create fabric and provide services to tenants.

5.  Install [!INCLUDE[spfshort](./Token/spfshort_md.md)][!INCLUDE[spfshort](./Token/spfshort_md.md)].

    You can specify the name of the SQL Server that has the [!INCLUDE[spfshort](./Token/spfshort_md.md)] database on the **Configure the database server** page of the setup wizard. For more information, see [How to Install Service Provider Foundation 2012 R2](http://go.microsoft.com/fwlink/p/?LinkId=310176).

## See Also
[Deploying Service Provider Foundation](./Deploying-Service-Provider-Foundation.md)
[System Requirements for Service Provider Foundation for System Center 2012 R2](assetId:///f7c87718-29bb-4fdd-8e2d-82c81936b346)
[How to Install Service Provider Foundation for System Center 2012 R2](./How-to-Install-Service-Provider-Foundation-for-System-Center-2012-R2.md)


