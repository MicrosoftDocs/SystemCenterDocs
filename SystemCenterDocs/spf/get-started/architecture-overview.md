---

description: This article provides a broad overview of Service Provider Foundation
manager: cfreeman
ms.topic: article
author: cfreemanwa
ms.author: cfreemanms
ms.prod: system-center-threshold
ms.tgt_pltfrm: na
ms.date:  2016-10-12
title: Architecture Overview of Service Provider Foundation
ms.technology: service-provider-foundation
ms.assetid: 0cce9ea6-adf3-422d-94c0-2bf15b0c1d95

---
# Architecture Overview of Service Provider Foundation
>Applies To: System Center 2016

Service providers can use Service Provider Foundation technology to offer infrastructure as a service \(IaaS\) to their clients. If a service provider has a front\-end portal for clients to interact with, Service Provider Foundation makes it possible for the clients to access the resources on their hosting provider's system without making changes to the portal.  

## Overview Diagram
The following illustration provides a high\-level view of how Service Provider Foundation operates.  

![Overview of Service Provider Foundation](../spf/media/SPFOverview.png "SPFOverview")  

The tenant represents a hoster's customer, and the tenant has assets on the hoster's system. Each tenant has their own administrators, applications, scripts, and other tools.  

The hoster provides tenants with the environment, which can include virtual machines. The hoster has an existing front\-end portal, which all tenants can use. On the back end, the hoster has a collection of resources, which is called the *fabric*. The hoster allocates those resources into discrete groups according to the hoster's needs. Each of these groups is known as a *stamp*. The hoster can then assign the tenant's resources to stamps in whatever manner is appropriate to the hoster. The resources may be divided across several stamps, according to the hoster's business model scheme. Service Provider Foundation makes it possible for the hoster to present a seamless user experience to the tenant by aggregating the data from each stamp and allowing the tenant to use the Service Provider Foundation application programming interfaces \(APIs\) to access that data.  

A stamp in Service Provider Foundation is a logical scale unit designed for scalability that provides an association between a server and its System Center 2016 components. As tenant demand increases, the hoster provides additional stamps to meet the demand. Note that Service Provider Foundation System Center 2016 supported only one type of stamp; that is a single server that has Virtual Machine Manager \(VMM\) installed.  

Service Provider Foundation does not configure clouds; instead, it manages their resources. Virtual machines are set to clouds, for example, when they are created for VMM or when they are created by the T:Microsoft.SystemCenter.VirtualMachineManager.Cmdlets.New\-SCVirtualMachine cmdlet.  

![Architecture of Service Provider Foundation](../spf/media/SPFArchitecture.png "SPFArchitecture")  

The hoster can have a portal client, which faces the tenant, that provides access to the infrastructure that the hoster has granted. The portal uses an extensible representational state transfer \(REST\) API to communicate with the web service by using the OData protocol. The claims\-based authentication verifies the tenant's identity and associates it with the user role that the hoster assigns.  

Service Provider Foundation uses a database to aggregate the tenant resources, which are managed with Windows PowerShell scripts and Orchestrator   runbooks. This makes it possible for the hoster to distribute tenant resources among management stamps in whatever way it decides, while to the tenant the resources are easy to access and appear contiguous.  

## See Also  
[Deploying Service Provider Foundation](../Deploy/Deploying-Service-Provider-Foundation.md)  
[Integrating Service Management Portal and API with System Center 2016](http://go.microsoft.com/fwlink/?LinkId=298454)  
[Cloud Resource Management with System Center 2016 - Orchestrator and Service Provider Foundation](http://go.microsoft.com/fwlink/p/?LinkId=263682)  
[Cmdlets in System Center 2016 - Service Provider Foundation](http://go.microsoft.com/fwlink/p/?LinkId=263677)  
[Service Provider Foundation Developer's Guide](http://go.microsoft.com/fwlink/p/?LinkID=263700)  
