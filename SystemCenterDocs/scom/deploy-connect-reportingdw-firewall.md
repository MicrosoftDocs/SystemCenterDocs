---
ms.assetid:
title: Connect to the Reporting Data Warehouse Across a Firewall
description: This article describes how to configure a System Center Operations Manager Report server behind a firewall.
author: jyothisuri
ms.author: jsuri
ms.date: 04/17/2025
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
---

# Connect to the reporting data warehouse across a firewall

This article describes how to configure your environment to support placing the reporting data warehouse behind a firewall for System Center Operations Manager.

In an environment where the reporting data warehouse is separated from the management server and reporting server by a firewall, you can't use Integrated Windows Authentication. You need to configure SQL Server authentication. The following sections explain how to enable SQL Server authentication between the management server, the reporting server, and the reporting data warehouse. The following diagram shows how SQL Server authentication works.

![Diagram that illustrates SQL Server authentication.](media/deploy-connect-reportingdw-firewall/reportingdw-firewall-comms.png)

## Management server and reporting data warehouse

Use the following steps to enable SQL Server authentication:

1. On the computer that hosts the reporting data warehouse, create a SQL Server sign-in in the proper role for reader and writer. The credentials that you supply for this account must be a member of the following roles in the data warehouse database on the computer running SQL Server:

   * **OpsMgrWriter**  
   * **db_owner** (only for the owning management group in the database)  

2. On the computer that hosts the management server, create a **Run As** account (of type **Simple**) by using the credentials from the previous step.

3. Associate this **Run As** account with the **Run As** profile called **Data Warehouse SQL Server Authentication Account**. Target this **Run As** profile to each management server. For more information, see [Create a Run As account and associate it with a Run As profile](manage-security-create-runas-link-profile.md).

If a firewall is between the management server and the reporting data warehouse, you have to open port 1433.

## Reporting server and reporting data warehouse

If a firewall or trust boundary exists between the reporting server and the reporting data warehouse, you need to establish point-to-point communications.  

The account that you specified as the **Data Reader** account during setup of reporting becomes the **Execution** account on the reporting server. You use this account to connect to the reporting data warehouse.

Identify what port number the computer running SQL Server on the reporting data warehouse is using. Enter this number into the **dbo.MT_DataWarehouse** table in the Operations Manager database. For more information, see [Configure settings for the data warehouse database](manage-sqlserver-communication.md#configure-settings-for-the-data-warehouse-database).

## Reporting server and management server separated by a firewall

If the reporting server and the management server are separated by a firewall, a "Could not verify if current user is in sysadmin Role" error message might appear when you're installing the reporting server role. This message might appear even if you opened the proper firewall ports.

This error occurs after you enter the computer name for the management server and select **Next**. This error might also appear because the reporting setup couldn't connect to the operational database. In this environment, determine what port number the SQL Server instance is using and configure the Operations Manager database to use the port number. For more information, see [Configure settings for the operational database](manage-sqlserver-communication.md#configure-settings-for-the-operational-database).

## Related content

* To understand the types of reports that are available and their purpose, review the [list of reports installed with Operations Manager](manage-reports-installed-during-setup.md).

* To understand how to preview your reports, how to save them with specific report parameters to minimize repeated entry of information or simplify the user experience, and how to export the report in various file formats, review [Run, save, and export a report](manage-reports-run-save-export.md).
