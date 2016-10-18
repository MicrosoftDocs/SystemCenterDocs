---
title: Supported Configurations for System Center 2016 - Service Manager
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 847fcf88-bee5-49e5-a783-92ed432db3a4

---

# Supported Configurations for System Center 2016 - Service Manager

>Applies To: System Center 2016 - Service Manager

This section includes information about the hardware and software requirements for System Center 2016 - Service Manager. Service Manager has been tested up to the workload described in this topic, based on the recommended hardware requirements in this guide. This environment contains one Service Manager management server supporting 80 to 100 concurrent Service Manager consoles. High\-performance storage using 15,000\-RPM SCSI drives is used on the database servers.  

 The hardware and software requirements described in this section are based on the following system environment and conditions:  

-   Up to 20,000 users, with up to 40 to 50 IT analysts providing concurrent support. Up to 50,000 users and up to 80 to 100 IT analysts can be supported if 32 gigabytes \(GB\) of memory is installed on the servers running Microsoft SQL Server.  

-   Up to 20,000 supported computers, assuming up to 10 to 12 configuration items \(installed software, software updates, and hardware components\) per computer. Up to 50,000 computers can be supported if 32 GB of memory is installed on the servers running SQL Server.  

-   5,000 incidents per week with three months of retention, for a total of 60,000 incidents in the Service Manager database for the 20,000\-computer configuration, and 2.5 times that for the 50,000\-computer configuration.  

-   1,000 change requests a week with three months of retention, for a total of 12,000 change requests in the Service Manager database for the 20,000\-computer configuration, and 2.5 times that for the 50,000\-computer configuration.  

 Using a slow storage subsystem or insufficient memory can reduce Service Manager performance significantly.  

## Supported Configuration Topics  

-   [Hardware Requirements for System Center 2016 - Service Manager](plan-hardware-requirements-for-system-center-2016-service-manager.md)  

     Describes the hardware requirements for Service Manager.  

-   [Software Requirements for System Center 2016 - Service Manager](plan-software-requirements-for-system-center-2016-service-manager.md)  

     Describes the software requirements for Service Manager.  
