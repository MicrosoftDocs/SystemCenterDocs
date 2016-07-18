---
title: Deployment Scenarios for System Center 2012 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91a72f45-07ff-41cd-80aa-7acde988f08f
 

















---
# Deployment Scenarios for System Center 2012 - Service Manager
System Center 2012 - Service Manager provides for many deployment scenarios. However, remember that you cannot deploy a Service Manager management server and a data warehouse management server on the same computer. In fact, Setup prevents you from installing both on a single server. The reason has to do with Service Manager architecture of the data warehouse, overall performance, and usage of the Operations Manager health service. The data warehouse was designed for quick data retrieval and hosting both the Service Manager management server and the data warehouse management server on a single server will negatively impact performance for both. Additionally, a single server doesn’t scale out as Service Manager usage and data storage grow.  
  
 You will also specify the server that hosts SQL Server Reporting Services \(SSRS\). Do not attempt to use the same SSRS instance for both Operations Manager and Service Manager.  
  
 This deployment guide describes the following three deployment scenarios: installing Service Manager on one computer, installing Service Manager on two computers, and installing Service Manager on four computers.  
  
> [!NOTE]  
>  The collation settings for Microsoft SQL Server must be the same for the computers that host the Service Manager database, the computers that host the data warehouse databases, and the computers that host the Reporting Services database. If you intend to import data from Operations Manager, then the database collations must match between Service Manager and Operations Manager.  
  
 While we do not recommend it \(for performance reasons\), if you want to host the Service Manager management server and the Self-Service Portal on the same computer, you must deploy the Service Manager management server before you deploy the Self-Service Portal.  
  
 Performing an upgrade from previous versions of Service Manager to Service Manager Community Technology Preview 1 \(CTP1\) is not supported. Furthermore, for this release, Service Manager setup installs files in predefined folders that might already exist if you have a previous version of Service Manager installed.  
  
 The user installing Service Manager has access to the Service Connection Point \(SCP\) object of Service Manager in the Active Directory. This SCP stores the information about the service. Client applications, such as Service Manager, can connect to services using the SCP. For more information about service connection points, see [Publishing Services in Active Directory](http://technet.microsoft.com/library/cc961733.aspx).  
  
## Deployment Scenario Topics  
  
-   [Installing Service Manager on a Single Computer \(Minimum Configuration\)](assetId:///c433f031-f876-4a29-b4b7-812bebae952a)  
  
     Describes how to install Service Manager on a single computer. This scenario requires you to use a virtual machine for the data warehouse management server. This scenario is useful for evaluation purposes.  
  
-   [Installing Service Manager on Two Computers](assetId:///06fe6de2-3084-4e83-a767-be2282afb962)  
  
     Describes how to install Service Manager on two computers. This scenario is useful for testing Service Manager in a lab environment.  
  
-   [Installing Service Manager on Four Computers](assetId:///194d3520-8a38-40b8-995c-9619fc78cb56)  
  
     Describes how to install Service Manager on four computers. This scenario is useful in a production environment, and it maximizes performance and scalability.  
  
-   [Manual Steps to Configure the Remote SQL Server Reporting Services](../../../sm/deploy/deploy-guide/Manual-Steps-to-Configure-the-Remote-SQL-Server-Reporting-Services.md)  
  
     Describes how to manually configure SSRS in situations where SSRS is not on the same server as the data warehouse management server.  
  
-   [Manual Steps to Prepare Upgraded SQL Server](../../../sm/deploy/deploy-guide/Manual-Steps-to-Prepare-Upgraded-SQL-Server.md)  
  
     Describes how to manually configure an upgraded version of SQL Server 2012 to enable SQL Server Reporting Services.  
  
-   [How to Create and Deploy Server Images of Service Manager](../../../sm/deploy/deploy-guide/How-to-Create-and-Deploy-Server-Images-of-Service-Manager.md)  
  
     Describes how to create and deploy server images of Service Manager.  
  
## Other Resources for This Component  
  
-   TechNet Library main page for [System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220655)  
  
-   [Operations Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220656)  
  
-   [Administrator's Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209669)  
  
-   [Planning Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209672)
