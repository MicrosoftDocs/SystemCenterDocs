---
description: This article is a primer for the necessary components to deploy DPM 2016 in your environment.
ms.topic: include
author: jyothisuri
ms.author: jsuri
ms.service: system-center
keywords:
ms.date: 10/08/2024
title: Preparing your environment for System Center Data Protection Manager
ms.subservice: data-protection-manager
ms.assetid:
---

## DPM deployment considerations

One of your first decisions is how to deploy DPM. You can deploy DPM:

- **As a physical standalone server** - You can deploy DPM as a physical standalone server to back up on-premises data. Physical DPM servers can’t be deployed in a cluster, but you can manage multiple physical servers from a single console by installing Central Console on System Center Operations Manager.

- **As a Hyper-V virtual machine** - You can run DPM as a virtual machine (hosted on an on-premises Hyper-V host server), to back up on-premises data. For a list of considerations in this environment, see Install DPM as a virtual machine on an on-premises Hyper-V server.

- **As a Windows virtual machine in VMware** - You can deploy DPM to protect Microsoft workloads running on Windows virtual machines in VMware. In this scenario, DPM can be deployed as a physical standalone server, as a Hyper-V virtual machine, or as a Windows virtual machine in VMware.

- **As an Azure virtual machine** - DPM can run as a virtual machine in Azure to back up cloud workloads running as Azure virtual machines. For information about this deployment, see Install DPM as an Azure virtual machine.

In all deployments you’ll need:

- A SQL Server Instance, installed and running, to use for the DPM database. The instance can be co-located on the DPM server or remote.
- Disk to be used as dedicated space for DPM data storage.
- DPM protection agent installed on computers and servers you want to protect using DPM.

## SQL Server database

DPM uses SQL Server as a database to store backup information for workloads, servers, and computers it protects. All SQL Server versions should be Standard or Enterprise 64-bit.

>[!NOTE]
> - For the supported versions of SQL, use the service packs that are currently in support by Microsoft.  
> - For the below supported SQL versions, Standard, Enterprise, and Datacenter (64-bit) editions are supported, based on availability.

**SQL Server - supported versions**

**DPM version** | **SQL version**
--- | ---
DPM 2016 | SQL Server 2014 SP2 or later <br/><br/>  SQL Server 2012 SP4 or later.
DPM 2016 UR2 and later| SQL Server 2014 SP2 or later <br/><br/> SQL Server 2012 SP4 or later <br/><br/> SQL Server 2016 and SPs as detailed [here](/lifecycle/products/?terms=SQL+Server+2016)

**SQL Server requirements**

|Requirement| Details  |
|-----------|----------|
|RAM|4 GB minimum, 8 GB recommended|
|Disk|1 GB minimum, 3 GB recommended|
|Required features|Database Engine Services, Reporting Services (for DPM 2019, install SSRS with SQL 2017 or later)<br/><br/>**Note** <br/><br/> - For Remote SQL, the database engine and reporting services must be on the same computer. <br/><br/> - For remote clustered SQL Instance, Database Engine must be on the cluster and SSRS must be on a separate computer, which can be the DPM server or any other computer)|
|Collations|SQL_Latin1_General_CP1_CI_AS|
|Dynamic ports|Supported|
|AlwaysOn|Not supported|
|Installation|Install SQL Server on a remote server, or the DPM server. It must be installed and running before you install DPM.|
|Remote installation|Install in the same domain and time zone as the DPM server.<br/> When used to support DPM, a SQL Server can't share a server with a domain controller.<br/> Read about [Setting up a remote SQL Server Instance](/system-center/dpm/install-dpm#BKMK_SQL).<br/> If you're deploying DPM as an Azure virtual machine, you can specify an Azure virtual machine running SQL Server as a remote SQL Server Instance. You can't use an on-premises SQL Server. Using an Azure SQL Database isn't currently supported.|
|Clustered SQL Server|Supported|

> [!NOTE]
> If you are upgrading SQL Database to SQL 2017, ensure you install SQL SSRS post SQL upgrade.

## DPM server

|Requirement|Details|
|-----------|-------|
|Operating System|Windows Server 2016, Datacenter, and Standard editions<br/>Windows Server 2012 R2, Datacenter, and Standard editions |
|Installation prerequisites|Microsoft .NET Framework 4.0<br/> Windows Installer 4.5 or later versions<br/> Windows PowerShell 3.0<br/> Windows Single Instance Store (SIS)<br/> Microsoft Application Error Reporting<br/> SQL management tools <br/><br/> Setup automatically installs the prerequisites if they aren't already installed.|

## Disks and storage

|Requirement|Minimum|Recommended|
|-----------|-------|-----------|
|Disk|DPM requires:<br/> - Disk for DPM installation, including system files, installation files, prerequisite software, and database files<br/> - Disk dedicated to the storages pool| |
|DPM installation|DPM installation location: 3 GB<br/> Database files drive: 900 MB<br/> System drive: 1 GB<br/> The system drive disk space is required if SQL Server is installed on the DPM server. If SQL Server is remote, you'll need considerably less disk space for the system drive.|Each protected volume requires a minimum of 300 MB of free space for the change journal. Additionally, you'll need space for DPM to copy the file catalog to a temporary DPM installation location when archiving. Free space of 2-3 GB is recommended for the DPM installation volume.|
|Disk for storage pool|1.5 times the size of the protected data|2-3 times the size of the protected data|
|Logical unit number (LUN)<br/><br/> *Applies only to DPM 2016/2019 servers upgraded from DPM 2012 R2, which uses a legacy storage pool.* | |Maximum of 17 TB for GUID partition table (GPT) dynamic disks<br/> 2 TB for master boot record (MBR) disks<br/> Requirements are based on the maximum size of the hard disk that appears in the operating system.|
|Limitations<br/><br/> *Applies only to DPM 2016/DPM 2019 servers upgraded from DPM 2012 R2 that used a legacy storage pool.* |- DPM storage pools must be dynamic.<br/> - You can't install DPM on the disk used for the storage pool.<br/> - You can attach or associate custom volumes with protected data sources. Custom volumes can be on basic or dynamic disks but you can't manage the space on these volumes in the DPM Administrator console.<br/> - You can back up to tape with iSCSI attached tape libraries. We recommend a separate adapter for that connection. For more information, see [Compatible tape libraries](/system-center/dpm/identify-compatible-tape-libraries).<br/>| |
|Virtualized DPM|- DPM running on a virtual machine can use the following storage types:<br/> - .VHD disk that meets the configuration requirements listed in installing DPM in a virtual environment.<br/> - Passthrough disk with host direct attached storage (DAS)<br/> - Passthrough iSCSI LUN attached to a host. <br/> - Passthrough Fibre Channel LUN attached to a host.<br/> - iSCSI target LUN connected directly to the DPM virtual machine.<br/> - Fibre Channel LUN connected to the DPM virtual machine using a Windows Server 2012 Virtual Fiber Channel (VFC) controller.| <br/> |
|Modern Backup Storage| Uses basic volumes and cannot be on a dynamic disk. <br/> A single DPM server has a soft limit of 120 TB storage.| <br/> |

## Storage recommendations for DPM

- Sector Size should always be consistent across underlying storage (that is WS storage) to DPM native storage.
- When storage spaces are used to carve out DPM storage, storage spaces are supported on iSCSI and FC controllers as  long as the virtual disks created on top of them are non-resilient (Simple with any number of columns)
- Write-back cache should always be set to zero while using Storage Spaces for DPM storage.

## Protected workloads

|Requirement|Details|
|-----------|-------|
|Protected workload size limits|DPM 2016 and later with Modern Backup Storage do not have LDM limits. <br/><br/> With DPM 2016 and later, you can protect more data per DPM server. Up to 120 TB of storage limit per DPM server has been tested. However, 120 TB is only a soft limit. Validation is underway to test a higher limit. This guidance will be updated post-completion of the validation.|
|.NET framework|All protected computers need at least .NET Framework 4.0 installed before you install the DPM protection agent.|
|Windows Management Framework (WMF) <br/><br/> (Not applicable to DPM 2019)| If you are protecting a server released prior to Windows Server 2012, you must install the appropriate version of WMF **before** installing the DPM agent:<br/><br/> - [WMF 3.0](https://www.microsoft.com/download/details.aspx?id=34595) for Windows Server 2008 SP 2<br/> - [Windows Management Frame 5.1](https://www.microsoft.com/download/details.aspx?id=54616) for Windows 7, Windows Embedded Standard 7, Windows Server 2008 R2<br/><br/> Windows Server 2012 and later do not require a separate installation of WMF.
|Protected workloads|Review the DPM protection support matrix for an up-to-date list of protected workloads.|
|Prerequisites|DPM protection agent must be installed on protected computer. For more information, see Set up the protection agent.<br/><br/> Protected volumes must be at least 1 GB in size with NTFS formatting.<br/><br/> Server operating systems protected by DPM must be 64-bit.|


## Networking

|Requirement|Details|
|-----------|-------|
|Domain|The DPM server should be in a Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, or Windows Server 2012|
|Domain trust|DPM supports data protection across forests as long as you establish a forest-level, two-way trust between the separate forests.<br/> <br/>DPM can protect servers and workstations across domains within a forest that has a two-way trust relationship with the DPM server domain. Without two-way trust, DPM can't protect computers in workgroups or untrusted domains. For more information, see [Back up and restore workloads in workgroups and untrusted domains](/system-center/dpm/back-up-machines-in-workgroups-and-untrusted-domains).|
|Network configuration|If you're protecting data over a wide area network (WAN), you'll need a minimum bandwidth of 512 kilobits per second (Kbps).<br/> DPM doesn't support disjointed namespaces.|

## Remote management

|Requirement|Details|
|-----------|-------|
|Central Console|Use the Central Console to administer multiple DPM servers from a single location.<br/><br/> Install it on a server running System Center 2016/2019 Operations Manager. You'll also need to install the Operations Management agent on the DPM server. See [Install Central Console](/system-center/dpm/use-central-console-to-manage-multiple-dpm-servers#set-up-central-console).|
|DPM Management Shell|Install the DPM Management Shell on a client computer to directly manage one or more DPM servers using Windows PowerShell. Install it from the DPM Setup.<br/><br/> The DPM Management Shell can be installed on computers running:<br/><br/> DPM 2019: Windows Server 2019, Windows Server 2016, Windows 8.1, and Windows 10 <br/><br/>DPM 2016: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, Windows 7, Windows 8, Windows 8.1<br/><br/>**Note**: DPM 2019 supports x64-bit computers only.|
|Remote Administration Console|Set up a Remote Administration Console to manage a single DPM server.<br/><br/> The DPM Management Shell can be installed on computers running Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, Windows 7, Windows 8, Windows 8.1, and Windows 10. The computer must be running at least .NET Framework 4.0.<br/><br/>**Note**: DPM 2019 supports X64-bit computers only.|