---
title: Recommended Administrator Capabilities in Service Provider Foundation
description: This topic describes the various roles required to support Service Provider Foundation.
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.date: 8-18-2016
ms.topic: article
ms.assetid: 1ca67a42-81f9-4df4-ba33-9b5d3fb60098
author:bwren
manager:cfreeman
ms.author: raynew
---
# Recommended Administrator Capabilities in Service Provider Foundation
>Apples To: System Center 2016

This topic provides guidelines for administrator capabilities and roles for administering Service Provider Foundation.  

## Roles for database administrators  
A database administrator \(DBA\) has full administrator rights on SQL Server, and operates as the SQL Server administrator. This administrator should be able to grant permissions to create databases in SQL Server or grant those permissions to the Service Provider Foundation Administrator \(SPFA\). This administrator should be able to do the following:  

-   Create database named SCSPFDB. The default database is set to SCSPFDB.  

-   Create a SQL Server logon and user for the Service Provider Foundation Administrator, and grant the user the permissions to create tables, connect to the SPF database, and create logon roles and grant permissions for users.  


## Roles for Service Provider Foundation administrators  
A Service Provider Foundation administrator is the user responsible for installing Service Provider Foundation, and should have administrative rights on the server where Service Provider Foundation is to be installed.  

There are two database scenario configurations:  

-   Install Service Provider Foundation by using a connection to an existing database.  

    The Service Provider Foundation administrator must verify that the permissions were granted by the database administrator as described in the previous section.  

-   Create a new database.  

    The database administrator must create the database \(SCSPFDB\) and then the Service Provider Foundation administrator must install Service Provider Foundation and have permission to configure the database as needed such as to add tables. Service Provider Foundation administrators must create the Service Provider Foundation Application Pool in Internet Information Services \(IIS\) and create a database user for an Application Pool User with the permissions to connect t the SPF database, perform select, update, delete, and insert operations, and create logon roles for Application Pool users.


## Roles for Application Pool users  
This is the Application Pool user in IIS who must have full administrative privileges in VMM. These users should have the permissions to perform Create, Read, Update, and Delete operations on the Service Provider Foundation database. For portal applications, these operations can be restricted to specific tables.  
