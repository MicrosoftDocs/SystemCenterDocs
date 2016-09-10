---
title: Portals in Service Provider Foundation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6d69f4df-9b24-4214-9714-2c838c5cd5f8
author:bwren
ms.author: raynew
manager:cfreeman
---
# Portals in Service Provider Foundation
Service Provider Foundation provides services for multiple tenants who receive IaaS through portal applications, and uniquely identifies each tenant and isolates them from one another. Portals communicate with the Service Provider Foundation Admin and VMM services through REST APIs as described in the [Service Provider Foundation Developer's Guide](http://go.microsoft.com/fwlink/p/?LinkID=263700).  

The following illustration shows how portal applications and Windows PowerShell interact with Service Provider Foundation.  

![Shows portals to Service Provider Foundation](../media/Orch2016_SPF_Portals.png "Orch2016_SPF_Portals")  

## Portal topics  

-   [Configuring Portals for Service Provider Foundation](../Deploy/Configuring-Portals-for-Service-Provider-Foundation.md)  

    Describes the configurations required for Windows Azure Pack for Windows Server .  

-   [Importing Gallery Items in Service Provider Foundation](../Manage/Importing-Gallery-Items.md)  

    Describes how to use Windows PowerShell cmdlets to import gallery items from downloaded packages so they can be easily accessible by portal applications.  

-   [How to Configure the System Center Resource Provider for Windows Azure Pack](../Manage/How-to-Configure-the-System-Center-Resource-Provider-for-Windows-Azure-Pack.md)  

    Describes how to use Windows PowerShell cmdlets to change the endpoints for Windows Azure Pack in case a different installation of Service Provider Foundation is required.  

## Other resources for this component     

-   [Deploying Service Provider Foundation](../Deploy/Deploying-Service-Provider-Foundation.md)  
