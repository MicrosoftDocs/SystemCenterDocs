---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  mgoedtel
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-27
title:  Deploying System Center 2016 Operations Manager
ms.technology:  operations-manager
ms.assetid:  0a3df7b4-885e-4e80-b6b7-960ba5c5a774
---



# Deploying System Center 2016 - Operations Manager

>Applies To: System Center 2016 Technical Preview - Operations Manager

All System Center 2016 Technical Preview - Operations Manager individual management group deployments will either be an "all-in-one" installation, where all features are loaded on a single server, or a distributed installation. Installations can then be combined together to form an overall Operations Manager infrastructure that consists of multiple management groups. These management groups can then relate to each other as your business needs dictate.

This section of the Deployment Guide describes an individual management group deployment, where you have one management group, but the features of Operations Manager are either installed on a single server or distributed over several servers.

-   [Single-Server Deployment of Operations Manager](Single-Server-Deployment-of-Operations-Manager.md)

-   [Distributed Deployment of Operations Manager](Distributed-Deployment-of-Operations-Manager.md)

For information about connecting management groups, see [Connecting Management Groups in Operations Manager](http://go.microsoft.com/fwlink/p/?LinkID=207755).

## <a name="BKMK_BeforeYouBegin"></a>Before You Begin
Before you begin your deployment, you should read the release notes, and ensure that your server meets the minimum system requirements for Operations Manager. For more information, see:

-   [Release Notes for System Center 2016](../../get-started/Release-Notes-for-System-Center-2016.md)

-   [System Requirements for System Center Technical Preview](../../system-requirements/System-Requirements-for-System-Center-Technical-Preview.md)

### Operations Manager Administrators Role Assignment
The System Center 2016 Technical Preview - Operations Manager, setup procedure automatically assigns the Administrators group on the local computer to the Operations Manager Administrators role. You must be logged on with an account that has local Administrator rights to run Setup on the first management server that you install; this ensures that you can open the Operations console after Setup is completed. When you install additional management servers, you must use a Domain account of which you are a member.

### Required Accounts
During setup, you are prompted for two accounts, the **management server action account** and the **System Center Configuration service and System Center Data Access service** account. In Operations Manager, you can use the same account for both services.

If you install Reporting, you are prompted for two additional accounts, **the Data Warehouse Write account** and the **Data Reader account**. These accounts are created as domain user accounts and added to the local Administrators group on the target server.

> [!NOTE]
> If you create a specific account for installation, this account must be a member of the **sysadmin** server role for Microsoft SQL Server, but also have access to the master database.

> [!NOTE]
> If you install multiple management servers, you are prompted for a **management server action account** and a **System Center Configuration service and System Center Data Access service account** each time you add a management server. You must provide the same accounts for each installation.

|Account|Description|Permissions|
|-----------|---------------|---------------|
|Management server action account|This account is used to carry out actions on monitored computers across a network connection.|To save time, specify a domain-based account. We recommend that you create an account for this purpose that has local administrative credentials. You should not use an account that has domain administrative credentials.|
|System Center Configuration service and System Center Data Access service account|This account is one set of credentials that is used to update and read information in the operational database. Operations Manager ensures that the credentials used for the System Center Data Access service and System Center Configuration service account are assigned to the sdk_user role in the operational database.|This account can be configured as either Local System or as a domain account. The account must have local administrative credentials. For cases where the operational database is hosted on a remote computer that is not a management server, a domain account must be used. For better security, we recommend that you use an account different from the one used for the management server action account.|
|Data Warehouse Write account|The Data Warehouse Write account writes data from the management server to the Reporting data warehouse and reads data from the operational database.|This account is assigned write permissions on the Data Warehouse database and read permissions on the operational database. **Note:** Ensure that the account you plan to use for the Data Warehouse Write account has SQL Server Logon rights and has logon rights for the computers hosting both the operational database and the reporting data warehouse. Otherwise, Setup fails, and all changes are rolled back. This might leave SQL Server Reporting Services in an inoperable state.|
|Data Reader account|The Data Reader account is used to define which account credentials SQL Server Reporting Services uses to run queries against the Operations Manager reporting data warehouse.|The account should be configured as a domain account. **Note:** Ensure that the account you plan to use for the Data Reader account has SQL Server logon rights and Management Server logon rights.|

### SQL Server Requirements
System Center 2016 Technical Preview - Operations Manager requires access to an instance of a server running Microsoft SQL Server 2008 SP1, SQL Server 2008 R2, or SQL Server 2008 R2 SP1. This instance can be located on a separate computer from the management servers in a distributed installation or on the first management server in the management group. In either case, the instance of Microsoft SQL Server 2008 SP1, SQL Server 2008 R2, or SQL Server 2008 R2 SP1 must already exist and be accessible before you start your first management server installation. The SQL Server Collation setting must be a supported value, and SQL Full Text Search must be enabled.

Operations Manager requires access to an instance of a server running a supported version of Microsoft SQL Server. This instance can be located on a separate computer from the management servers in a distributed installation or on the first management server in the management group. In either case, the instance of Microsoft SQL Server must already exist and be accessible before you start your first management server installation. The SQL Server Collation setting must be a supported value, and SQL Full Text Search must be enabled.

During setup, you are prompted for the following:

-   The SQL Server database server name and instance name. If you have installed SQL Server by using the default instance, you only have to specify the SQL Server name.

You can accept the default values for or set:

-   SQL Server Port number. By default, 1433.

-   A new operational database (for first management server installation in the management group) or an existing operational database (for installing additional management servers in an existing management group).

-   The database name. By default, OperationsManager.

-   The starting database size. By default, 1000 MB.

-   The Data file and Log folder locations. By default, these are C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\Data or C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\Log as appropriate to the SQL Server defaults.

> [!IMPORTANT]
> If TCP/IP is disabled on a remote server that is hosting the SQL Server database, Setup will not be able to connect to the SQL Server database. To resolve this issue, enable TCP/IP on the remote server.

Ensure that SQL Server Reporting Services has been correctly installed and configured. For more information about how to install and configure SQL Server 2012 Reporting Services, see [SQL Server Installation (SQL Server 2008 R2)](http://go.microsoft.com/fwlink/p/?LinkId=146943).
