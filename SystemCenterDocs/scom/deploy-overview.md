---
ms.assetid: 2369cbef-5f0d-4fc2-8288-ea315aab20b6
title: Deploy System Center Operations Manager
description: This article provides a high-level overview of what preparations you should make before deploying Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.custom: intro-deployment, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: install-set-up-deploy
ms.update-cycle: 180-days
---

# Deploy System Center Operations Manager

All System Center Operations Manager individual management group deployments will either be an "all-in-one" installation, where all features are loaded on a single server, or a distributed installation. Installations can then be combined together to form an overall Operations Manager infrastructure that consists of multiple management groups. These management groups can then relate to each other as your business needs require.

This section describes an individual management group deployment, where you have one management group, but the features of Operations Manager are either installed on a single server or distributed over several servers.

- [Single Server Deployment of Operations Manager](deploy-single-server.md)

- [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md)

For information about connecting management groups, see [Connecting Management Groups in Operations Manager](manage-connecting-mgmtgroups.md).

## Before you begin

::: moniker range=">=sc-om-2016 <=sc-om-2019"

Before you begin your deployment, you should read the release notes, and ensure that your server meets the minimum system requirements for Operations Manager. For more information, see:

- [Release Notes for System Center 2019 - Operations Manager](./release-notes-om.md?preserve-view=true&view=sc-om-2019)

- [Release Notes for System Center 2016 - Operations Manager](./release-notes-om.md?preserve-view=true&view=sc-om-2016)

- [System Requirements for System Center Operations Manager](./system-requirements.md)

::: moniker-end

::: moniker range=">=sc-om-2022"

Before you begin your deployment, you should read the release notes, and ensure that your server meets the minimum system requirements for Operations Manager. For more information, see:

- [System Requirements for System Center Operations Manager](./system-requirements.md)

::: moniker-end

### Operations Manager Administrators role assignment

The System Center Operations Manager setup procedure automatically assigns the Administrators group on the local computer to the Operations Manager Administrators role. You must be signed in with an account that has local Administrator rights to run Setup on the first management server that you install; this ensures that you can open the Operations console after Setup is completed. When you install additional management servers, you must use a Domain account of which you're a member.

### Required accounts

During setup, you're prompted for three accounts: the **management server action account**,  the **System Center Configuration service and System Center Data Access service** account, and the **Data Warehouse Write account**. In Operations Manager, you can use the same account for the **System Center Configuration and System Center Data Access service** services.

If you install Reporting, you're prompted for one additional account, the **Data Reader account**. For further information on the specific privileges to be granted before running setup and what rights are assigned to the accounts during setup, review the [Service, User, and Security accounts](plan-security-accounts.md) guidance.  

> [!NOTE]
> If you create a specific account for installation, this account must be a member of the **sysadmin** server role for Microsoft SQL Server and also have access to the master database.

> [!NOTE]
> If you install multiple management servers, you're prompted for a **management server action account** and a **System Center Configuration service and System Center Data Access service account** each time you add a management server. You must provide the same accounts for each installation.

### SQL Server requirements

System Center Operations Manager requires access to an instance of a server running Microsoft SQL Server. This instance can be located on a separate computer from the management servers in a distributed installation or on the first management server in the management group. In either case, the instance of Microsoft SQL Server must already exist and be accessible before you start your first management server installation. The SQL Server Collation setting must be a supported value, and SQL Full Text Search must be enabled.  To review which versions of SQL Server are supported for Operations Manager, see [SQL Server requirements](plan-sqlserver-design.md#sql-server-requirements) in the SQL Server Design Considerations planning article.

During setup, you're prompted for the following:

- The SQL Server database server name, Always On availability group name, or primary cluster name and instance name. If you have installed SQL Server using the default instance, you only have to specify the SQL Server name.  

You can accept the default values for or set:

- SQL Server Port number. By default, 1433.

- A new operational database (for first management server installation in the management group) or an existing operational database (when installing additional management servers in an existing management group).

- The database name. By default, OperationsManager.

- The starting database size. By default, 1000 MB.

- The Data file and Log folder locations. By default, these are C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\Data or C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\Log as appropriate to the SQL Server defaults.

> [!IMPORTANT]
> If TCP/IP is disabled on a remote server that is hosting the SQL Server database, Setup won't be able to connect to the SQL Server database. To resolve this issue, enable TCP/IP on the remote server.

Ensure that SQL Server Reporting Services has been correctly installed and configured. For more information about how to install and configure SQL Server Reporting Services, see [SQL Server Installation (SQL Server 2014)](/sql/reporting-services/install-windows/install-reporting-services-native-mode-report-server?viewFallbackFrom=sql-server-2014). For more information about how to install and configure SQL Server 2016 Reporting Services, see [SQL Server Installation (SQL Server 2016)](/sql/reporting-services/install-windows/install-reporting-services-native-mode-report-server).

For additional information to help you properly plan your SQL Server configuration in support of Operations Manager, see [SQL Server Design Considerations](plan-sqlserver-design.md).  

## Next steps

- To deploy the Windows agent from the Operations console using the Discovery Wizard, review [Install Agent on Windows Using the Discovery Wizard](~/scom/manage-deploy-windows-agent-console.md).

- If you would like to manually install the Windows agent from the command line or automate the deployment using a script or other automation solution, review [Install Windows Agent Manually Using MOMAgent.msi](~/scom/manage-deploy-windows-agent-manually.md).

- If you would like to install the Nano Server agent from the command line or automate the deployment using a script or other automation solution, review [Install Agent on Nano Server](manage-deploy-windows-agent-nano.md).

- To deploy the agent to UNIX and Linux computers from the Operations console using the Discovery Wizard, review [Install Agent on UNIX and Linux Using the Discovery Wizard](~/scom/manage-deploy-crossplat-agent-console.md).
