---
ms.assetid:
title: include file
description: include file to provide system requirements for Orchestrator 2022, includes general performance and scalability guidance for consideration as part of your design planning of your Orchestrator's deployment.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 01/31/2024
ms.custom: na
ms.service: system-center
ms.subservice: Orchestrator
ms.topic: include
ms.update-cycle: 1095-days
---

## System requirements for System Center 2022 - Orchestrator

The following sections provide general performance and scalability guidance for System Center 2022 - Orchestrator and state the recommended hardware configurations for various workloads. As System Center 2022 is built to be flexible and scalable, the hardware requirements for specific scenarios may differ from the guidelines that are presented here.

## Hardware

| Orchestrator Server Role | x64 Processor (min) | Memory (min) | Disk space (min) |
|:-----|:----|:---- |:---- |
|All server roles|2.1 GHz, dual-core CPU |2 GB|200 MB

## Server operating system

The following versions of Windows Server operating system are supported.

| Component | Windows Server 2019 Standard, Datacenter with Desktop Experience | Windows Server 2022 Standard, Datacenter with Desktop Experience |
|:--- |:---|:--- |:--- |
|All server roles|Supported|Supported|


## Client operating system

The following versions of Windows client operating system are supported for the Orchestrator.

|Component| Windows Server 2019 Standard, Datacenter with Desktop Experience| Windows Server 2022 Standard, Datacenter with Desktop Experience |
|:--- |:---|:--- |
|Runbook Designer|supported|Supported|

## Running the Setup

Install the [Microsoft Visual C++ Redistributable](/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022&preserve-view=true) before running the Setup executable (SetupOrchestrator.exe).

## Software

The following software is required for a full installation of Orchestrator on a single computer:

- Microsoft SQL Server 2019 – Orchestrator requires only the basic SQL Server features found in the Database Engine Service. No additional features are required. Orchestrator supports SQL_Latin1_General_CP1_CI_AS for collation. The installation wizard uses SQL_Latin1_General_CP1_CI_AS as the default collation to create the orchestration database. For more information, see the section on [SQL Server](#sql-server).

    > [!NOTE]
    > Management servers and runbook servers installed on the same computer must use the same database.

- Microsoft Internet Information Services (IIS) – Orchestrator Setup enables IIS if it isn't enabled.

- Microsoft .NET Framework 4.5 or later.

- Ensure that [Microsoft OLE DB Driver for SQL Server v18](/sql/connect/oledb/release-notes-for-oledb-driver-for-sql-server?view=sql-server-ver16#previous-releases&preserve-view=true) is installed on machines that host the Management Server, Runbook Service, Runbook Designer, or the Web API Service.

- Join the computer to an Active Directory domain.

## SQL Server

> [!NOTE]
> - For the supported versions of SQL, use the service packs/cumulative updates that are currently in support by Microsoft.
> -	SQL *Always ON*  is supported, except in cases where configuration is done on multi subnets.

**SQL version** | **Supported**
--- | ---
**[SQL Server 2022](https://www.microsoft.com/sql-server/sql-server-2022)** | Y
**[SQL Server 2019](/lifecycle/products/?terms=SQL+Server+2019)** | Y
**[SQL Server 2017](/lifecycle/products/?terms=SQL+Server+2017)** | Y

>[!NOTE]
> When you deploy Orchestrator in an **Always ON** scenario, the Database Availability wizard prompts for the database encryption key password. For information on how to retrieve the password, see [database migration](../orchestrator/migrate-orchestrator-between-environments.md).

## .NET requirements

Orchestrator requires .NET Framework 4.5 or later to run; we recommend installing .NET Framework 4.7.2.

Orchestrator Web API requires the following versions of .NET Core and Hosting Bundles:

|SCO version|.NET Core|
|---|---|
|2022 RTM|[.NET Core 5 Hosting Bundle](https://dotnet.microsoft.com/download/dotnet/thank-you/runtime-aspnetcore-5.0.17-windows-hosting-bundle-installer)|
|2022 UR1, UR2|[.NET Core 6 Hosting Bundle](/aspnet/core/host-and-deploy/iis/hosting-bundle?view=aspnetcore-6.0&preserve-view=true)|

## Virtualization

Deploying and running Orchestrator on a virtualized operating system is fully supported. The software requirements are the same as those listed above. Any of the Orchestrator roles can also be run on a virtualized server running in Microsoft Azure.

