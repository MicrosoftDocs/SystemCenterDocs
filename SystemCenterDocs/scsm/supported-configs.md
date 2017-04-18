---
title: Supported configurations for Service Manager
description: The article describes supported configurations for Service Manager.
ms.custom: na
ms.prod: system-center-2016
manager: carmonm
author: bandersmsft
ms.author: banders
ms.date: 02/06/2017
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 847fcf88-bee5-49e5-a783-92ed432db3a4

---

# Supported configurations for System Center 2016 - Service Manager

>Applies To: System Center 2016 - Service Manager

Service Manager has been tested up to the workload described in this topic, based on recommended hardware. The test environment contains one Service Manager management server supporting 80 to 100 concurrent Service Manager consoles. High\-performance storage using 15,000\-RPM SCSI drives is used on the database servers.  

The hardware and software tested are based on the following system environment and conditions:  

-   Up to 20,000 users, with up to 40 to 50 IT analysts providing concurrent support. Up to 50,000 users and up to 80 to 100 IT analysts can be supported if 32 gigabytes \(GB\) of memory is installed on the servers running Microsoft SQL Server.  

-   Up to 20,000 supported computers, assuming up to 10 to 12 configuration items \(installed software, software updates, and hardware components\) per computer. Up to 50,000 computers can be supported if 32 GB of memory is installed on the servers running SQL Server.  

-   5,000 incidents per week with three months of retention, for a total of 60,000 incidents in the Service Manager database for the 20,000\-computer configuration, and 2.5 times that for the 50,000\-computer configuration.  

-   1,000 change requests a week with three months of retention, for a total of 12,000 change requests in the Service Manager database for the 20,000\-computer configuration, and 2.5 times that for the 50,000\-computer configuration.  

>[!NOTE]
>Using a slow storage subsystem or insufficient memory can reduce Service Manager performance significantly.  


## Next steps

- Review [Considerations for Operations Manager with Service Manager](om-considerations.md) to learn about possible issues before you combine Operations Manager and Service Manager.
