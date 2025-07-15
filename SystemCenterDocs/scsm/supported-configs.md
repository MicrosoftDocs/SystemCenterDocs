---
title: Supported configurations for System Center - Service Manager
description: The article describes supported configurations for Service Manager.
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.subservice: service-manager
ms.topic: concept-article
ms.custom: UpdateFrequency2, engagement-fy24
---

# Supported configurations



This article summarizes the workloads for which System Center - Service Manager is tested.

- The test environment contains one Service Manager management server supporting 80 to 100 concurrent Service Manager consoles.
- High\-performance storage using 15,000\-RPM SCSI drives was used on the database servers.

## Test conditions

The hardware and software tested are based on the following conditions:

- Up to 20,000 users, with up to 40 to 50 IT analysts providing concurrent support.
- Up to 50,000 users (and up to 80 to 100 IT analysts) can be supported. Assumes that 32 GB of memory is installed on the SQL Server machines.
- Up to 20,000 supported computers. This assumes up to 10 to 12 configuration items of installed software, software updates, and hardware components, per computer.
- Up to 50,000 computers can be supported. Assumes 32 GB of memory is installed on the SQL Server machines.  
- 5,000 incidents per week with three months of retention. Based on a total of 60,000 incidents in the Service Manager database for the 20,000\-computer configuration. Based on 2.5 times that for the 50,000\-computer configuration.  
-   1,000 change requests a week with three months of retention. Based on a total of 12,000 change requests in the Service Manager database for the 20,000\-computer configuration. Based on 2.5 times that for the 50,000\-computer configuration.  

>[!NOTE]
>Using a slow storage subsystem or insufficient memory can reduce Service Manager performance significantly.  


## Next steps

[Learn about](~/scsm/om-considerations.md) combining Operations Manager and Service Manager.
