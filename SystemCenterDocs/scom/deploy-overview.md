---
ms.assetid: 2369cbef-5f0d-4fc2-8288-ea315aab20b6
title:  Deploying System Center 2016 Operations Manager
description: This article provides a high-level overview of what preparations you should make before deploying Operations Manager 2016.  
author: mgoedtel
ms.author: carmonm
manager: cfreemanwa
ms.date: 01/25/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Deploying System Center 2016 - Operations Manager

>Applies To: System Center 2016 - Operations Manager

All System Center 2016 - Operations Manager individual management group deployments will either be an "all-in-one" installation, where all features are loaded on a single server, or a distributed installation. Installations can then be combined together to form an overall Operations Manager infrastructure that consists of multiple management groups. These management groups can then relate to each other as your business needs require.

This section of the Deployment Guide describes an individual management group deployment, where you have one management group, but the features of Operations Manager are either installed on a single server or distributed over several servers.

-   [Single Server Deployment of Operations Manager](deploy-single-server.md)

-   [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md)

For information about connecting management groups, see [Connecting Management Groups in Operations Manager](http://go.microsoft.com/fwlink/p/?LinkID=207755).

## Before you begin

Before you begin your deployment, you should read the release notes, and ensure that your server meets the minimum system requirements for Operations Manager. For more information, see:

-   [Release Notes for System Center 2016](~/system-center.md)

-   [System Requirements for System Center 2016 - Operations Manager](../orchestrator/system-requirements.md)

### Operations Manager Administrators role assignment

The System Center 2016 - Operations Manager, setup procedure automatically assigns the Administrators group on the local computer to the Operations Manager Administrators role. You must be logged on with an account that has local Administrator rights to run Setup on the first management server that you install; this ensures that you can open the Operations console after Setup is completed. When you install additional management servers, you must use a Domain account of which you are a member.

### Required accounts

During setup, you are prompted for three accounts, the **management server action account**,  the **System Center Configuration service and System Center Data Access service** account, and the **Data Warehouse Write account**. In Operations Manager, you can use the same account for the **System Center Configuration and System Center Data Access service** services.

If you install Reporting, you are prompted for one additional account, the **Data Reader account**. For further information regarding the specific privileges they need to be granted before running setup and what rights it is assigned during setup, please review the [Service, User, and Security accounts](plan-security-accounts.md) guidance.  

> [!NOTE]
> If you create a specific account for installation, this account must be a member of the **sysadmin** server role for Microsoft SQL Server, but also have access to the master database.

> [!NOTE]
> If you install multiple management servers, you are prompted for a **management server action account** and a **System Center Configuration service and System Center Data Access service account** each time you add a management server. You must provide the same accounts for each installation.


### SQL Server requirements

System Center 2016 - Operations Manager requires access to an instance of a server running Microsoft SQL Server 2012, 2014, or SQL Server 2016. This instance can be located on a separate computer from the management servers in a distributed installation or on the first management server in the management group. In either case, the instance of Microsoft SQL Server must already exist and be accessible before you start your first management server installation. The SQL Server Collation setting must be a supported value, and SQL Full Text Search must be enabled.  To review which versions of SQL Server are supported for Operations Manager, see [SQL Server requirements](plan-sqlserver-design.md#sql-server-requirements) in the SQL Server Design Considerations planning topic.   

During setup, you are prompted for the following:

-   The SQL Server database server name, Always On availability group name, or primary cluster name and instance name. If you have installed SQL Server by using the default instance, you only have to specify the SQL Server name.  

You can accept the default values for or set:

-   SQL Server Port number. By default, 1433.

-   A new operational database (for first management server installation in the management group) or an existing operational database (when installing additional management servers in an existing management group).

-   The database name. By default, OperationsManager.

-   The starting database size. By default, 1000 MB.

-   The Data file and Log folder locations. By default, these are C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\Data or C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\Log as appropriate to the SQL Server defaults.

> [!IMPORTANT]
> If TCP/IP is disabled on a remote server that is hosting the SQL Server database, Setup will not be able to connect to the SQL Server database. To resolve this issue, enable TCP/IP on the remote server.

Ensure that SQL Server Reporting Services has been correctly installed and configured. For more information about how to install and configure SQL Server 2014 Reporting Services, see [SQL Server Installation (SQL Server 2014)](https://msdn.microsoft.com/library/ms143711%28v=sql.120%29.aspx).  For more information about how to install and configure SQL Server 2016 Reporting Services, see [SQL Server Installation (SQL Server 2016)](https://msdn.microsoft.com/library/ms143711%28v=sql.130%29.aspx).

For additional information to help you properly plan your SQL Server configuration in support of Operations Manager, see [SQL Server Design Considerations](plan-sqlserver-design.md).  

## Next steps

- To deploy the Windows agent from the Operations console using the Discovery Wizard, review [Install Agent on Windows Using the Discovery Wizard](~/scom/manage-deploy-windows-agent-console.md)

- If you would like to manually install the Windows agent from the command line or automate the deployment using a script or other automation solution, review [Install Windows Agent Manually Using MOMAgent.msi](~/scom/manage-deploy-windows-agent-manually.md)

- If you would like to install the Nano Server agent from the command line or automate the deployment using a script or other automation solution, review [Install Agent on Nano Server](manage-deploy-windows-agent-nano.md)

- To deploy the agent to UNIX and Linux computers from the Operations console using the Discovery Wizard, review [Install Agent on UNIX and Linux Using the Discovery Wizard](~/scom/manage-deploy-crossplat-agent-console.md)
