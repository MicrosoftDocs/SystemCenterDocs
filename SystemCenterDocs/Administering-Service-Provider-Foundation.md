---
title: Administering Service Provider Foundation
ms.custom: na
ms.prod: system-center-2012-sp1
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 380f5828-54f2-4280-9794-4a8126e52534
---
# Administering Service Provider Foundation
A tenant in [!INCLUDE[spflong]./Token/spflong_md.md)] is a customer of a hoster, and the customer is maintained in the database together with its status, metadata, and with one or more of the following associations:

-   To a stamp.

    A stamp in [!INCLUDE[spfshort]./Token/spfshort_md.md)] is a logical scale unit designed for scalability that provides an association between a server and its [!INCLUDE[sc2012sp1_long]./Token/sc2012sp1_long_md.md)]components. As tenant demand increases, the hoster provides additional stamps to meet the demand. Currently, [!INCLUDE[spflong]./Token/spflong_md.md)] supports only one type of stamp; that is a single server that has Virtual Machine Manager \(VMM\) installed.

-   To a trusted issuer and a public key.

    A public key to a certificate and the name of the trusted issuer can be specified for a tenant when the tenant is created.

-   To an offer.

    Offers provide associations for a provider's plan to stamps and tenants.

-   To tenant security user roles.

    A Tenant Administrator Role and one or more Tenant Self\-Service user roles can be associated with a tenant.

## Administering topics

-   [Recommended Administrator Capabilities in Service Provider Foundation](./Recommended-Administrator-Capabilities-in-Service-Provider-Foundation.md)

    Specifies recommended permissions for [!INCLUDE[spfshort]./Token/spfshort_md.md)] administrators, database administrators, and application pool users.

-   [Manage Web Services and Connections in Service Provider Foundation](./Manage-Web-Services-and-Connections-in-Service-Provider-Foundation.md)

    Provides a comprehensive overview of the web services, credentials, and connectivity required to administer [!INCLUDE[spfshort]./Token/spfshort_md.md)] .

-   [Manage Certificates and User Roles in Service Provider Foundation](./Manage-Certificates-and-User-Roles-in-Service-Provider-Foundation.md)

    Provides an overview of how multi\-tenant security is implemented in [!INCLUDE[spfshort]./Token/spfshort_md.md)]. This section contains a walkthrough topic with procedures on creating and managing a tenant's certificate and defining tenant administrator and tenant self\-service user roles. In addition, topics describe recommended administrator capabilities and an example of a token authentication.

-   [Portals in Service Provider Foundation](./Portals-in-Service-Provider-Foundation.md)

    Describes how client and portal applications can communicate with and obtain services from [!INCLUDE[spfshort]./Token/spfshort_md.md)]. This section also contains procedures for configuring [!INCLUDE[conceroshort]./Token/conceroshort_md.md)] and [!INCLUDE[katal_long]./Token/katal_long_md.md)].

-   [Usage Metering in Service Provider Foundation](./Usage-Metering-in-Service-Provider-Foundation.md)

    Describes how [!INCLUDE[spfshort]./Token/spfshort_md.md)] provides usage metering data of virtual machine usage by tenants.

-   [Extensibility in Service Provider Foundation](./Extensibility-in-Service-Provider-Foundation.md)

    Describes how to have an runbook in [!INCLUDE[orchlong]./Token/orchlong_md.md)] invoked by [!INCLUDE[spfshort]./Token/spfshort_md.md)].

## Other resources for this component

-   TechNet Library main page for [Service Provider Foundation](./Service-Provider-Foundation.md)

-   [Deploying Service Provider Foundation](./Deploying-Service-Provider-Foundation.md)

-   [Architecture Overview of Service Provider Foundation](./Architecture-Overview-of-Service-Provider-Foundation.md)

-   [Cmdlets in System Center 2012 \- Service Provider Foundation](http://go.microsoft.com/fwlink/p/?LinkId=263677)

-   [Service Provider Foundation Developer's Guide](http://go.microsoft.com/fwlink/p/?LinkID=263700)



