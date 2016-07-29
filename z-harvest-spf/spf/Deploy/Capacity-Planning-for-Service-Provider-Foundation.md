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
5 GB is sufficient storage for even large Service Provider Foundation databases.  
  
## Hardware recommendations for servers  
The following server scenarios each pertain to the recommendations listed in the following table.  
  
-   --- translation.priority.ht:    - cs-cz   - da-dk   - de-de   - el-gr   - es-es   - fi-fi   - fr-fr   - hu-hu   - it-it   - ja-jp   - ko-kr   - nb-no   - nl-nl   - pl-pl   - pt-br   - pt-pt   - ru-ru   - sv-se   - tr-tr   - zh-cn   - zh-hk   - zh-tw --- Virtual Machine Manager \(VMM\) with or without SQL Server  
  
-   Service Provider Foundation with or without SQL Server  
  
-   App Controller  with or without SQL Server  
  
|5,000 or Fewer Virtual Machines|5,000 - 12,000 Virtual Machines|12,000 - 25,000 Virtual Machines|  
|-----------------------------------|-----------------------------------|------------------------------------|  
|4 processor cores, 8 GB RAM|8 processor cores, 8 GB RAM.<br /><br />4 processor cores, 8 GB RAM is sufficient for computers running App Controller  with or without SQL Server.|16 processor cores, 8 GB RAM recommended only for computers running --- translation.priority.ht:    - ar-sa   - cs-cz   - da-dk   - de-de   - el-gr   - es-es   - fi-fi   - fr-fr   - he-il   - hu-hu   - it-it   - ja-jp   - ko-kr   - nb-no   - nl-nl   - pl-pl   - pt-br   - pt-pt   - ro-ro   - ru-ru   - sv-se   - tr-tr   - zh-cn   - zh-hk   - zh-tw --- VMM with or without SQL Server.|  
  
## Web service settings  
By default, Service Provider Foundation supports up to 1000 concurrent requests for its web services. We recommend this be a lower number in a production environment. You can change this configuration by specifying the value for the **MaxRequestsPerTimeSlot** key in the **C:\\inetpub\\SPF\\web.config** file.  
  
## See Also  
[System Requirements for Service Provider Foundation for System Center 2012 SP1](../../spf/Deploy/System-Requirements-for-Service-Provider-Foundation-for-System-Center-2012-SP1.md)  
[How to Install Service Provider Foundation for System Center 2012 SP1](../../spf/Deploy/How-to-Install-Service-Provider-Foundation-for-System-Center-2012-SP1.md)  
[Security Planning for Service Provider Foundation](../../spf/Deploy/Security-Planning-for-Service-Provider-Foundation.md)  
[Deploying Service Provider Foundation](../../spf/Deploy/Deploying-Service-Provider-Foundation.md)  
[Administering Service Provider Foundation](../../spf/Deploy/Administering-Service-Provider-Foundation.md)  
  
