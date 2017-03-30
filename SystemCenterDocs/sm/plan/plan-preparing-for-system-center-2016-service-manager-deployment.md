---
title: Prepare for Service Manager deployment
description: Describes Service Manager deployment preparation considerations.
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
ms.assetid: f5b2cb5d-96d6-4b49-a2ce-251372baf9a5
---

# Prepare for System Center 2016 - Service Manager deployment

>Applies To: System Center 2016 - Service Manager

Before you start the deployment of System Center 2016 - Service Manager, you create a group of users in Active Directory Domain Services \(AD DS\), and you create or identify a domain account that will be used during the Setup process. Make sure that the domain account is a member of the appropriate groups that are necessary for proper operation of Service Manager. Keep the following in mind when you are installing Service Manager and Operations Manager on the same server:  

- Operations Manager can share the database server with Service Manager.  

- An Operations Manager agent is automatically installed as part of Service Manager. After Setup completes, you must manually configure the agent for use with the Operations Manager management server.

     To validate that the Operations Manager Agent was installed, open Control Panel and verify that the Operations Manager Agent is present.

-   You can install both the Operations Manager console and the Service Manager console on the same computer. The order in which you install the consoles does not matter.  

-   Do not attempt to use the same SQL Server Reporting Services \(SSRS\) instance for both Operations Manager and Service Manager.  

## Account considerations before you run Setup

Before running Setup for System Center 2016 - Service Manager, review the following sections to make sure that the requirements that are needed to install Service Manager have been met. During Setup, you will be prompted to provide domain users or groups for various Service Manager functions. Review this information to make sure that you are ready for the setup process.


### Account used when you install Service Manager


This section describes the permissions that you need when you are installing a Service Manager management server and Service Manager console databases and when you are registering the Service Manager management group with the data warehouse management group in System Center 2016 - Service Manager.

> [!NOTE]  
>  The account that you use to run Setup is automatically made an administrator in Service Manager.

#### Service Manager management server

You need the following permissions when you are installing a Service Manager management server:  

-   Local administrator on the computer that you run Setup on  
-   Local administrator on the computer that will host the Service Manager database if it is on a remote computer  
-   Logged\-on user must be a domain account  
-   The Sysadmin SQL Server role on the SQL Server instance where the Service Manager database is being created  


#### Service Manager console

You need the following permissions when you are installing the Service Manager console:  

-   Local administrator on the computer that you run Setup on  

#### Data warehouse management server

You need the following permissions when you are installing the data warehouse management server:  

-   Local administrator on the computer that you run Setup on  
-   Local administrator on the computer that will host the data warehouse database if it is on a remote computer  
-   Logged\-in user must be a domain account  
-   The Content Manager role in SQL Server Reporting Services \(SSRS\) at the site level \(root\)  
-   The Sysadmin SQL Server role on the SQL Server instance where the data warehouse database is being created  

#### SQL Server Reporting Services

You need the following permissions when you are installing SSRS:  

-   Permissions to place a binary file into the \\Program Files\\Microsoft SQL Server\\*Instance Name*\Reporting Services\\ReportServer\\Bin folder on the computer hosting the data warehouse management server  

#### Registering Service Manager with the data warehouse  

You need the following permissions when you are registering Service Manager with the data warehouse:  

-   The Sysadmin or security admin SQL Server role on the instance that is hosting the Service Manager database  
-   The Sysadmin or security admin SQL Server role on the instance that is hosting the data warehouse database  
-   Membership in the Service Manager Administrators user role on the Service Manager management server  
-   Membership in the Service Manager Administrators user role on the data warehouse management server

### Accounts required when you install Service Manager

You will have to provide credentials for the accounts in the following table during the installation of the System Center 2016 - Service Manager and data warehouse management servers.  

> [!NOTE]  
The user accounts and group accounts that are required for the installation of Service Manager must reside in the Users organizational unit \(OU\) in Active Directory Domain Services \(AD DS\).  

#### Accounts used when installing a Service Manager management server  

|Account|Permissions|How it is used in Service Manager|  
|-------------|-----------------|---------------------------------------------|  
|Management group administrators|-   Must be a domain user or group. <br> **Important:**      The user account that is logged into the computer during installation of an initial Service Manager management server is automatically added to this group.|-   Added to the Service Manager Administrators user role.|  
|Service Manager services account|-   Must be a domain user or group.<br />-   Must be member of local administrators.|-   Becomes the Operational System Account.<br />-   Assigned to the logon account for the System Center Data Access Service.<br />-   Assigned to the logon account for System Center Management Configuration service.<br />-   Becomes a member of the sdk\_users and configsvc\_users database roles for the Service Manager database.<br />-   If you change the credentials for these two services, make sure that the new account has a SQL Login in the ServiceManager database and that this account is a member of the Builtin\\Administrators group.|  
|Workflow account|-   Must be a domain user or group.<br />-   Must have permissions to send email and must have a mailbox on the Simple Mail Transfer Protocol \(SMTP\) server \(required for the E\-mail Incident feature\).<br />-   Must be member of the Users local security group.<br />-   Must be made a member of the Service Manager Administrators user role for email notifications for function properly.|-   This account is used for all workflows and is made a member of the Service Manager Workflows user role.|  

#### Security best practices for accounts

 When you are assigning Active Directory accounts for use with Service Manager Run As Accounts, it is a best practice to use service accounts. We strongly recommend against using Active Directory user accounts that are associated with individual people.  

 For more information about security best practices, download a copy of the Windows Server Security Guide, which is now part of the [Windows Server Security Compliance Management Toolkit](http://go.microsoft.com/fwlink/p/?LinkID=167160).

#### Accounts used when you install a data warehouse management server  

|Account|Permissions|How it is used in Service Manager|  
|-------------|-----------------|---------------------------------------------|  
|Management group administrators|-   Must be a domain user or group.|-   Added to the data warehouse administrators user role.|  
|Service Manager services account|-   Must be a domain user or group.<br />-   Must be member of local administrators on the data warehouse management server.<br />-   Must be the same account that you used for the Service Manager management server services account.|-   Becomes the data warehouse system Run As account.<br />-   Assigned to the ServiceManager SDK Service account.<br />-   Assigned to ServiceManager Config account.<br />-   Becomes a member of the sdk\_users and configsvc\_users database roles for the DWDataMart database.<br />-   Becomes a member of the db\_datareader database role for the DWRepository database.<br />-   Becomes a member of the configsvc\_users database role for the Service Manager database.|  
|Reporting account|-   Must be a domain account.|-   Used by SQL Server Reporting Services \(SSRS\) to access the DWDataMart database to get data for reporting.<br />-   Becomes a member of the db\_datareader database role for the DWDataMart database.<br />-   Becomes a member of the reportuser database role for the DWDatamart database.|  
|Analysis Services account|-   Must be a domain account.|-   Used to communicate with datamarts.<br />-   Account is added as an administrator role in the Analysis Services server database \(DWASDataBase\) for database processing and cube reading.|  

### Credential used when registering a Service Manager management group with the data warehouse management group

 As part of the installation process, you register the Service Manager management group with the data warehouse management group. During this process, you will be prompted to provide credentials. The account credentials that you provide must be a domain account. Furthermore, you will have to provide an account with the following permissions:  

-   Must be a member of the Administrator user role in both the Service Manager and data warehouse management groups.  
-   Must be a member of the users local administrator group on the data warehouse management server.  

### Accounts required to create connectors

 When you are creating connectors, you are asked for credentials that the connector will use to perform its function. The following table outlines the permissions that this account will need, and it describes best practices for high security.  

#### Operations Manager Alert connector  

|Permissions|Best practices|  
|-----------------|--------------------|  
|-   Must be a domain account.<br />-   Must be a member of the Users local security group on the Service Manager management server.<br />-   Must be an Operations Manager Administrator.|Domain account specifically created for this purpose that is only in the Users local security group and in an Administrator user role in Operations Manager and in an Advanced Operator user role in Service Manager.|  

#### Operations Manager CI connector  

|Permissions|Best practices|  
|-----------------|--------------------|  
|-   Must be a domain account.<br />-   Must be a member of the Users local security group on the management server.<br />-   Must be an Operations Manager Operator.|Domain account specifically created for this purpose that is only in the Users local security group and in an Operator user role in Operations Manager and in an Advanced Operator user role in Service Manager.|  

#### Active Directory connector  

|Permissions|Best practices|  
|-----------------|--------------------|  
|-   Must be a domain account.<br />-   Must be a member of the Users local security group on the Service Manager management server.<br />-   Must have permissions to bind to the domain controller that the connector will read data from.<br />-   Needs generic read rights on the objects that are being synchronized into the Service Manager database from AD DS.|Domain account specifically created for this purpose that is only in the Users local security group and in an Advanced Operator user role in Service Manager and has read\-only permissions in AD DS.|  

#### Configuration Manager connector  

|Permissions|Best practices|  
|-----------------|--------------------|  
|-   Must be a domain account.<br />-   Must be a member of the Users local security group on the Service Manager management server.|Domain account specifically created for this purpose that is only in the Users local security group, must be a member of the smsdbrole\_extract and db\_datareader on the System Center Configuration Manager database, and is in an Advanced Operator user role in Service Manager.|



## Prepare computers for Service Manager deployment


Use the following procedures to prepare computers for deployment of System Center 2016 - Service Manager.  

### To prepare computers for Service Manager deployment  

1.  Make sure that no Operations Manager parts are installed on the computers that will host either Service Manager or the data warehouse.  
2.  Create an Active Directory group of users that will be assigned to the role of Service Manager administrators of both the data warehouse and Service Manager management groups. For example, create the group **SM\_Admins**.  

    > [!NOTE]  
    >  This group of users must be in the same domain that Service Manager is in. Users from any other domain-even child domains-are not supported.  

3.  Create the accounts that are necessary for Service Manager.

    > [!NOTE]  
    >  Service Manager accounts must be in the same domain that Service Manager is in. Accounts from any other domain-even child domains-are not supported.  

4.  Make sure that the Structured Query Language \(SQL\) instances that are used for Service Manager databases are using port number 1433.
5.  If you are installing the databases on a remote computer running Microsoft SQL Server, the user who is running Setup must be a domain user with local administrator permissions on the SQL Server computer.  
6.  On computers that will host the Service Manager console, under **Internet Options**, **Local Area Network \(LAN\) Settings**, select **Bypass proxy server for local addresses**.  

7.  Open a browser, and then enter the following two URLs:  

    -   `http://<computer hosting SSRS>/reports`  

    -   `http://<computer hosting SSRS>/reportserver`  

     If either connection attempt fails or returns an error-for example, **HTTP Error 404.0 Not Found**-complete the steps in the procedure "To configure the reporting server." Otherwise, continue with the installation of Service Manager.  

### To configure the reporting server  

1.  By using an account that has administrator rights, log on to the computer that will host SQL Server Reporting Services \(SSRS\).  

2.  Click **Start**, point to **Programs**, point to **Microsoft SQL Server 2008**, point to **Configuration Tools**, and then click **Reporting Services Configuration Manager**.  

3.  In the **Reporting Services Configuration Connection** dialog box, make sure that the information in **Server Name** and **Report Server Instance** is correct, and then click **Connect**.  

4.  In the **Connect** pane, click **Web Service URL**.  

5.  In the **Report Server Web Service Virtual Directory** area, in the **Virtual Directory** text box, make sure that the entry is **ReportServer**, and then click **Apply**.  

6.  In the **Connect** pane, click **Report Manager URL**.  

7.  In the **Report Manager Site Identification** area, in the **Virtual Directory** text box, make sure that the entry reads **Reports**, and then click **Apply**.  

8.  In the **Connect** pane, click the top entry (`<server>\\<instance>`).  

9. In the **Current Report Server** area, click **Stop**, and then click **Start**.
