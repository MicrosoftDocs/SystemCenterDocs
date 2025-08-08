---
ms.assetid: e252996f-c52c-4688-8a97-c0e70734b365
title: Reporting services Run As profiles in Management Pack for SQL Server Reporting Services
description: This article explains Reporting Services Run As Profiles.
author: epomortseva
ms.author: v-fkornilov
manager: evansma
ms.date: 11/01/2024
ms.topic: how-to
ms.service: system-center
ms.subservice: operations-manager
---

# Reporting Services Run As Profiles

Management Pack for SQL Server Reporting Services provides the following Run As profiles:

- **Microsoft SQL Server Discovery Run As Profile**

    This profile is used for the "MSSQL Reporting Services: Deployment Seed Discovery" workflow.

- **Microsoft SQL Server SCOM SDK Run As Profile**

    This profile is used for the "MSSQL Reporting Services: Native Mode Deployment" discovery and the "All deployment instances are discovered" unit monitor.

- **Microsoft SQL Server Monitoring Run As Profile**

    This profile is used for the following **Unit Monitor** workflows:

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

    For the following **Performance Rule** workflows:

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
    - Working Set Maximum (GB)
    - Working Set Minimum (GB)

By default, all discoveries, monitors, and rules in the management pack use Run As accounts are defined in the **Default Action Account** Run As profile.

If the default action account for the given system doesn't have the necessary permissions to discover and monitor instances of SQL Server Reporting Services, those systems can be bound to more specific credentials in **Microsoft SQL Server** Run As profiles.

> [!IMPORTANT]
> It's not recommended to use the **Local System account** or **HealthService SSID** because it's a specific case to monitor SQL Server Reporting Services. Some workflows run on the server hosting a Reporting Services instance and try to reach the Reporting Services database commonly installed on another computer. You'll need to provide computer accounts of all the servers hosting SQL Server Reporting Services instances with the required permissions to access the Reporting Services databases. A domain account is a more suitable and secure option.

## Configuring Run As Profiles

To configure Run As profiles, perform the following steps:

1. Identify the names of the target computers where the default action account has insufficient rights to monitor SQL Server Reporting Services.

2. For each system, create or use an existing set of credentials that have at least the set of privileges described in [Least-Privilege Monitoring](reporting-services-management-pack-least-privilege-monitoring.md).

3. For each set of credentials identified in Step 2, ensure that a corresponding **Run As Account** exists in the management group. Create a **Run As Account**, if necessary.

4. Configure mapping between targets and Run As accounts on the **Run As Accounts** tab of each of the Run As profiles.
