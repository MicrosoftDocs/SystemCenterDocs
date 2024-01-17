---
ms.assetid: e252996f-c52c-4688-8a97-c0e70734b365
title: Reporting services Run As profiles in Management Pack for SQL Server Reporting Services
description: This article explains Reporting Services Run As Profiles
author: Anastas1ya
ms.author: v-ekaterinap
manager: evansma
ms.date: 12/8/2023
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Reporting Services Run As Profiles

After importing Management Pack for SQL Server Reporting Services, the following default Run As profiles are created:

- **Microsoft SQL Server Discovery Run As Profile**

    - Workflow Type: **Discovery**
        - MSSQL Reporting Services: Deployment Seed Discovery
        - Microsoft SQL Server Reporting Services (Discovery)

- **Microsoft SQL Server SCOM SDK Run As Profile**

    - Workflow Type: **Discovery**
        - MSSQL Reporting Services: Native Mode Deployment Discovery
    - Workflow Type: **Monitor**
        - All deployment instances are discovered

- **Microsoft SQL Server Monitoring Run As Profile**

    - Workflow Type: **Monitor**
        - Configuration conflict with SQL Server
        - Securables configuration status
        - CPU utilization (%)
        - Database accessible
        - Instance configuration state
        - Product version compliance
        - Memory consumed by others
        - Memory consumed by SSRS Instance
        - Misconfigured data sources
        - Number of failed report executions
        - Report manager accessible
        - Temporary database accessible
        - Web service accessible
        - Windows service state

    - Workflow Type: **Rule**
        - CPU utilization (%)
        - Failed report executions per minute
        - Failed report executions per minute (Deployment)
        - Memory consumed by other processes (%)
        - Memory consumed by SSRS (GB)
        - Number of reports
        - Number of shared data sources
        - Number of subscriptions
        - On-demand execution failures per minute
        - On-demand executions per minute
        - Report executions per minute
        - Report executions per minute (Deployment)
        - Scheduled execution failures per minute
        - Scheduled executions per minute
        - Total memory consumed on the server (GB)
        - Total memory on the Server (GB)
        - WorkingSetMaximum (GB)
        - WorkingSetMinimum (GB)

By default, all discoveries, monitors, and rules defined in the management pack use accounts are defined in the **Default Action Account** Run As profile.

If the default action account for the given system doesn't have the necessary permissions to discover and monitor instances of SQL Server Analysis Services, those systems can be bound to more specific credentials in **Microsoft SQL Server** Run As profiles.

> [!NOTE]
> It's not recommended to use the Local System account or HealthService SSID because it's a special case to monitor SSRS. Some workflows run on the server hosting an SSRS instance and try to reach the SSRS Database usually installed on another server. You'll need to provide computer accounts of all the servers hosting SSRS instances with the required permissions to access the SSRS Database. A domain account is a more preferable option.

## Configuring Run As Profiles

To configure Run As profiles, perform the following steps:

1. Identify the names of the target computers where the default action account has insufficient rights to monitor SQL Server Reporting Services.

2. For each system, create or use an existing set of credentials that have at least the set of privileges described in [Least-Privilege Monitoring](reporting-services-management-pack-least-privilege-monitoring.md).

3. For each set of credentials identified in Step 2, ensure that a corresponding **Run As Account** exists in the management group. Create a **Run As Account**, if necessary.

4. Configure mapping between targets and Run As accounts on the **Run As Accounts** tab of each of the Run As profiles.

## SQL Server and SQL Server Reporting Services Run As Profiles

To use separate accounts for monitoring of DB Engine, SSRS, and SSAS, create three different Windows accounts, and configure each account in each Run As profile according to the following table.

|Monitoring Account|[Association] Used for|
|-|-|
|SQL Server DB Monitoring Opt. # 1|**[Class]** SQL Server Components <br/> **[Class]** SQL Server DB Engine|
|SQL Server DB Monitoring Opt. # 2|**[Group]** SQL Server Components|
|SQL Server AS Monitoring|**[Class]** SSAS Seed <br/> **[Class]** SSAS Instance|
|SQL Server RS Monitoring|**[Class]** SSRS Deployment Seed <br/> **[Class]** Microsoft SQL Server Reporting Services Instance Seed <br/> **[Class]** Microsoft SQL Server Reporting Services (Native Mode) <br/> **[Class]** SSRS Deployment|

> [!NOTE]
> For the SQL Server DB account, use either **SQL Server DB Monitoring Opt. # 1** or **SQL Server DB Monitoring Opt. # 2**.
