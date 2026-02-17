---
title: Prepare for Service Manager deployment
description: Describes Service Manager deployment preparation considerations.
ms.service: system-center
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.subservice: service-manager
ms.topic: how-to
ms.update-cycle: 1095-days
ms.custom: UpdateFrequency2, engagement-fy23, engagement-fy24
---

# Prepare for System Center - Service Manager deployment

Before you start the deployment of System Center - Service Manager, you create a group of users in Active Directory Domain Services \(AD DS\), and you create or identify a domain account that will be used during the Setup process. Ensure that the domain account is a member of the appropriate groups that are necessary for proper operation of Service Manager. Keep the following in mind when you're installing Service Manager and Operations Manager on the same server:  

- Operations Manager can share the database server with Service Manager.  

- An Operations Manager agent is automatically installed as part of Service Manager. After the Setup completes, you must manually configure the agent for use with the Operations Manager management server.

     To validate that the Operations Manager Agent was installed, open the Control Panel and verify that the Operations Manager Agent is present.

- You can install both the Operations Manager console and the Service Manager console on the same computer. The order in which you install the consoles doesn't matter.  

- Don't attempt to use the same SQL Server Reporting Services \(SSRS\) instance for both Operations Manager and Service Manager.  

## Account considerations before you run Setup

Before running Setup for Service Manager, review the following sections to ensure that the requirements that are needed to install Service Manager have been met. During Setup, you will be prompted to provide domain users or groups for various Service Manager functions. Review this information to ensure that you're ready for the setup process.

### Account used when you install Service Manager

This section describes the permissions that you need when you're installing a Service Manager management server and Service Manager console databases and when you're registering the Service Manager management group with the data warehouse management group in Service Manager.

> [!NOTE]  
> The account that you use to run Setup is automatically made an administrator in Service Manager.

Select the required tab for details of the permissions that you need:

# [Service Manager management server](#tab/SMManagementServer)

You need the following permissions when you're installing a Service Manager management server:  

- Local administrator on the computer that you run Setup on  
- Local administrator on the computer that will host the Service Manager database if it's on a remote computer  
- Logged-on user must be a domain account  
- The Sysadmin SQL Server role on the SQL Server instance where the Service Manager database is being created  

# [Service Manager console](#tab/SMConsole)

You need the following permissions when you're installing the Service Manager console:  

- Local administrator on the computer that you run Setup on  

# [Data warehouse management server](#tab/DataWarehouse)

You need the following permissions when you're installing the data warehouse management server:  

- Local administrator on the computer that you run Setup on  
- Local administrator on the computer that will host the data warehouse database if it's on a remote computer  
- Logged\-in user must be a domain account  
- The Content Manager role in SQL Server Reporting Services \(SSRS\) at the site level \(root\)  
- The Sysadmin SQL Server role on the SQL Server instance where the data warehouse database is being created  

# [SQL Server Reporting Services](#tab/SQLServer)

You need the following permissions when you're installing SSRS:  

Permissions to place a binary file into the \\Program Files\\Microsoft SQL Server\\*Instance Name*\Reporting Services\\ReportServer\\Bin folder on the computer hosting the data warehouse management server.

# [Registering Service Manager with the data warehouse](#tab/SMDataWarehouse)

You need the following permissions when you're registering Service Manager with the data warehouse:  

- The Sysadmin or security admin SQL Server role on the instance that is hosting the Service Manager database  
- The Sysadmin or security admin SQL Server role on the instance that is hosting the data warehouse database  
- Membership in the Service Manager Administrators user role on the Service Manager management server  
- Membership in the Service Manager Administrators user role on the data warehouse management server

---

### Accounts required when you install Service Manager

You will have to provide credentials for the accounts in the following table during the installation of the Service Manager and data warehouse management servers.  

> [!NOTE]  
>The user accounts and group accounts that are required for the installation of Service Manager must reside in the Users organizational unit \(OU\) in Active Directory Domain Services \(AD DS\).  

#### Accounts used when installing a Service Manager management server  

|Account|Permissions|How it's used in Service Manager|  
|-------------|-----------------|---------------------------------------------|  
|Management group administrators|-   Must be a domain user or group. <br> **Important:**      The user account that is logged into the computer during installation of an initial Service Manager management server is automatically added to this group.|-   Added to the Service Manager Administrators user role.|  
|Service Manager services account|-   Must be a domain user or group.<br />-   Must be member of local administrators.<br />- Must have **Log on as a service**. <br /><br /> To set these permissions, use **Security Settings** > **Local Policies** > **User Rights Assignment**.  <br /> <br /> **Optional**: <br /><br />- Deny log on as a batch job <br /><br /> - Deny log on through Remote Desktop Services. |-   Becomes the Operational System Account.<br />-   Assigned to the logon account for the System Center Data Access Service.<br />-   Assigned to the logon account for System Center Management Configuration service.<br />- Becomes a member of the sdk\_users and configsvc\_users database roles for the Service Manager database.<br />-   If you change the credentials for these two services, ensure that the new account has a SQL Login in the ServiceManager database and that this account is a member of the Builtin\\Administrators group.|  
|Workflow account|-   Must be a domain user or group.<br />-   Must have permissions to send email and must have a mailbox on the Simple Mail Transfer Protocol \(SMTP\) server \(required for the E\-mail Incident feature\).<br />-   Must be member of the Users local security group.<br />-   Must be made a member of the Service Manager Administrators user role for email notifications for function properly. Must be a domain user or group.<br />-   Must be member of local administrators.<br />- Must have **Log on as a service**. <br /><br /> To set these permissions, use **Security Settings** > **Local Policies** > **User Rights Assignment**.<br /><br /> **Optional**: <br />-Deny log on as a batch job<br /><br />-Deny log on through Remote Desktop Services.  |-   This account is used for all workflows and is made a member of the Service Manager Workflows user role.|  

#### Security best practices for accounts

 When you're assigning Active Directory accounts for use with Service Manager Run As Accounts, it's a best practice to use service accounts. We strongly recommend against using Active Directory user accounts that are associated with individual people.  

 For more information about security best practices, download a copy of the Windows Server Security Guide, which is now part of the [Windows Server Security Compliance Management Toolkit](https://www.microsoft.com/download/details.aspx?id=55319).

#### Accounts used when you install a data warehouse management server  

|Account|Permissions|How it's used in Service Manager|  
|-------------|-----------------|---------------------------------------------|  
|Management group administrators|-   Must be a domain user or group.|-   Added to the data warehouse administrators user role.|  
|Service Manager services account|-   Must be a domain user or group.<br />-   Must be member of local administrators on the data warehouse management server.<br />-   Must be the same account that you used for the Service Manager management server services account.|-   Becomes the data warehouse system Run As account.<br />-   Assigned to the ServiceManager SDK Service account.<br />-   Assigned to ServiceManager Config account.<br />-   Becomes a member of the sdk\_users and configsvc\_users database roles for the DWDataMart database.<br />-   Becomes a member of the db\_datareader database role for the DWRepository database.<br />-   Becomes a member of the configsvc\_users database role for the Service Manager database.|  
|Reporting account|-   Must be a domain account. <br />- Must have **Log on as a service**. <br /><br /> To set these permissions, use **Security Settings** > **Local Policies** > **User Rights Assignment**. <br /> <br /> **Optional**: <br /><br />- Deny log on as a batch job <br /><br /> - Deny log on through Remote Desktop Services.|-   Used by SQL Server Reporting Services \(SSRS\) to access the DWDataMart database to get data for reporting.<br />-   Becomes a member of the db\_datareader database role for the DWDataMart database.<br />-   Becomes a member of the reportuser database role for the DWDatamart database.|  
|Analysis Services account|-   Must be a domain account.<br />- Must have **Log on as a service**. <br /><br /> To set these permissions, use **Security Settings** > **Local Policies** > **User Rights Assignment**. <br /> <br /> **Optional**: <br /><br />- Deny log on as a batch job <br /><br /> - Deny log on through Remote Desktop Services.|-   Used to communicate with datamarts.<br />-   Account is added as an administrator role in the Analysis Services server database \(DWASDataBase\) for database processing and cube reading.|  

### Credential used when registering a Service Manager management group with the data warehouse management group

 As part of the installation process, you register the Service Manager management group with the data warehouse management group. During this process, you'll be prompted to provide credentials. The account credentials that you provide must be a domain account. Furthermore, you will have to provide an account with the following permissions:  

- Must be a member of the Administrator user role in both the Service Manager and data warehouse management groups.  
- Must be a member of the users local administrator group on the data warehouse management server.  

### Accounts required to create connectors

 When you're creating connectors, you're asked for credentials that the connector will use to perform its function. The following outlines the permissions that this account will need, and it describes best practices for high security.  

 Connector accounts for Operations Manager, Orchestrator, SCVMM, and AD require **Log on as a service**.

 To set these permissions, use **Security Settings** > **Local Policies** > **User Rights Assignment** .

**Optional**:
- Deny log on as a batch job
- Deny log on through Remote Desktop Services
 
Select the required tab to view the permissions and best practices:

# [Operations Manager Alert connector](#tab/OMAlertConnector)

|Permissions|Best practices|  
|-----------------|--------------------|  
|-   Must be a domain account.<br />-   Must be a member of the Users local security group on the Service Manager management server.<br />-   Must be an Operations Manager Administrator.|Domain account specifically created for this purpose that is only in the Users local security group and in an Administrator user role in Operations Manager and in an Advanced Operator user role in Service Manager.|  

# [Operations Manager CI connector](#tab/OMCIConnector)

|Permissions|Best practices|  
|-----------------|--------------------|  
|-   Must be a domain account.<br />-   Must be a member of the Users local security group on the management server.<br />-   Must be an Operations Manager Operator.|Domain account specifically created for this purpose that is only in the Users local security group and in an Operator user role in Operations Manager and in an Advanced Operator user role in Service Manager.|  

# [Active Directory connector](#tab/ADConnector)

|Permissions|Best practices|  
|-----------------|--------------------|  
|-   Must be a domain account.<br />-   Must be a member of the Users local security group on the Service Manager management server.<br />-   Must have permissions to bind to the domain controller that the connector will read data from.<br />-   Needs generic read rights on the objects that are being synchronized into the Service Manager database from AD DS.|Domain account specifically created for this purpose that is only in the Users local security group and in an Advanced Operator user role in Service Manager and has read\-only permissions in AD DS.|  

# [Configuration Manager connector](#tab/CMConnector)

|Permissions|Best practices|  
|-----------------|--------------------|  
|-   Must be a domain account.<br />-   Must be a member of the Users local security group on the Service Manager management server.|Domain account specifically created for this purpose that is only in the Users local security group must be a member of the smsdbrole\_extract and db\_datareader on the Configuration Manager database, and is in an Advanced Operator user role in Service Manager.|

---

## Prepare computers for Service Manager deployment

To prepare computers for Service Manager deployment, follow these steps:

1. Ensure that no Operations Manager parts are installed on the computers that will host either Service Manager or the data warehouse.  
2. Create an Active Directory group of users that will be assigned to the role of Service Manager administrators of both the data warehouse and Service Manager management groups. For example, create the group **SM\_Admins**.  

   > [!NOTE]  
   > This group of users must be in the same domain that Service Manager is in. Users from any other domain—even child domains—aren't supported.  

3. Create the accounts that are necessary for Service Manager.

   > [!NOTE]  
   > Service Manager accounts must be in the same domain that Service Manager is in. Accounts from any other domain—even child domains—aren't supported.  

4. Ensure that the Structured Query Language \(SQL\) instances that are used for Service Manager databases are using port number 1433.
5. If you're installing the databases on a remote computer running Microsoft SQL Server, the user who is running Setup must be a domain user with local administrator permissions on the SQL Server computer.  
6. On computers that will host the Service Manager console, under **Internet Options**, **Local Area Network \(LAN\) Settings**, select **Bypass proxy server for local addresses**.  
7. Open a browser, and then enter the following two URLs:  

   - `http://<computer hosting SSRS>/reports`  

   - `http://<computer hosting SSRS>/reportserver`  

     If either connection attempt fails or returns an error—for example, **HTTP Error 404.0 Not Found**—complete the steps in the procedure **To configure the reporting server**. Otherwise, continue with the installation of Service Manager.  

### Configure the reporting server  

1. By using an account that has administrator rights, sign in to the computer that will host SQL Server Reporting Services \(SSRS\).  

2. Select **Start**, point to **Programs**, point to **Microsoft SQL Server 2008**, point to **Configuration Tools**, and select **Reporting Services Configuration Manager**.  

3. In the **Reporting Services Configuration Connection** dialog, ensure that the information in **Server Name** and **Report Server Instance** is correct, and select **Connect**.  

4. In the **Connect** pane, select **Web Service URL**.  

5. In the **Report Server Web Service Virtual Directory** area, in the **Virtual Directory** text box, ensure that the entry is **ReportServer**, and select **Apply**.  

6. In the **Connect** pane, select **Report Manager URL**.  

7. In the **Report Manager Site Identification** area, in the **Virtual Directory** text box, ensure that the entry reads **Reports**, and select **Apply**.  

8. In the **Connect** pane, select the top entry (`<server>\\<instance>`).  

9. In the **Current Report Server** area, select **Stop**, and select **Start**.

::: moniker range=">=sc-sm-2019"

> [!IMPORTANT]
> When you install System Center Service Manager with SQL Server Reporting Services (SSRS) 2017 or later, Service Manager reports don't deploy, an event 33410 occurs and displays the details for the deployment failure. See the following information for the cause and resolution for this issue.  

SSRS 2017 version 14.0.600.1274 and later includes a new advanced setting *AllowedResourceExtensionsForUpload*. This setting restricts the set of extensions of resource files that can be uploaded to the reporting server. This issue occurs because Service Manager reporting uses extensions that aren't included in the default set in *AllowedResourceExtensionsForUpload*.

To resolve this issue, add \*.\* to the list of extensions. Follow these steps:

1. Start SQL Server Management Studio, and then connect to a report server instance that Service Manager uses.
2. Right-click the report server name, select **Properties**, and then select **Advanced**.
3. Locate the **AllowedResourceExtensionsForUpload** setting, add \*.\* to the list of extensions, and then select **OK**.
4. Restart SSRS.

::: moniker-end

## Next steps

To learn about the issues that affect performance and scalability in Service Manager, review [Planning for performance and scalability](plan-perf-scale.md). It also suggests best practices to achieve good performance using suggested hardware configurations.
