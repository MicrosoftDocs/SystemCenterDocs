---
title: Administering Service Provider Foundation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 380f5828-54f2-4280-9794-4a8126e52534
author:bwren
manager:cfreemanwa
---
# Administering Service Provider Foundation
A tenant in [!INCLUDE[spflong](../../spf/Deploy/includes/spflong_md.md)] is a customer of a hoster, and the customer is maintained in the database together with its status, metadata, and with one or more of the following associations:  
  
-   To a stamp.  
  
    A stamp in [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] is a logical scale unit designed for scalability that provides an association between a server and its [!INCLUDE[sc2012sp1_long](../../om/manage/includes/sc2012sp1_long_md.md)]components. As tenant demand increases, the hoster provides additional stamps to meet the demand. Currently, [!INCLUDE[spflong](../../spf/Deploy/includes/spflong_md.md)] supports only one type of stamp; that is a single server that has Virtual Machine Manager \(VMM\) installed.  
  
-   To a trusted issuer and a public key.  
  
    A public key to a certificate and the name of the trusted issuer can be specified for a tenant when the tenant is created.  
  
-   To an offer.  
  
    Offers provide associations for a provider's plan to stamps and tenants.  
  
-   To tenant security user roles.  
  
    A Tenant Administrator Role and one or more Tenant Self\-Service user roles can be associated with a tenant.  
  
## Administering topics  
  
-   [Recommended Administrator Capabilities in Service Provider Foundation](../../spf/Deploy/Recommended-Administrator-Capabilities-in-Service-Provider-Foundation.md)  
  
    Specifies recommended permissions for [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] administrators, database administrators, and application pool users.  
  
-   [Manage Web Services and Connections in Service Provider Foundation](../../spf/Deploy/Manage-Web-Services-and-Connections-in-Service-Provider-Foundation.md)  
  
    Provides a comprehensive overview of the web services, credentials, and connectivity required to administer [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] .  
  
-   [Manage Certificates and User Roles in Service Provider Foundation](../../spf/Deploy/Manage-Certificates-and-User-Roles-in-Service-Provider-Foundation.md)  
  
    Provides an overview of how multi\-tenant security is implemented in [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)]. This section contains a walkthrough topic with procedures on creating and managing a tenant's certificate and defining tenant administrator and tenant self\-service user roles. In addition, topics describe recommended administrator capabilities and an example of a token authentication.  
  
-   [Portals in Service Provider Foundation](../../spf/Deploy/Portals-in-Service-Provider-Foundation.md)  
  
    Describes how client and portal applications can communicate with and obtain services from [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)]. This section also contains procedures for configuring [!INCLUDE[conceroshort](../../om/manage/includes/conceroshort_md.md)] and [!INCLUDE[katal_long](../../spf/Deploy/includes/katal_long_md.md)].  
  
-   [Usage Metering in Service Provider Foundation](../../spf/Deploy/Usage-Metering-in-Service-Provider-Foundation.md)  
  
    Describes how [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] provides usage metering data of virtual machine usage by tenants.  
  
-   [Extensibility in Service Provider Foundation](../../spf/Deploy/Extensibility-in-Service-Provider-Foundation.md)  
  
    Describes how to have an runbook in [!INCLUDE[orchlong](../../orch/deploy/includes/orchlong_md.md)] invoked by [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)].  
  
## Other resources for this component  
  
-   TechNet Library main page for [Service Provider Foundation](../../spf/Deploy/Service-Provider-Foundation.md)  
  
-   [Deploying Service Provider Foundation](../../spf/Deploy/Deploying-Service-Provider-Foundation.md)  
  
-   [Architecture Overview of Service Provider Foundation](../../spf/Deploy/Architecture-Overview-of-Service-Provider-Foundation.md)  
  
-   [Cmdlets in System Center 2012 \- Service Provider Foundation](http://go.microsoft.com/fwlink/p/?LinkId=263677)  
  
-   [Service Provider Foundation Developer's Guide](http://go.microsoft.com/fwlink/p/?LinkID=263700)  
  
