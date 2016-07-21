---
title: Capacity Planning for Service Provider Foundation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 617ee2c1-4dea-40e6-85b3-d87b15c0221d
author:bwren
manager:cfreemanwa
---
# Capacity Planning for Service Provider Foundation
This topic provides database and resource recommendations to accommodate tenant usage of up to 25,000 virtual machines.  
  
## Database storage  
5 GB is sufficient storage for even large [!INCLUDE[spflong](../../spf/Deploy/includes/spflong_md.md)] databases.  
  
## Hardware recommendations for servers  
The following server scenarios each pertain to the recommendations listed in the following table.  
  
-   [!INCLUDE[vmm12sp1_long](../../spf/Deploy/includes/vmm12sp1_long_md.md)] with or without SQL Server  
  
-   [!INCLUDE[spflong](../../spf/Deploy/includes/spflong_md.md)] with or without SQL Server  
  
-   [!INCLUDE[conceroshort](../../om/manage/includes/conceroshort_md.md)] with or without SQL Server  
  
|5,000 or Fewer Virtual Machines|5,000 - 12,000 Virtual Machines|12,000 - 25,000 Virtual Machines|  
|-----------------------------------|-----------------------------------|------------------------------------|  
|4 processor cores, 8 GB RAM|8 processor cores, 8 GB RAM.<br /><br />4 processor cores, 8 GB RAM is sufficient for computers running [!INCLUDE[conceroshort](../../om/manage/includes/conceroshort_md.md)] with or without SQL Server.|16 processor cores, 8 GB RAM recommended only for computers running [!INCLUDE[vmm12short](../../spf/Deploy/includes/vmm12short_md.md)] with or without SQL Server.|  
  
## Web service settings  
By default, [!INCLUDE[spflong](../../spf/Deploy/includes/spflong_md.md)] supports up to 1000 concurrent requests for its web services. We recommend this be a lower number in a production environment. You can change this configuration by specifying the value for the **MaxRequestsPerTimeSlot** key in the **C:\\inetpub\\SPF\\web.config** file.  
  
## See Also  
[System Requirements for Service Provider Foundation for System Center 2012 SP1](../../spf/Deploy/System-Requirements-for-Service-Provider-Foundation-for-System-Center-2012-SP1.md)  
[How to Install Service Provider Foundation for System Center 2012 SP1](../../spf/Deploy/How-to-Install-Service-Provider-Foundation-for-System-Center-2012-SP1.md)  
[Security Planning for Service Provider Foundation](../../spf/Deploy/Security-Planning-for-Service-Provider-Foundation.md)  
[Deploying Service Provider Foundation](../../spf/Deploy/Deploying-Service-Provider-Foundation.md)  
[Administering Service Provider Foundation](../../spf/Deploy/Administering-Service-Provider-Foundation.md)  
  
