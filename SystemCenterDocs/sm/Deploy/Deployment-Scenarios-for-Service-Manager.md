---
title: Deployment Scenarios for Service Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 037167a4-a9c3-49f4-9232-c76ea32a68a9
---
# Deployment Scenarios for Service Manager
System Center 2016 Technical Preview \- Service Manager provides for many deployment scenarios. However, remember that you cannot deploy a Service Manager management server and a data warehouse management server on the same computer. In fact, Setup prevents you from installing both on a single server. The reason has to do with Service Manager architecture of the data warehouse, overall performance, and usage of the Operations Manager health service. The data warehouse was designed for quick data retrieval and hosting both the Service Manager management server and the data warehouse management server on a single server will negatively impact performance for both. Additionally, a single server doesn’t scale out as Service Manager usage and data storage grow.

You will also specify the server that hosts SQL Server Reporting Services \(SSRS\). Do not attempt to use the same SSRS instance for both Operations Manager and Service Manager.

This deployment guide describes the following three deployment scenarios: installing Service Manager on one computer, installing Service Manager on two computers, and installing Service Manager on four computers.

> [!NOTE]
> The collation settings for Microsoft SQL Server must be the same for the computers that host the Service Manager database, the computers that host the data warehouse databases, and the computers that host the Reporting Services database. If you intend to import data from Operations Manager, then the database collations must match between Service Manager and Operations Manager.

While we do not recommend it \(for performance reasons\), if you want to host the Service Manager management server and the Self\-Service Portal on the same computer, you must deploy the Service Manager management server before you deploy the Self\-Service Portal.

The user installing Service Manager has access to the Service Connection Point \(SCP\) object of Service Manager in the Active Directory. This SCP stores the information about the service. Client applications, such as Service Manager, can connect to services using the SCP. For more information about service connection points, see [Publishing Services in Active Directory](http://technet.microsoft.com/library/cc961733.aspx).

## Deployment Scenario Topics

-   [How to Install the Service Manager Management Server &#40;Two-Computer Scenario&#41;](How-to-Install-the-Service-Manager-Management-Server--Two-Computer-Scenario-.md)

    Describes how to install Service Manager on two computers. This scenario is useful for testing Service Manager in a lab environment.

-   [How to Install the Service Manager Management Server &#40;Four-Computer Scenario&#41;](How-to-Install-the-Service-Manager-Management-Server--Four-Computer-Scenario-.md)

    Describes how to install Service Manager on four computers. This scenario is useful in a production environment, and it maximizes performance and scalability.

-   [How to Install the Service Manager Data Warehouse &#40;Two-Computer Scenario&#41;](How-to-Install-the-Service-Manager-Data-Warehouse--Two-Computer-Scenario-.md)

    Describes how to install the data warehouse on two computers.

-   [How to Install the Service Manager Data Warehouse &#40;Four-Computer Scenario&#41;](How-to-Install-the-Service-Manager-Data-Warehouse--Four-Computer-Scenario-.md)

    Describes how to install the data warehouse on four computers.


