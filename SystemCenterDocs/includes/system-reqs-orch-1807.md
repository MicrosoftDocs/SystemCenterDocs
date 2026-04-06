---
ms.assetid: 1e6e82dd-2ba6-45f2-8340-8efaeae1d4a6
title: include file
description: include file to provide system requirements for Orchestrator 1807, includes general performance and scalability guidance for consideration as part of your design planning of your Orchestrator's deployment.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 08/31/2018
ms.custom: na
ms.service: system-center
ms.subservice: Orchestrator
ms.topic: include
ms.update-cycle: 1095-days
---

## System requirements for System Center 1807 - Orchestrator

The following sections provide general performance and scalability guidance for System Center 1807 - Orchestrator and state the recommended hardware configurations for various workloads. As System Center 1807 is built to be flexible and scalable, the hardware requirements for specific scenarios may differ from the guidelines that are presented here.

## Hardware

| Orchestrator Server Role | x64 Processor (min) | Memory (min) | Disk space (min) |
|:-----|:----|:---- |:---- |
|All server roles|2.1 GHz, dual-core CPU |2 GB|200 MB

## Server operating system

The following versions of Windows Server operating system are supported.

| Component | Windows Server 2012 R2 Standard, Datacenter | Windows Server 2016 Standard, Datacenter with Desktop Experience | Windows Server Core 2016 |
|:--- |:---|:--- |:--- |
|All server roles|Supported|Supported|Not Supported


## Client operating system

The following versions of Windows client operating system are supported for Orchestrator.

|Component| Windows 7 | Windows 8 | Windows 8.1 | Windows 10 Enterprise |
|:--- |:---|:--- |:--- |:---|
|Runbook Designer|Not supported|Not Supported|Not Supported|Supported

## Software

The following software is required for a full installation of Orchestrator on a single computer:

* Microsoft SQL Server 2012, 2014, or 2016 – Orchestrator requires only the basic SQL Server features found in the Database Engine Service. No additional features are required. Orchestrator supports SQL_Latin1_General_CP1_CI_AS for collation. The installation wizard uses SQL_Latin1_General_CP1_CI_AS as the default collation to create the orchestration database. For more information, see the section on [SQL Server](#sql-server).

  > [!NOTE]
  > Management servers and runbook servers installed on the same computer must use the same database. The management server must run as a 32-bit application.

* Microsoft Internet Information Services (IIS) – Orchestrator Setup enables IIS if it isn't enabled.

* Microsoft .NET Framework 3.5 Service Pack 1 - Orchestrator Setup installs and enables .NET Framework 3.5 SP1 if it isn't installed and enabled.

* Microsoft .NET Framework 4
* [Microsoft SQL Server 2012 Native Client - QFE   (applies to SQL 2012/2014/2016)](https://www.microsoft.com/download/details.aspx?id=50402).

We recommend the following software for a full installation of Orchestrator on a single computer:

* Join the computer to an Active Directory domain.

> [!NOTE]
> On the first use of the Orchestration console, you're prompted to install Microsoft Silverlight on the computer if it isn't already installed. Install Silverlight 5.0.

## SQL Server

> [!NOTE]
> - For the supported versions of SQL, use the service packs that are currently in support by Microsoft.
> - SQL *Always ON*  is supported, except in the cases where configuration is done on multi subnets.

|                                                                 **SQL version**                                                                 | **Supported** |
|-------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
|                                                               **SQL Server 2008**                                                               |       N       |
| **SQL Server 2012 and SPs as detailed [here](/lifecycle/products/?terms=SQL+Server+2012)** |       Y       |
| **SQL Server 2014 and SPs as detailed [here](/lifecycle/products/?terms=SQL+Server+2014)** |       Y       |
| **SQL Server 2016 and SPs as detailed [here](/lifecycle/products/?terms=SQL+Server+2016)** |       Y       |

## .NET requirements

All Orchestrator server roles require .NET 3.5 SP1 in order to run the setup program. The Orchestrator Web Service requires .NET 4.5 with WCF Activation.

You can download .NET 3.5 SP1 at:

### To turn on WCF activation

1. On the Windows Start screen, select the **Server Manager** tile.
2.	On the **Manage** menu in the Server Manager console, select **Add Roles and Features**.
3.	Go through the wizard until you reach the **Features** page.
4.	Expand **.NET Framework 4.5 Features**.
5.	Select **.NET Framework 4.5** if it isn’t already selected.
6.	Expand **WCF Services**.
7.	Select **HTTP Activation** if it isn’t already selected.
8.	Select **Next** and follow the prompts to finish the installation. If you've problems, check the issues covered in [Troubleshoot Your Orchestrator Installation](/previous-versions/system-center/system-center-2012-R2/hh546549(v=sc.12)).


## Virtualization

Deploying and running Orchestrator on a virtualized operating system is fully supported. The software requirements are the same as those listed above. Any of the Orchestrator roles can also be run on a virtualized server running in Microsoft Azure.