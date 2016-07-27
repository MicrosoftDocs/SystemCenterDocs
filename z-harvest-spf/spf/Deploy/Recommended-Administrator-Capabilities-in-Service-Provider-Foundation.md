---
title: Recommended Administrator Capabilities in Service Provider Foundation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1ca67a42-81f9-4df4-ba33-9b5d3fb60098
author:bwren
manager:cfreemanwa
---
# Recommended Administrator Capabilities in Service Provider Foundation
This topic provides guidelines for administrator capabilities and roles for administering Service Provider Foundation.  
  
## Roles for database administrators  
A database administrator \(DBA\) has full administrator rights on SQL Server, and operates as the SQL Server administrator. This administrator should be able to grant permissions to create databases in SQL Server or grant those permissions to the Service Provider Foundation Administrator \(SPFA\). This administrator should be able to do the following:  
  
-   Create database named SCSPFDB. The default database is set to SCSPFDB.  
  
-   Create a SQL Server logon and user for the Service Provider Foundation Administrator, and grant the user the permissions described in this table.  
  
    |Permissions|Purpose|  
    |---------------|-----------|  
    |*Alter*|To be able to create tables.|  
    |*Connect with Grant*|To connect to the existing database.|  
    |*Select with Grant*, *Update with Grant*,  *Delete with Grant*, *Insert with Grant*|To grant these permissions to application users.|  
    |*Alter All logins*|To create SQL Server logins for the application pool users.|  
  
## Roles for Service Provider Foundation administrators  
A Service Provider Foundation administrator is the user responsible for installing Service Provider Foundation, and should have administrative rights on the server where Service Provider Foundation is to be installed.  
  
There are two database scenario configurations:  
  
-   Install Service Provider Foundation by using a connection to an existing database.  
  
    The Service Provider Foundation administrator must verify that the permissions were granted by the database administrator as described in the previous section.  
  
-   Create a new database.  
  
    The database administrator must create the database \(SCSPFDB\) and then the Service Provider Foundation administrator must install Service Provider Foundation and have permission to configure the database as needed such as to add tables. Service Provider Foundation administrators must create the Service Provider Foundation Application Pool in Internet Information Services \(IIS\) and create a database user for an Application Pool User with the following permissions:  
  
    |Permission|Purpose|  
    |--------------|-----------|  
    |*Connect*|To be able to connect to the Service Provider Foundation database.|  
    |*Select*, *Update*, *Delete*, *Insert*|To be able to perform basic operations.|  
    |Create the SQL Server logon for Application Pool User with default database set to SCSPFDB.|To be able to log on to SQL Server and access this database.|  
  
## Roles for Application Pool users  
This is the Application Pool user in IIS who must have full administrative privileges in --- translation.priority.ht:    - ar-sa   - cs-cz   - da-dk   - de-de   - el-gr   - es-es   - fi-fi   - fr-fr   - he-il   - hu-hu   - it-it   - ja-jp   - ko-kr   - nb-no   - nl-nl   - pl-pl   - pt-br   - pt-pt   - ro-ro   - ru-ru   - sv-se   - tr-tr   - zh-cn   - zh-hk   - zh-tw --- System&nbsp;Center&nbsp;2012&nbsp;- Virtual&nbsp;Machine&nbsp;Manager&nbsp;\(VMM\). These users should have the permissions to perform Create, Read, Update, and Delete operations on the Service Provider Foundation database. For portal applications, these operations can be restricted to specific tables.  
  
## See Also  
[Manage Certificates and User Roles in Service Provider Foundation](../../spf/Deploy/Manage-Certificates-and-User-Roles-in-Service-Provider-Foundation.md)  
[Administering Service Provider Foundation](../../spf/Deploy/Administering-Service-Provider-Foundation.md)  
[Walkthrough: Creating a Certificate and User Roles for Service Provider Foundation](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md)  
[Configuring Portals for Service Provider Foundation](../../spf/Deploy/Configuring-Portals-for-Service-Provider-Foundation.md)  
  
