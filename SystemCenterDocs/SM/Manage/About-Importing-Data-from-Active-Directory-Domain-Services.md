---
title: About Importing Data from Active Directory Domain Services
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1d1485f-7c42-4572-8725-56685f51e0e0
---
# About Importing Data from Active Directory Domain Services
The [!INCLUDE[smshort](Token/smshort_md.md)] database in Service Manager contains information about your enterprise, and it is used by all the parts of your service management structure. You can use an Active Directory connector to add users, groups, printers, and computers \(and only these object types\) as configuration items into the [!INCLUDE[smshort](Token/smshort_md.md)] database.

> [!NOTE]
> If the same user name exists in two different organizational units \(OUs\) within the Active Directory domain, [!INCLUDE[smshort](Token/smshort_md.md)] cannot import both user accounts, and an event is logged in the System Center Operations Manager application log.

In addition, when you configure an Active Directory connector to import data from an Active Directory group, you can select an option to automatically add users from the Active Directory group. When they are selected, any users that are added to the Active Directory group will be automatically added to the [!INCLUDE[smshort](Token/smshort_md.md)] database. If those users are removed from the Active Directory group, they will remain in the [!INCLUDE[smshort](Token/smshort_md.md)] database; however, they will reside in the Deleted Items group.

When you have created an Active Directory connector, **Select objects** in the connector cannot be updated. Instead, you create security groups in Active Directory that map to User Roles in [!INCLUDE[smshort](Token/smshort_md.md)]. For example, you can create a Security Group in Active Directory Domain Services \(AD DS\), named Incident Resolvers. In [!INCLUDE[smshort](Token/smshort_md.md)], you can assign this security group to the Incident Resolvers user role. When you create the Active Directory connector and you select **Automatically add users of AD Groups imported by this connector**, when a user who is a member of the Incident Resolvers security group starts the [!INCLUDE[smcons](Token/smcons_md.md)], they will be granted Incident Resolver rights and permissions.

If you are importing data from several OUs or subdomains, you have the option of creating a Lightweight Directory Access Protocol \(LDAP\) query that specifies computers, printers, users, or user groups to import with the connector. For example, an LDAP filter of all objects that are in either Dallas or Austin and that have the first name of John looks like `(&(givenName=John) (|(l=Dallas) (l=Austin)))`. You can test your queries, and all errors must be corrected before you can configure the Active Directory connector. For more information about LDAP queries, see [Search Filter Syntax](http://go.microsoft.com/fwlink/?LinkId=149908).

If you must later perform maintenance operations on the [!INCLUDE[smshort](Token/smshort_md.md)] database, you can temporarily disable the connector and suspend the importation of data. Later, you can resume the importation of data by re\-enabling the connector.

When you import a large number of users from AD DS\) or from System Center Configuration Manager, CPU utilization might increase to 100 percent. You will notice this on one core of the CPU. For example, if you import 20,000 users, CPU utilization might remain high for up to an hour. You can mitigate this issue by creating connectors and importing the users into [!INCLUDE[smshort](Token/smshort_md.md)] before you deploy the product in your enterprise and by scheduling connector synchronization during off hours. Installing [!INCLUDE[smshort](Token/smshort_md.md)] on a computer that has a multi\-core CPU also minimizes the impact of importing a large number of users.


