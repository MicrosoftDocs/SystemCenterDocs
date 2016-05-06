---
title: Guidance for Installing Service Manager on Virtual Machines
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 866fa7d8-0803-40d3-ae63-765f4850159e
---
# Guidance for Installing Service Manager on Virtual Machines
This topic provides guidance that you have to consider when you install [!INCLUDE[scsm_threshold_1](./Token/scsm_threshold_1_md.md)] in a Hyper\-V virtual environment. If you are installing Microsoft SQL Server into an environment without Hyper\-V, consult your vendor’s documentation for guidance regarding the use of SQL Server.

## Deploying SQL Server in a Virtual Environment
Before you deploy SQL Server in a Hyper\-V environment, see [Running SQL Server 2008 in a Hyper-V Environment](http://go.microsoft.com/fwlink/p/?LinkID=144622). Keep the following in mind when you prepare a virtual environment for SQL Server:

-   Using a dynamic virtual hard drive \(VHD\) can decrease performance. We do not recommend using a VHD.

-   Allocate at least two virtual CPUs for the instance of SQL Server.

-   Do not allocate more virtual CPUs than the number of available logical CPUs.

-   If you observe a drop in [!INCLUDE[smshort12](./Token/smshort12_md.md)] performance in a virtual environment, check CPU and memory utilization on the virtual machines that are hosting the instance of SQL Server and the [!INCLUDE[smshort12](./Token/smshort12_md.md)] management server. If CPU utilization is near 100 percent, either allocate additional virtual CPUs or reduce the number of concurrent [!INCLUDE[smcons](./Token/smcons_md.md)] sessions.

## Memory
The amount of memory you have in your logical computer and the amount of memory you allocate to each virtual machine are critical. If you deploy an instance of SQL Server, [!INCLUDE[smshort12](./Token/smshort12_md.md)] management server, and [!INCLUDE[smcons](./Token/smcons_md.md)] to the same virtual machine, the memory requirements are cumulative. You need enough memory to meet the requirements of each part of [!INCLUDE[smshort12](./Token/smshort12_md.md)]. In this environment, 8 gigabytes \(GB\) of memory is the minimum recommended amount.

## Deploying Service Manager Databases in a Virtual Environment
In this release, if you are installing [!INCLUDE[smshort12](./Token/smshort12_md.md)] and data warehouse databases on virtual machines, we recommend that you use one virtual machine for the [!INCLUDE[smshort12](./Token/smshort12_md.md)] database and another virtual machine for the data warehouse databases. Furthermore, each virtual machine should be configured for two CPUs.


