---
ms.assetid: 6d774c55-b334-489e-977e-206b2c6bc2e9
title: Known issues and troubleshooting in Management Pack for Azure SQL Database
description: This article explains known issues and troubleshooting in Management Pack for Azure SQL Database
author: Anastas1ya
ms.author: jsuri
ms.date: 11/01/2024
ms.topic: troubleshooting-known-issue
ms.service: system-center
ms.subservice: operations-manager
---

# Known Issues and Troubleshooting in Management Pack for Azure SQL Database

This article lists the known issues for Management Pack for Azure SQL Database.

> [!WARNING]
> There is an issue in the **SQL Server 2019 CU8 and higher** which is used as the **OperationsManager** database-hosted SQL server in the System Center Operations Manager. In the case of this configuration, the Azure SQL Database MP failed to import into the System Center Operations Manager with the following error: `MPInfra_p_ManagementPackInstall failed with exception: Conversion failed when converting from a character string to uniqueidentifier.` It's related to the [Scalar UDF Inlining](/sql/relational-databases/user-defined-functions/scalar-udf-inlining) feature that improves the performance of queries that invoke scalar UDFs starting with SQL Server 2019. [See the workaround below](#disable-scalar-udf-inlining-without-changing-the-database-compatibility-level).

|Issue title|Behavior / Symptom|Known workaround|
|-|-|-|
|Templates can't be removed|When removing a monitoring template, the following message appears: “The item you're trying to delete can't be deleted because another object references it…”. Since System Center Operations Manager doesn't support the cascade templates removal, you must manually remove all monitors that target the server defined by the template before removing the template.|In the System Center Operations Manager console, navigate to **Authoring** > **Management Pack Objects** > **Monitors**, scope the list to the server defined by the template and remove all custom monitors.|
|Some elastic pools may not be discovered|Elastic pools with no databases aren't discovered.|No resolution.|
|Error messages are received when Azure SQL Server is discovered by several templates simultaneously|If several Azure SQL Database templates with different user rights are used simultaneously to discover the same Azure SQL Servers, error events (ID 6302) appear in the Operations Manager Event Viewer.|Each Azure SQL Server must be discovered by a single template only.|
|Rules and monitors may provide incorrect data if the default interval override values are changed|If the value of the **Interval (seconds)** parameter is set to lower than the default value, rules and monitors may provide incorrect data.|The **Interval (seconds)** parameter must be set to no lower than the default value.|
|The server exclude list option may work incorrectly|The server exclude list may behave incorrectly. The masks that were configured may disappear from the list and some performance may still be received.|No resolution.|
|Some performance collection rules fail to collect data when REST+T-SQL is enabled|Some performance collection rules may not work due to lack of required T-SQL permissions.|Run T-SQL queries specified in [Configuring Azure REST API Monitoring](azure-sql-management-pack-monitoring-types.md#set-up-azure-rest-api-monitoring).|
|The **Use T-SQL for monitoring** checkbox configuration can't be saved|After creating the Azure SQL Database monitoring template using **Azure Service Principal** authentication mode and the **Use Existing Run As Profile SPN Configuration** option, the **Use T-SQL for monitoring** checkbox remains enabled regardless of the user choice.|No resolution.|
|The monitored objects become unavailable if the management server is changed in the resource pool|The monitored objects become unavailable in System Center Operations Manager if the management server is changed in the resource pool. An alert with the following description is displayed in the System Center Operations Manager log: “The pool member no longer owns any managed objects assigned to the pool because half or fewer members of the pool have acknowledged the most recent lease request. The pool member has unloaded the workflows for managed objects it previously owned.”|Wait until the objects are processed on a new management server.|
|The Azure portal may stop retrieving results in responses to Azure REST API requests from some performance rules|In cases of a high number of databases (about 1000 databases), the Azure portal may stop retrieving results in responses to Azure REST API requests from some performance rules.|No resolution.|
|SQL connection to the Azure SQL Databases may fail if the number of databases is too high|If the number of databases is over 2000 databases, the SQL connection to Azure SQL Databases may fail with the exceptions described in [Azure SQL Databases Exceptions](#azure-sql-databases-exceptions). As a result, the **Database Connection Availability** monitor changes its state from **Healthy** to **Warning**. It may also affect workflows with T-SQL query datasources due to connection loss.|No resolution.|

## Azure SQL Databases Exceptions

The following is a list of exceptions that might occur if the number of databases exceeds 2000:

- A connection was successfully established with the server, but then an error occurred during the pre-login handshake.

- Connection Timeout Expired. The timeout period elapsed while attempting to consume the pre-login handshake acknowledgment. This could be because the pre-login handshake failed or the server was unable to respond back in time.

- A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server wasn't found or wasn't accessible. Verify that the instance name is correct and the SQL Server is configured to allow remote connections.

## Disable Scalar UDF Inlining without changing the database compatibility level

To import the Azure SQL Database management pack on an environment with the Operations Manager database hosted on the SQL Server 2019 and higher, you can temporarily disable at the Operations Manager database the Scalar UDF Inlining at the database scope. To disable it, execute the following statement within the context of the applicable database:

```SQL
USE OperationsManager;
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF;
```

When the importing process of the management pack is successfully done, you can enable back the Scalar UDF Inlining at the Operations Manager database:

```SQL
USE OperationsManager;
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = ON;
```
