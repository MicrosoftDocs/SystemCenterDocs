---
ms.assetid: e252996f-c52c-4688-8a97-c0e70734b365
title: Reporting Services Run As Profiles
description: This article explains Reporting Services Run As Profiles
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
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
        - CPU utilization (%)
        - Database accessible
        - Instance configuration state
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

By default, all discoveries, monitors, and rules defined in the management pack use accounts defined in the **Default Action Account** Run As profile.

If the default action account for the given system does not have necessary permissions to discover and monitor instances of SQL Server Analysis Services, those systems can be bound to more specific credentials in **Microsoft SQL Server** Run As profiles.

>[!NOTE]
>It is not recommended to use the Local System account or HealthService SSID because its special case to monitor SSRS. Some workflows run on the server hosting an SSRS instance and try to reach the SSRS Database usually installed on another server. You will need to provide computer accounts of all servers hosting SSRS instances with the required permissions to access the SSRS Database. A domain account is a more preferable option.

## Configuring Run As Profiles

To configure Run As profiles, perfrom the following steps:

1. Identify the names of the target computers where the default action account has insufficient rights to monitor SQL Server Reporting Services.

2. For each system, create or use an existing set of credentials that have at least the set of privileges described in [Least-Privilege Monitoring](rsmp-least-privilege-monitoring.md).

3. For each set of credentials identified in Step 2, make sure that a corresponding **Run As Account** exists in the management group. Create a **Run As Account** if necessary.

4. Configure mapping between targets and Run As accounts on the **Run As Accounts** tab of each of the Run As profiles.

Refer to the [Reporting Services Run As Profiles](rsmp-run-as-profiles.md) section for the detailed explanation of what Run As profiles are defined in the management pack.