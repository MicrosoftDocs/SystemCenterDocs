---
title: Recommended Administrator Capabilities in Service Provider Foundation
ms.custom: na
ms.prod: system-center-2012-sp1
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1ca67a42-81f9-4df4-ba33-9b5d3fb60098
---
# Recommended Administrator Capabilities in Service Provider Foundation
This topic provides guidelines for administrator capabilities and roles for administering [!INCLUDE[spflong](../Token/spflong_md.md)].

## Roles for database administrators
A database administrator \(DBA\) has full administrator rights on SQL Server, and operates as the SQL Server administrator. This administrator should be able to grant permissions to create databases in SQL Server or grant those permissions to the [!INCLUDE[spfshort](../Token/spfshort_md.md)] Administrator \(SPFA\). This administrator should be able to do the following:

-   Create database named SCSPFDB. The default database is set to SCSPFDB.

-   Create a SQL Server logon and user for the [!INCLUDE[spfshort](../Token/spfshort_md.md)] Administrator, and grant the user the permissions described in this table.

    |Permissions|Purpose|
    |---------------|-----------|
    |*Alter*|To be able to create tables.|
    |*Connect with Grant*|To connect to the existing database.|
    |*Select with Grant*, *Update with Grant*,  *Delete with Grant*, *Insert with Grant*|To grant these permissions to application users.|
    |*Alter All logins*|To create SQL Server logins for the application pool users.|

## Roles for [!INCLUDE[spfshort](../Token/spfshort_md.md)] administrators
A [!INCLUDE[spfshort](../Token/spfshort_md.md)] administrator is the user responsible for installing [!INCLUDE[spfshort](../Token/spfshort_md.md)], and should have administrative rights on the server where [!INCLUDE[spfshort](../Token/spfshort_md.md)] is to be installed.

There are two database scenario configurations:

-   Install [!INCLUDE[spfshort](../Token/spfshort_md.md)] by using a connection to an existing database.

    The [!INCLUDE[spfshort](../Token/spfshort_md.md)] administrator must verify that the permissions were granted by the database administrator as described in the previous section.

-   Create a new database.

    The database administrator must create the database \(SCSPFDB\) and then the [!INCLUDE[spfshort](../Token/spfshort_md.md)] administrator must install [!INCLUDE[spfshort](../Token/spfshort_md.md)] and have permission to configure the database as needed such as to add tables. [!INCLUDE[spfshort](../Token/spfshort_md.md)] administrators must create the [!INCLUDE[spfshort](../Token/spfshort_md.md)] Application Pool in Internet Information Services \(IIS\) and create a database user for an Application Pool User with the following permissions:

    |Permission|Purpose|
    |--------------|-----------|
    |*Connect*|To be able to connect to the [!INCLUDE[spfshort](../Token/spfshort_md.md)] database.|
    |*Select*, *Update*, *Delete*, *Insert*|To be able to perform basic operations.|
    |Create the SQL Server logon for Application Pool User with default database set to SCSPFDB.|To be able to log on to SQL Server and access this database.|

## Roles for Application Pool users
This is the Application Pool user in IIS who must have full administrative privileges in [!INCLUDE[vmm12long](../Token/vmm12long_md.md)]. These users should have the permissions to perform Create, Read, Update, and Delete operations on the [!INCLUDE[spfshort](../Token/spfshort_md.md)] database. For portal applications, these operations can be restricted to specific tables.

## See Also
[Manage Certificates and User Roles in Service Provider Foundation](../Topic/Manage-Certificates-and-User-Roles-in-Service-Provider-Foundation.md)
[Administering Service Provider Foundation](../Topic/Administering-Service-Provider-Foundation.md)
[Walkthrough: Creating a Certificate and User Roles for Service Provider Foundation](../Topic/Walkthrough--Creating-a-Certificate-and-User-Roles-for-Service-Provider-Foundation.md)
[Configuring Portals for Service Provider Foundation](../Topic/Configuring-Portals-for-Service-Provider-Foundation.md)

