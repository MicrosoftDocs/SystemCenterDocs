---
ms.assetid: 6d774c55-b334-489e-977e-206b2c6bc2e9
title: Known issues and troubleshooting in Management Pack for Azure SQL Database
description: This article explains known issues and troubleshooting in Management Pack for Azure SQL Database
author: TDzakhov
manager: evansma
ms.date: 5/31/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Known Issues and Troubleshooting in Management Pack for Azure SQL Database

This article lists the known issues for Management Pack for Azure SQL Database.

|Issue title|Behavior / Symptom|Known workaround|
|-|-|-|
|Templates cannot be removed|When removing a monitoring template, the following message appears: “The item you are trying to delete cannot be deleted because another object references it…”. Since System Center Operations Manager does not support the cascade templates removal, you must manually remove all monitors that target the server defined by the template before removing the template.|In the System Center Operations Manager console, navigate to **Authoring** > **Management Pack Objects** > **Monitors**, scope the list to the server defined by the template and remove all custom monitors.|
|Some elastic pools may not be discovered|Elastic pools with no databases are not discovered.|No resolution.|
|Error messages are received when Azure SQL Server is discovered by several templates simultaneously|If several Azure SQL Database templates with different user rights are used simultaneously to discover the same Azure SQL Servers, error events (ID 6302) appear in the Operations Manager Event Viewer.|Each Azure SQL Server must be discovered by a single template only.|
|Rules and monitors may provide incorrect data if the default interval override values are changed|If the value of the **Interval (seconds)** parameter is set to lower than the default value, rules and monitors may provide incorrect data.|The **Interval (seconds)** parameter must be set to no lower than the default value.|
|The server exclude list option may work incorrectly|The server exclude list may behave incorrectly. The masks that were configured may disappear from the list and some performance may still be received.|No resolution.|
|Some performance collection rules fail to collect data when REST+T-SQL is enabled|Some performance collection rules may not work due to lack of required T-SQL permissions.|Run T-SQL queries specified in [Configuring Azure REST API Monitoring](azure-sql-management-pack-monitoring-types.md#configuring-azure-rest-api-monitoring).|
|The **Use T-SQL for monitoring** checkbox configuration cannot be saved|After creating the Azure SQL Database monitoring template using **Azure Service Principal** authentication mode and the **Use Existing Run As Profile SPN Configuration** option, the **Use T-SQL for monitoring** checkbox remains enabled regardless of the user choice.|No resolution.|
|The monitored objects become unavailable if the management server is changed in the resource pool|The monitored objects become unavailable in System Center Operations Manager if the management server is changed in the resource pool. An alert with the following description is displayed in the System Center Operations Manager log: “The pool member no longer owns any managed objects assigned to the pool because half or fewer members of the pool have acknowledged the most recent lease request. The pool member has unloaded the workflows for managed objects it previously owned.”|Wait until the objects are processed on a new management server.|
|The Azure portal may stop retrieving results in responses to Azure REST API requests from some performance rules|In cases of a high number of databases (about 1000 databases), the Azure portal may stop retrieving results in responses to Azure REST API requests from some performance rules.|No resolution.|
|SQL connection to the Azure SQL Databases may fail if the number of databases is too high|If the number of databases is over 2000 databases, the SQL connection to Azure SQL Databases may fail with the exceptions described in [Azure SQL Databases Exceptions](#azure-sql-databases-exceptions). As a result, the **Database Connection Availability** monitor changes its state from **Healthy** to **Warning**. It may also affect workflows with T-SQL query datasources due to connection loss.|No resolution.|
|Space monitoring limitations in Hyperscale service tier|[Monitoring workflows](#hyperscale-service-tier-limitations) may not collect data correctly for Hyperscale service tier databases.|As a temporary solution, turn off the performance rules and monitors. This issue will be fixed in one of the next updates of the management pack.|

## Azure SQL Databases Exceptions

The following is a list of exceptions that might occur if the number of databases exceeds 2000:

- A connection was successfully established with the server, but then an error occurred during the pre-login handshake.

- Connection Timeout Expired. The timeout period elapsed while attempting to consume the pre-login handshake acknowledgment. This could be because the pre-login handshake failed or the server was unable to respond back in time.

- A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and the SQL Server is configured to allow remote connections.

## Hyperscale Service Tier Limitations

The following workflows may not collect data correctly for the Hyperscale service tier databases:

- Rules
  - Free Space (MB)
  - Free Space Percentage
  - Used Space Percentage
  - Total Space Quota (MB)
- Unit monitors
  - Database Free Space
