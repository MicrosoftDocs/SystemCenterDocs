---
description: This article is a primer for the necessary components to deploy DPM in your environment.
manager:  carmonm
ms.topic:  article
author:  markgalioto
ms.author: markgal
ms.prod:  system-center-threshold
keywords:  
ms.date: 10/24/2016
title:  Data Protection Manager
ms.technology:  data-protection-manager
ms.assetid:  e2a65d9d-5038-4a86-a495-f4745b78d040
---

# Preparing your environment for System Center 2016 Data Protection Manager

>Applies To: System Center 2016 - Data Protection Manager

Keep these requirements and considerations in mind when you deploy System Center 2016 Data Protection Manager (DPM).
If you’re evaluating your environment, see [System Requirements for System Center 2016](../orchestrator/system-requirements.md).

## First things first

Decide how you want to deploy DPM:

- **As a physical standalone server**—You can deploy DPM as a physical standalone server to back up on-premises data. Note that physical DPM servers can’t be deployed in a cluster, but you can manage multiple physical servers from a single console by installing Central Console on System Center Operations Manager.

- **As a Hyper-V virtual machine**—You can run DPM as a virtual machine hosted on an on-premises Hyper-V host server, to back up on-premises data. For a list of considerations in this environment see Install DPM as a virtual machine on an on-premises Hyper-V server.

- **As a Windows virtual machine in VMWare**—From DPM 2012 R2 with Update 5 onwards, you can deploy DPM to provide protection for Microsoft workloads running on Windows virtual machines in VMWare. In this scenario DPM can be deployed as a physical standalone server, as a Hyper-V virtual machine, or as a Windows virtual machine in VMWare.

- **As an Azure virtual machine**—From DPM 2012 R2 Update 3 onwards you can run DPM as a virtual machine in Azure to back up cloud workloads running as Azure virtual machines. For information about this deployment see Install DPM as an Azure virtual machine.

In all deployments you’ll need the following:

- Instance of SQL Server installed and running for the DPM database. The instance can be collocated on the DPM server or remote.
- Disk to be used as dedicated space for DPM data storage.
- DPM protection agent installed on computers and servers you want to protect using DPM.

## SQL Server database

DPM uses SQL Server as a database to store backup information for workloads, servers, and computers it protects.

|Requirement| Details  |
|-----------|----------|
|Version|SQL Server 2016 - Standard or Enterprise 64-bit (from DPM 2016 R2 with Update Rollup 2 onwards) <br/>SQL Server 2014 with all service packs and updates - Standard or Enterprise 64-bit <br/> SQL Server 2012 SP2 onwards - Standard or Enterprise 64-bit|
|RAM|4 GB minimum, 8 GB recommended|
|Disk|1 GB minimum, 3 GB recommended|
|Required features|Database Engine Services, Reporting Services|
|Collations|SQL_Latin1_General_CP1_CI_AS|
|Dynamic ports|Supported|
|AlwaysOn|Not supported|
|Installation|Install SQL Server on a remote server, or on the DPM server. It must be installed and running before you install DPM.|
|Remote installation|Install in the same domain and time zone as the DPM server.<br/> Installing SQL Server on a domain controller is not supported for DPM.<br/> Read about [Setting up a remote SQL Server instance](~/dpm/back-up-sql-server.md).<br/> If you're deploying DPM as an Azure virtual machine you can specify an Azure virtual machine running SQL Server as a remote SQL Server instance. You can't use an on-premises SQL Server. Using an Azure SQL Database isn't currently supported.|
|Clustered SQL Server|Supported|



## DPM server

|Requirement|Details|
|-----------|-------|
|Hardware|See [Hardware Requirements for System Center 2016](~/system-center.md)|
|Software|Windows Server 2016, Datacenter and Standard editions<br/>Windows Server 2012 R2, Datacenter and Standard editions|
|Installation prerequisites|Microsoft .NET Framework 4.0<br/> Windows Installer 4.5 or later versions<br/> Microsoft Visual C++ 2008 Redistributable<br/> Windows PowerShell 3.0<br/> Windows Single Instance Store (SIS)<br/> Microsoft Application Error Reporting<br/> Setup automatically installs these if they aren't already installed.|
|Limitations|You can install DPM on the operation system volume or on a different volume.<br/> DPM is designed to run on a dedicated, single-purpose server. Don't install DPM on:<br/> - a server running Application Server role<br/> - An Operations Manager Management server<br/> - A server running Exchange<br/> - A server running on a cluster node<br/> DPM isn't supported on the Turkish language version of any of the supported Windows Server versions.|


## Disks and storage

|Requirement|Minimum|Recommended|
|-----------|-------|-----------|
|Disk|DPM requires:<br/> - Disk for DPM installation including system files, installation files, prerequisite software, and database files<br/> - Disk dedicated to the storage pool| |
|DPM installation|DPM installation location: 3 GB<br/> Database files drive: 900 MB<br/> System drive: 1 GB<br/> The system drive disk space is required if SQL Server is installed on the DPM server. If SQL Server is remote, you'll need considerably less disk space for the system drive.|On each protected volume you'll need a minimum of 300 MB of free space for the change journal. In addition you'll need space because DPM copies the file catalog to a temporary DPM installation location for archiving. We recommend that the DPM installation volume has 2-3 GB of free space.|
|Disk for storage pool|1.5 times the size of the protected data|2-3 times the size of the protected data|
|Logical unit number (LUN)| |Maximum of 17 TB for GUID partition table (GPT) dynamic disks<br/> 2 TB for master boot record (MBR) disks<br/> Requirements are based on the maximum size of the hard disk that appears in the operating system.|
|Limitations|DPM storage pools must be dynamic.<br/> You can't install DPM on the dis used for the storage pool.<br/> You can attach or associate custom volumes with protected data sources. Custom volumes can be on basic or dynamic disks but you can't manage the space on these volumes in the DPM Administrator console.<br/> You can back up to tape with iSCSI attached tape libraries. We recommend a separate adapter for that connection. If you're running DPM 2012 R2 with Update Rollup 3 or later you can also use virtual tape libraries with a virtual fibre channel adapter. For more information see [Compatible tape libraries]().<br/>|
|Virtualized DPM|When DPM is running on a virtual machine it can use this storage:<br/> - .VHD disk that meets the configuration requirements listed in installing DPM in a virtual environment.<br/> - Passthrough disk with host direct attached storage (DAS)<br/> - Passthrough iSCSI LUN attached to a host. <br/> - Passthrough Fibre Channel LUN attached to a host.<br/> - iSCSI target LUN connected directly to the DPM virtual machine.<br/> - Fibre Channel LUN connected to the DPM virtual machine using a Windows Server 2012 Virtual Fiber Channel (VFC) controller.| |


## Protected workloads

|Requirement|Details|
|-----------|-------|
|Protected workload size limits|DPM can protect up to 600 volumes. 300 replica volumes and 300 recovery point volumes.<br/><br/> At the maximum size, protected sources are typically spread across approximately 75 servers and 150 client computers.<br/><br/> To protect this maximum size, DPM needs 120 TB per DPM server, with 80 TB replica space with a maximum recovery point size of 40 TB.|
|.NET framework|All protected computers need at least .NET Framework 4.0 installed before you install the DPM protection agent.|
|Windows Management Framework (WMF)|If you are protecting a server released prior to Windows Server 2012, you must install the appropriate version of WMF **before** installing the DPM agent:<br/> - [WMF 3.0](http://www.microsoft.com/download/details.aspx?id=34595) for Windows Server 2008 SP 2<br/> - [WMF 4.0](http://www.microsoft.com/download/details.aspx?id=40855) for Windows 7, Windows Embedded Standard 7, Windows Server 2008 R2<br/> Windows Server 2012 and later do not require a separate installation of WMF.
|Protected workloads|Review the DPM protection support matrix for an up-to-date list of protected workloads.|
|Prerequisites|DPM protection agent must be installed on protected computer. For more information, see Set up the protection agent.<br/><br/> Protected volumes must be at least 1 GB in size with NTFS formatting.<br/><br/> Server operating systems protected by DPM must be 64-bit.|


## Networking

|Requirement|Details|
|-----------|-------|
|Domain|The DPM server should be in a Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, or Windows Server 2003 Active Directory domain.|
|Domain trust|DPM supports data protection across forests as long as you establish a forest-level, two-way trust between the separate forests.<br/> <br/>DPM can protect servers and workstations across domains within a forest that has a two-way trust relationship with the DPM server domain. If there's no two-way trust DPM can't provide protection for computers in workgroups or untrusted domains. For more information see [Back up and restore workloads in workgroups and untrusted domains]().|
|Network configuration|If you're protecting data over a wide area network (WAN), you'll need a minimum bandwidth of 512 kilobits per second (Kbps).<br/> DPM doesn't support disjointed namespaces.|

## Remote management

|Requirement|Details|
|-----------|-------|
|Central Console|Use the Central Console to administer multiple DPM servers from a single location.<br/><br/> Install it on a server running System Center 2016 Operations Manager. You'll also need to install the Operations Management agent on the DPM server. See [Install Central Console]().|
|DPM Management Shell|Install the DPM Management Shell on a client computer to directly manage one or more DPM servers using Windows PowerShell. Install it from the DPM Setup.<br/><br/> The DPM Management Shell can be installed on computers running Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, Windows 7, Windows 8, Windows 8.1, and Windows 10. The computer must be running at least .NET Framework 4.0.|
|Remote Administration Console|Set up a Remote Administration Console to manage a single DPM server.<br/><br/> The DPM Administrator console can't be installed on a remote computer.<br/><br/> The DPM Management Shell can be installed on computers running Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, Windows 7, Windows 8, Windows 8.1, and Windows 10. The computer must be running at least .NET Framework 4.0.|
