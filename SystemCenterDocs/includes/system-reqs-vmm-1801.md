---
ms.assetid: 0b604566-dab0-4e9e-90e1-ff62861c4396
title: include file
description: include article to detail the system requirements for VMM 1801
author: Jeronika-MS
ms.author: v-gajeronika
ms.date:  04/26/2018
ms.topic:  include
ms.service:  system-center
ms.subservice:  virtual-machine-manager
---

## VMM 1801 system requirements

The following sections describe the scalability information, hardware, software, and SQL Server requirements for VMM 1801, and summarize the support for the servers managed in the VMM fabric.

## Capacity limits

The following table provides the scale limits that were tested for System Center 1801 Virtual Machine Manager. There are various factors that impact the scale limits, such as hardware configuration, network, topology, and others.

The [planning guide](../vmm/plan-install.md) provides the details about how these factors can be adapted to specific requirements.

**Entity** | **Recommended maximum count**
--- | ---
Physical hosts | 1000
Virtual Machines | 25000
Services | 1000
User roles | 1000
Clouds | 20
Virtual networks| 2000
logical networks| 20
Library resources| 1000
Library Objects (templates, profiles)| 100

## Hardware

  **Hardware** | **VMM server** | **VMM database** | **VMM  library** | **VMM console**
  --- | --- | --- | --- | ---
  **Processor (minimum)** | 8 core Pentium 4, 2 GHz (x64) | 8 core Pentium 4, 2.8 GHz | 4 core Pentium 4, 2.8 GHz | 2 core Pentium 4, 1 GHz CPU
  **Processor (recommended)** | 16-core, 2.66 GHz CPU | 16 core 2.6 GHz CPU | 4 core 2.8 GHz CPU | 2 core 2 GHz CPU
  **RAM (minimum)** | 4 GB | 8 GB | 2 GB | 4 GB
  **RAM (recommended)** | 16 GB | 16 GB | 4 GB | 4 GB
  **Hard drive (minimum)** | 4 GB | 50 GB | Based on size/amount of stored files | 10 GB
  **Hard drive (recommended)** | 10 GB | 200 GB | Based on size/amount of stored files | 10 GB


## Server operating system

**Operating system** | **VMM server** | **Remote VMM library** | **Remote VMM database**
--- | --- | --- | ---
Windows Server 2012 R2 Standard/Datacenter (Server Core)| N | Y | If supported by SQL Server version
Windows Server 2012 R2 Standard/Datacenter (with desktop experience)| N | Y | If supported by SQL Server version
Windows Server 2016 (Server Core)| Y | N | If supported by SQL Server version
Windows Server 2016 (with desktop experience) | Y | Y | If supported by SQL Server version
Windows Server 1709 | Y | Y | Y

## VMM console operating system

**Operating system** | **Supported**
--- | ---
Windows 10 Enterprise | Y
Windows Server 2012 R2 Standard, Datacenter | Y
Window Server 2016 Standard, Datacenter | Y


## SQL Server

> [!NOTE]
> - For the supported versions of SQL, use the service packs that are currently in support by Microsoft.  
> - For the below supported SQL versions, Standard, Enterprise and Datacenter (64-bit) editions are supported, based on the availability.

**SQL version** | **Supported**
--- | ---
SQL Server 2008 | N
SQL Server 2012 and SPs as detailed [here](/lifecycle/products/?terms=SQL+Server+2012)| Y
SQL Server 2014 and SPs as detailed [here](/lifecycle/products/?terms=SQL+Server+2014) | Y
SQL Server 2016 and SPs as detailed [here](/lifecycle/products/?terms=SQL+Server+2016) | Y
SQL Server command line utilities | Install on VMM server if you want to deploy SQL Server data-tier apps in the VMM fabric.<br/><br/> Install SQL Server 2012 Command-Line Utilities from the [Microsoft® SQL Server® 2012 Feature Pack](https://www.microsoft.com/download/details.aspx?id=56041) <br/> or <br/> Install the SQL Server 2014 Command-Line Utilities from the [Microsoft® SQL Server® 2014 Feature Pack](https://go.microsoft.com/fwlink/?LinkID=529794)  <br/> or <br/> Install the SQL Server 2016 Command-Line Utilities from the [Microsoft® SQL Server® 2016 Feature Pack](https://www.microsoft.com/download/details.aspx?id=56833 )<br/><br/> Not required for VMM installation.

## Virtualization

**VM** | **Supported**
--- | ---
VMM management server | The VMM management server can be installed on a VM.<br/><br/> If you use dynamic memory, set the start RAM of the VM to at least 2048 MB.<br/><br/> Don't install on a server running Hyper-V.<br/><br/> You can deploy the VMM management server (physical or VM) in a highly available cluster.
VMM console | You can install the VMM console on a VM.



## Installation components

These components should be installed on the server before you install VMM.

**Component** | **VMM server** | **VMM console**
--- | --- | ---
Active Directory | The VMM management server must be a domain member.<br><br> The computer name shouldn't exceed 15 characters. | A computer with the VMM console installed should be a domain member.
Windows ADK | [Download](/windows-hardware/get-started/adk-install) Windows ADK for Windows 10 | Not applicable
PowerShell | PowerShell 5.0 | PowerShell 4.0, 5.0
.NET | 4.6 | 4.5, 4.5.1, 4.5.2, 4.6


## Servers in the VMM fabric

>[!NOTE]
> Hyper-V server 2016 and 2019 aren't supported.

**Operating system** | **Hyper-V host** | **SOFS** | **Update server** | **PXE server**
--- | --- | --- | --- | ---
Windows Server 2012 Standard/Datacenter | N | N | N | N
Windows Server 2012 R2 Standard/Datacenter | Y | Y | Y | Y
Windows Server 2016 | Y | Y | N | N
Windows Server 2016 (with desktop experience) | Y | Y | Y | Y
Windows Server 1709 | Y | Y | N | N

## VMware servers in the VMM fabric

**VMware** | **Supported**
--- | ---
ESX | ESX/ESXi 5.1, 5.5, 6.0
vCenter | 5.1, 5.5, 5.8, 6.0</td>
Supported | [Features and limitations](../vmm/manage-VMware-hosts.md)

## VMs in the VMM fabric

**Guest operating system** | **Supported**
--- | ---
Hyper-V VMs | Any guest running on supported Hyper-V hosts.<br/><br/> Learn more about support for [2016](/windows-server/virtualization/hyper-v/Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows) and [earlier versions](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/mt126277(v=ws.11)).
VMware VM | Any VM running on supported VMware servers. [Learn more](http://www.VMware.com/resources/compatibility/search.php?deviceCategory=software).