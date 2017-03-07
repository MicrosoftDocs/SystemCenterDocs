---
title: Accounts required during Service Manager Setup
description: Describes the accounts that are required when you install Service Manager.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 54ebd290-b024-4b24-89dd-7c9d482737e3
---

# Accounts required when you install Service Manager

>Applies To: System Center 2016 - Service Manager

You will have to provide credentials for the accounts in the following table during the installation of the System Center 2016 - Service Manager and data warehouse management servers.  

> [!NOTE]  
The user accounts and group accounts that are required for the installation of Service Manager must reside in the Users organizational unit \(OU\) in Active Directory Domain Services \(AD DS\).  

## Accounts used when installing a Service Manager management server  

|Account|Permissions|How it is used in Service Manager|  
|-------------|-----------------|---------------------------------------------|  
|Management group administrators|-   Must be a domain user or group. <br> **Important:**      The user account that is logged into the computer during installation of an initial Service Manager management server is automatically added to this group.|-   Added to the Service Manager Administrators user role.|  
|Service Manager services account|-   Must be a domain user or group.<br />-   Must be member of local administrators.|-   Becomes the Operational System Account.<br />-   Assigned to the logon account for the System Center Data Access Service.<br />-   Assigned to the logon account for System Center Management Configuration service.<br />-   Becomes a member of the sdk\_users and configsvc\_users database roles for the Service Manager database.<br />-   If you change the credentials for these two services, make sure that the new account has a SQL Login in the ServiceManager database and that this account is a member of the Builtin\\Administrators group.|  
|Workflow account|-   Must be a domain user or group.<br />-   Must have permissions to send email and must have a mailbox on the Simple Mail Transfer Protocol \(SMTP\) server \(required for the E\-mail Incident feature\).<br />-   Must be member of the Users local security group.<br />-   Must be made a member of the Service Manager Administrators user role for email notifications for function properly.|-   This account is used for all workflows and is made a member of the Service Manager Workflows user role.|  

### Security best practices for accounts

 When you are assigning Active Directory accounts for use with Service Manager Run As Accounts, it is a best practice to use service accounts. We strongly recommend against using Active Directory user accounts that are associated with individual people.  

 For more information about security best practices, download a copy of the Windows Server Security Guide, which is now part of the [Windows Server Security Compliance Management Toolkit](http://go.microsoft.com/fwlink/p/?LinkID=167160).

## Accounts used when you install a data warehouse management server  

|Account|Permissions|How it is used in Service Manager|  
|-------------|-----------------|---------------------------------------------|  
|Management group administrators|-   Must be a domain user or group.|-   Added to the data warehouse administrators user role.|  
|Service Manager services account|-   Must be a domain user or group.<br />-   Must be member of local administrators on the data warehouse management server.<br />-   Must be the same account that you used for the Service Manager management server services account.|-   Becomes the data warehouse system Run As account.<br />-   Assigned to the ServiceManager SDK Service account.<br />-   Assigned to ServiceManager Config account.<br />-   Becomes a member of the sdk\_users and configsvc\_users database roles for the DWDataMart database.<br />-   Becomes a member of the db\_datareader database role for the DWRepository database.<br />-   Becomes a member of the configsvc\_users database role for the Service Manager database.|  
|Reporting account|-   Must be a domain account.|-   Used by SQL Server Reporting Services \(SSRS\) to access the DWDataMart database to get data for reporting.<br />-   Becomes a member of the db\_datareader database role for the DWDataMart database.<br />-   Becomes a member of the reportuser database role for the DWDatamart database.|  
|Analysis Services account|-   Must be a domain account.|-   Used to communicate with datamarts.<br />-   Account is added as an administrator role in the Analysis Services server database \(DWASDataBase\) for database processing and cube reading.|  

## Credential used when registering a Service Manager management group with the data warehouse management group

 As part of the installation process, you register the Service Manager management group with the data warehouse management group. During this process, you will be prompted to provide credentials. The account credentials that you provide must be a domain account. Furthermore, you will have to provide an account with the following permissions:  

-   Must be a member of the Administrator user role in both the Service Manager and data warehouse management groups.  
-   Must be a member of the users local administrator group on the data warehouse management server.  

## Accounts required to create connectors

 When you are creating connectors, you are asked for credentials that the connector will use to perform its function. The following table outlines the permissions that this account will need, and it describes best practices for high security.  

### Operations Manager Alert connector  

|Permissions|Best practices|  
|-----------------|--------------------|  
|-   Must be a domain account.<br />-   Must be a member of the Users local security group on the Service Manager management server.<br />-   Must be an Operations Manager Administrator.|Domain account specifically created for this purpose that is only in the Users local security group and in an Administrator user role in Operations Manager and in an Advanced Operator user role in Service Manager.|  

### Operations Manager CI connector  

|Permissions|Best practices|  
|-----------------|--------------------|  
|-   Must be a domain account.<br />-   Must be a member of the Users local security group on the management server.<br />-   Must be an Operations Manager Operator.|Domain account specifically created for this purpose that is only in the Users local security group and in an Operator user role in Operations Manager and in an Advanced Operator user role in Service Manager.|  

### Active Directory connector  

|Permissions|Best practices|  
|-----------------|--------------------|  
|-   Must be a domain account.<br />-   Must be a member of the Users local security group on the Service Manager management server.<br />-   Must have permissions to bind to the domain controller that the connector will read data from.<br />-   Needs generic read rights on the objects that are being synchronized into the Service Manager database from AD DS.|Domain account specifically created for this purpose that is only in the Users local security group and in an Advanced Operator user role in Service Manager and has read\-only permissions in AD DS.|  

### Configuration Manager connector  

|Permissions|Best practices|  
|-----------------|--------------------|  
|-   Must be a domain account.<br />-   Must be a member of the Users local security group on the Service Manager management server.|Domain account specifically created for this purpose that is only in the Users local security group, must be a member of the smsdbrole\_extract and db\_datareader on the System Center Configuration Manager database, and is in an Advanced Operator user role in Service Manager.|
