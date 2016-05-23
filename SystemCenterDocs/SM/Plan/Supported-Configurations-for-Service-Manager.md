---
title: Supported Configurations for Service Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec7184bf-732a-4a91-92ee-3a845e99e743
---
# Supported Configurations for Service Manager
This section includes information about the hardware and software requirements for [!INCLUDE[scsm_threshold_1](../../Token/scsm_threshold_1_md.md)]. [!INCLUDE[scsm_threshold_1](../../Token/scsm_threshold_1_md.md)] has been tested up to the workload described in this topic, based on the recommended hardware requirements in this guide. This environment contains one [!INCLUDE[scsm_threshold_1](../../Token/scsm_threshold_1_md.md)] management server supporting 80 to 100 concurrent [!INCLUDE[smcons](../../Token/smcons_md.md)]s. High\-performance storage using 15,000\-RPM SCSI drives is used on the database servers.

The hardware and software requirements described in the[System Requirements for System Center Technical Preview](../../System Center/System Requirements/System-Requirements-for-System-Center-Technical-Preview.md) section are based on the following system environment and conditions:

-   Up to 20,000 users, with up to 40 to 50 IT analysts providing concurrent support. Up to 50,000 users and up to 80 to 100 IT analysts can be supported if 32 gigabytes \(GB\) of memory is installed on the servers running Microsoft SQL Server.

-   Up to 20,000 supported computers, assuming up to 10 to 12 configuration items \(installed software, software updates, and hardware components\) per computer. Up to 50,000 computers can be supported if 32 GB of memory is installed on the servers running SQL Server.

-   5,000 incidents per week with three months of retention, for a total of 60,000 incidents in the [!INCLUDE[scsm_threshold_1](../../Token/scsm_threshold_1_md.md)] database for the 20,000\-computer configuration, and 2.5 times that for the 50,000\-computer configuration.

-   1,000 change requests a week with three months of retention, for a total of 12,000 change requests in the [!INCLUDE[scsm_threshold_1](../../Token/scsm_threshold_1_md.md)] database for the 20,000\-computer configuration, and 2.5 times that for the 50,000\-computer configuration.

Using a slow storage subsystem or insufficient memory can reduce [!INCLUDE[scsm_threshold_1](../../Token/scsm_threshold_1_md.md)] performance significantly.


