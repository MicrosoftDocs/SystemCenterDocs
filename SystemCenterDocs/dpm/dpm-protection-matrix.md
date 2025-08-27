---
description: A complete matrix of all workloads, data types, and installations that DPM protects.
ms.topic: concept-article
ms.service: system-center
keywords:
ms.date: 03/03/2025
ms.update-cycle: 180-days
title: What can System Center Data Protection Manager back up?
ms.subservice: data-protection-manager
ms.assetid: 2ddbf72a-a82a-497e-afe1-672c8b253ed4
author: jyothisuri
ms.author: jsuri
ms.custom: engagement-fy23, UpdateFrequency.5, engagement-fy24
---

# What can DPM back up?

This article provides details of the workloads that DPM can back up.

::: moniker range="sc-dpm-2016"

Use the following matrix for DPM 2016:

- Workloads – The workload type of technology.

- Version – Supported VMM version for the workloads.

- DPM installation – The computer/location where you wish to install DPM.

- Protection and recovery – List the detailed information about the workloads, such as supported storage container or supported deployment.

::: moniker-end

::: moniker range="sc-dpm-2022"

Use the following matrix for DPM 2022:

::: moniker-end

::: moniker range="sc-dpm-2025"

Use the following matrix for DPM 2025:

::: moniker-end

::: moniker range="sc-dpm-2019"

Use the following matrix for DPM 2019:

::: moniker-end

::: moniker range=">=sc-dpm-2019"

- Workloads – The workload type of technology.

- Version – Supported DPM version for the workloads.

- DPM installation – The computer/location where you wish to install DPM.

- Protection and recovery – List the detailed information about the workloads such as supported storage container or supported deployment.  

::: moniker-end

::: moniker range=">=sc-dpm-2019"

## Protection support matrix

The following sections provide details of the protection support matrix for DPM:

- [Applications Backup](#applications-backup)
- [VM backup](#vm-backup)
- [Linux](#linux)

::: moniker-end

::: moniker range="sc-dpm-2019"

### Applications backup

|Workload|Version|DPM installation|Protection and recovery|
|------------|-----------|--------------------|--------------------------------------------|--------------------------------|---------------------------|
|Client computers (64-bit)|Windows 11, Windows 10|Physical server<br /><br />Hyper-V virtual machine<br /><br />VMware virtual machine|Volume, share, folder, files, and deduped volumes.<br /><br />Protected volumes must be NTFS. FAT and FAT32 aren't supported.<br /><br />Volumes must be at least 1 GB. DPM uses Volume Shadow Copy Service (VSS) to take the data snapshot and the snapshot only works if the volume is at least 1 GB.|
|Servers (64-bit)|Windows Server 2022, 2019, 2016, 2012 R2, 2012 |Azure virtual machine (when workload is running as Azure virtual machine)<br /><br />Physical server<br /><br />Hyper-V virtual machine<br /><br />VMware virtual machine|Volume, share, folder, file, and deduped volumes.<br /><br />[System state and bare metal](back-up-system-state-and-bare-metal.md) (not supported for Azure virtual machine).<br /><br />DPM 2019 UR1 and later supports the protection of ReFS volumes and ReFS deduped volumes.  |
|System Center VMM|VMM 2019, 2016|Physical server<br /><br />Hyper-V virtual machine<br /><br />VMware virtual machine|All deployment scenarios: Database.|
|SQL Server|SQL Server 2022, SQL Server 2019, SQL Server 2017, 2016 and [supported SPs](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202016), 2014 and supported [SPs](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202014) |Physical server <br /><br /> Hyper-V virtual machine <br /><br /> VMware virtual machine <br /> <br /> Azure virtual machine |All deployment scenarios: Database.<br /><br />DPM 2019 UR1 and later supports the backup of SQL over ReFS. <br /><br /> DPM 2019 UR2 and later supports the backup of SQL database, stored on the Cluster Shared Volumes (CSVs). <br/><br/> SQL Server 2022 is supported from 2019 UR5 and later.|
|Exchange|Exchange 2019, 2016|Physical server<br/><br/> Hyper-V virtual machine <br /><br />VMware virtual machine |Protect (all deployment scenarios): Standalone Exchange server, database under a database availability group (DAG).<br /><br />Recover (all deployment scenarios): Mailbox, mailbox databases under a DAG.<br/><br/> DPM 2019 doesn't support the backup of Exchange over ReFS.<br /><br /> DPM 2019 UR1 and later supports the backup of Exchange over ReFS.|
|SharePoint|SharePoint 2019, 2016 with latest SPs|Physical server<br /><br /> Hyper-V virtual machine <br /><br />VMware virtual machine <br /><br />Azure virtual machine (when workload is running as Azure virtual machine)|Protect (all deployment scenarios): Farm, frontend web server content.<br /><br />Recover (all deployment scenarios): Farm, database, web application, file or list item, SharePoint search, frontend web server.<br /><br />DPM 2019 UR1 and later supports the backup of SharePoint over ReFS.|

### VM backup

| Workload | Version | DPM installation | Protection and recovery |
| ------------ | ----------- | -------------------- | -------------------------------------------- |
|Hyper-V host - DPM protection agent on Hyper-V host server, cluster, or VM| Windows Server 2022, 2019, 2016, 2012 R2, 2012|Physical server<br /><br /> Hyper-V virtual machine <br /><br />VMware virtual machine |Protect: Hyper-V computers, [Hyper-V VMs](back-up-hyper-v-virtual-machines.md) hosted on Cluster Shared Volumes (CSVs).<br /><br />Recover: Virtual machines, item-level recovery of files and folders, volumes, and virtual hard drives.|
|VMware VMs | VMware server 5.5, 6.0, 6.5, 6.7 or 7.0|Physical server<br /><br /> Hyper-V virtual machine <br /><br />VMware virtual machine| Protect: VMware VMs on Cluster Shared Volumes (CSVs), NFS, and SAN storage. <br /><br />Recover: Virtual machines, item-level recovery of files and folders available only for Windows, volumes, and virtual hard drives.<br /><br />VMware vApps aren't supported.<br/><br/>vSphere 5.5 is not supported in 2019 UR5 and later.<br/><br/>vSphere 7.0 is supported from 2019 UR5 and later.|

### Linux

|Workload|Version|DPM installation|Protection and recovery|
|------------|-----------|--------------------|--------------------------------------------|--------------------------------|---------------------------|
|Linux|Linux running as Hyper-V guest (Hyper-V running on Windows Server 2016/2019/2012 R2/2012) <br /><br /> Linux virtual machines running on the versions 5.5, 6.0, 6.5 or 6.7 of VMware vCenter and vSphere Hypervisor (ESXi).|Physical server <br /><br />Hyper-V virtual machine <br /><br />VMware virtual machine|Hyper-V must be running on Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012. <br /><br />Protect: Entire virtual machine<br /><br />Recover: Entire virtual machine<br /><br />Only file-consistent snapshots are supported. <br/><br/> For a complete list of supported Linux distributions and versions, see the article, [Linux on distributions endorsed by Azure](/azure/virtual-machines/linux/endorsed-distros).|

::: moniker-end

::: moniker range="sc-dpm-2022"

### Applications backup

| Workload | Version | DPM installation | Protection and recovery |
|---|---|---|---|---|---|
| Client computers (64-bit) | Windows 10<br /><br />Windows 11 | Physical server<br /><br />Hyper-V virtual machine<br /><br />VMware virtual machine | Volume, share, folder, files, and deduped volumes<br /><br />Protected volumes must be NTFS. FAT and FAT32 aren't supported.<br /><br />Volumes must be at least 1 GB. DPM uses Volume Shadow Copy Service (VSS) to take the data snapshot and the snapshot only works if the volume is at least 1 GB. |
| Servers (64-bit) | Windows Server 2022, 2019, 2016 | Azure virtual machine (when workload is running as Azure virtual machine)<br /><br />Physical server<br /><br />Hyper-V virtual machine<br /><br />VMware virtual machine | Volume, share, folder, file, and deduped volumes.<br /><br />[System state and bare metal](back-up-system-state-and-bare-metal.md) (not supported for Azure virtual machine).<br /><br />DPM 2019 UR1 and later supports the protection of ReFS volumes and ReFS deduped volume. |
| System Center VMM | VMM 2022, 2019, 2016 | Physical server<br /><br />Hyper-V virtual machine<br /><br />VMware virtual machine | All deployment scenarios: Database |
| SQL Server | SQL Server 2022, SQL Server 2019, SQL Server 2017, 2016 and [supported SPs](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202016), 2014 and supported [SPs](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202014) | Physical server <br /><br /> Hyper-V virtual machine <br /><br /> VMware virtual machine <br /> <br /> Azure virtual machine | All deployment scenarios: database<br /><br />DPM 2019 UR1 and later supports the backup of SQL over ReFS. <br /><br /> DPM 2019 UR2 and later supports the backup of SQL database, stored on the Cluster Shared Volumes (CSVs). <br /><br />SQL Server 2022 is supported from 2022 UR1 and later.|
| Exchange | 2019, 2016 | Physical server<br/><br/> Hyper-V virtual machine <br /><br />VMware virtual machine | Protect (all deployment scenarios): Standalone Exchange server, database under a database availability group (DAG)<br /><br />Recover (all deployment scenarios): Mailbox, mailbox databases under a DAG<br/><br/> DPM 2019 doesn't support the backup of Exchange over ReFS<br /><br /> DPM 2019 UR1 and later supports the backup of Exchange over ReFS |
| SharePoint | 2019, 2016 with latest SPs | Physical server<br /><br /> Hyper-V virtual machine <br /><br />VMware virtual machine <br /><br />Azure virtual machine (when workload is running as Azure virtual machine) | Protect (all deployment scenarios):  Farm,  frontend web server content<br /><br />Recover (all deployment scenarios):  Farm, database, web application, file or list item, SharePoint search, frontend web server<br /><br />DPM 2019 UR1 and later supports the backup of SharePoint over ReFS |

### VM backup

|Workload|Version|DPM installation|Protection and recovery|
|------------|-----------|--------------------|--------------------------------------------|--------------------------------|---------------------------|
|Hyper-V host - DPM protection agent on Hyper-V host server, cluster, or VM| Windows Server 2022, 2019, 2016|Physical server<br /><br /> Hyper-V virtual machine <br /><br />VMware virtual machine |Protect: Hyper-V computers, [Hyper-V VMs](back-up-hyper-v-virtual-machines.md) hosted on Cluster Shared Volumes (CSVs)<br /><br />Recover: Virtual machines, item-level recovery of files and folders, volumes, and virtual hard drives.|
|VMware VMs | VMware server 6.0, 6.5, 6.7, 7.0, 8.0|Physical server<br /><br /> Hyper-V virtual machine <br /><br />VMware virtual machine| Protect: VMware VMs on Cluster Shared Volumes (CSVs), NFS, and SAN storage. <br /><br />Recover: Virtual machines, item-level recovery of files and folders available only for Windows, volumes, and virtual hard drives.<br /><br />VMware vApps aren't supported.<br /><br />vSphere 6.0 isn't supported in 2022 UR1 and later. <br/><br/>vSphere 8.0 is supported from 2022 UR2.|

### Linux

|Workload|Version|DPM installation|Protection and recovery|
|------------|-----------|--------------------|--------------------------------------------|--------------------------------|---------------------------|
|Linux|Linux running as Hyper-V guest (Hyper-V running on Windows Server 2016/2019/2022) <br /><br /> Linux virtual machines running on versions 6.0, 6.5, 6.7, or 7.0 of VMware vCenter and vSphere Hypervisor (ESXi).|Physical server <br /><br />Hyper-V virtual machine <br /><br />VMware virtual machine|Hyper-V must be running on Windows Server 2022, Windows Server 2019, and Windows Server 2016. <br /><br />Protect: Entire virtual machine.<br /><br />Recover: Entire virtual machine.<br /><br />Only file-consistent snapshots are supported. <br/><br/> For a complete list of supported Linux distributions and versions, see the article [Linux on distributions endorsed by Azure](/azure/virtual-machines/linux/endorsed-distros).|

::: moniker-end

::: moniker range="sc-dpm-2025"

### Applications backup

| Workload | Version | DPM installation | Protection and recovery |
|---|---|---|---|---|---|
| Client computers (64-bit) | Windows 10<br /><br />Windows 11 | Physical server<br /><br />Hyper-V virtual machine<br /><br />VMware virtual machine | Volume, share, folder, files, and deduped volumes<br /><br />Protected volumes must be NTFS. FAT and FAT32 aren't supported.<br /><br />Volumes must be at least 1 GB. DPM uses Volume Shadow Copy Service (VSS) to take the data snapshot and the snapshot only works if the volume is at least 1 GB. |
| Servers (64-bit) | Windows Server 2025, 2022, 2019 | Azure virtual machine (when workload is running as Azure virtual machine)<br /><br />Physical server<br /><br />Hyper-V virtual machine<br /><br />VMware virtual machine | Volume, share, folder, file, and deduped volumes.<br /><br />[System state and bare metal](back-up-system-state-and-bare-metal.md) (not supported for Azure virtual machine).<br /><br />DPM 2019 UR1 and later supports the protection of ReFS volumes and ReFS deduped volume. |
| System Center VMM | VMM 2025, 2022, 2019 | Physical server<br /><br />Hyper-V virtual machine<br /><br />VMware virtual machine | All deployment scenarios: Database |
| SQL Server | SQL Server 2022, SQL Server 2019, SQL Server 2017, 2016 and [supported SPs](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202016), 2014 and supported [SPs](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202014) | Physical server <br /><br /> Hyper-V virtual machine <br /><br /> VMware virtual machine <br /> <br /> Azure virtual machine | All deployment scenarios: database<br /><br />DPM 2019 UR1 and later supports the backup of SQL over ReFS. <br /><br /> DPM 2019 UR2 and later supports the backup of SQL database, stored on the Cluster Shared Volumes (CSVs). <br /><br />SQL Server 2022<br /><br />Note: Install latest version of OLEDB 19 (19.3 and above)|
| Exchange | 2019, 2016 and Exchange Subscription Edition| Physical server<br/><br/> Hyper-V virtual machine <br /><br />VMware virtual machine | Protect (all deployment scenarios): Standalone Exchange server, database under a database availability group (DAG)<br /><br />Recover (all deployment scenarios): Mailbox, mailbox databases under a DAG<br/><br/> DPM 2019 doesn't support the backup of Exchange over ReFS<br /><br /> DPM 2019 UR1 and later supports the backup of Exchange over ReFS |
| SharePoint | 2019, 2016 with latest SPs and Sharepoint Subscription Edition | Physical server<br /><br /> Hyper-V virtual machine <br /><br />VMware virtual machine <br /><br />Azure virtual machine (when workload is running as Azure virtual machine) | Protect (all deployment scenarios):  Farm,  frontend web server content<br /><br />Recover (all deployment scenarios):  Farm, database, web application, file or list item, SharePoint search, frontend web server<br /><br />DPM 2019 UR1 and later supports the backup of SharePoint over ReFS<br /><br />Note: Install latest version of OLEDB 19 (19.3 and above)|

### VM backup

|Workload|Version|DPM installation|Protection and recovery|
|------------|-----------|--------------------|--------------------------------------------|--------------------------------|---------------------------|
|Hyper-V host - DPM protection agent on Hyper-V host server, cluster, or VM| Windows Server 2025, 2022, 2019|Physical server<br /><br /> Hyper-V virtual machine <br /><br />VMware virtual machine |Protect: Hyper-V computers, [Hyper-V VMs](back-up-hyper-v-virtual-machines.md) hosted on Cluster Shared Volumes (CSVs)<br /><br />Recover: Virtual machines, item-level recovery of files and folders, volumes, and virtual hard drives.|
|VMware VMs | VMware server 6.5, 6.7, 7.0, 8.0|Physical server<br /><br /> Hyper-V virtual machine <br /><br />VMware virtual machine| Protect: VMware VMs on Cluster Shared Volumes (CSVs), NFS, and SAN storage. <br /><br />Recover: Virtual machines, item-level recovery of files and folders available only for Windows, volumes, and virtual hard drives.<br /><br />VMware vApps aren't supported.|

### Linux

|Workload|Version|DPM installation|Protection and recovery|
|------------|-----------|--------------------|--------------------------------------------|--------------------------------|---------------------------|
|Linux|Linux running as Hyper-V guest (Hyper-V running on Windows Server 2016/2019/2022/2025) <br /><br /> Linux virtual machines running on versions 6.5, 6.7, or 7.0 of VMware vCenter and vSphere Hypervisor (ESXi).|Hyper-V virtual machine <br /><br />VMware virtual machine|Hyper-V must be running on Windows Server 2025, Windows Server 2022, Windows Server 2019, and Windows Server 2016. <br /><br />Protect: Entire virtual machine.<br /><br />Recover: Entire virtual machine.<br /><br />Only file-consistent snapshots are supported. <br/><br/> For a complete list of supported Linux distributions and versions, see the article [Linux on distributions endorsed by Azure](/azure/virtual-machines/linux/endorsed-distros).|

::: moniker-end

::: moniker range="<sc-dpm-2019"

## Protection support matrix

|Workload|Version|DPM installation|DPM - System Center SAC|DPM - System Center 2016|Protection and recovery|
|------------|-----------|--------------------|--------------------------------------------|--------------------------------|---------------------------|
|System Center VMM|VMM 2016,<br/>VMM 2012, SP1, R2|Physical server<br /><br />Hyper-V virtual machine|Y|Y|All deployment scenarios: Database|
|Client computers (64-bit and 32-bit)|Windows 10|Physical server<br /><br />Hyper-V virtual machine<br /><br />VMware virtual machine|Y|Y|Volume, share, folder, files, and deduped volumes.<br /><br />Protected volumes must be NTFS. FAT and FAT32 aren't supported.<br /><br />Volumes must be at least 1 GB. DPM uses Volume Shadow Copy Service (VSS) to take the data snapshot and the snapshot only works if the volume is at least 1 GB.|
|Client computers (64-bit and 32-bit)|Windows 8.1|Physical server<br /><br />Hyper-V virtual machine|Y|Y|Volume, share, folder, files, and deduped volumes.<br /><br />Protected volumes must be NTFS. FAT and FAT32 aren't supported.<br /><br />Volumes must be at least 1 GB. DPM uses Volume Shadow Copy Service (VSS) to take the data snapshot and the snapshot only works if the volume is at least 1 GB.|
|Client computers (64-bit and 32-bit)|Windows 8.1|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y<br /><br />From Update Rollup 5 onwards|Volume, share, folder, files, and deduped volumes.<br /><br />Protected volumes must be NTFS. FAT and FAT32 aren't supported.<br /><br />Volumes must be at least 1 GB. DPM uses Volume Shadow Copy Service (VSS) to take the data snapshot and the snapshot only works if the volume is at least 1 GB.|
|Client computers (64-bit and 32-bit)|Windows 8|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Volume, share, folder, files, and deduped volumes.<br /><br />Protected volumes must be NTFS and at least 1 GB.|
|Client computers (64-bit and 32-bit)|Windows 8|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y |Volume, share, folder, files, and deduped volumes.<br /><br />Protected volumes must be NTFS. FAT and FAT32 aren't supported.<br /><br />Volumes must be at least 1 GB. DPM uses Volume Shadow Copy Service (VSS) to take the data snapshot and the snapshot only works if the volume is at least 1 GB.|
|Client computers (64-bit and 32-bit)|Windows 7|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Volume, share, folder, files, and deduped volumes.<br /><br />Protected volumes must be NTFS and at least 1 GB.|
|Client computers (64-bit and 32-bit)|Windows 7|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y|Volume, share, folder, files, and deduped volumes.<br /><br />Protected volumes must be NTFS. FAT and FAT32 aren't supported.<br /><br />Volumes must be at least 1 GB. DPM uses Volume Shadow Copy Service (VSS) to take the data snapshot and the snapshot only works if the volume is at least 1 GB.|
|Servers (32-bit and 64-bit)|Windows Server 2016|Azure virtual machine (when workload is running as Azure virtual machine)<br /><br />Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)<br /><br />Physical server<br /><br />On-premises Hyper-V virtual machine|Y<br /><br />Not Nano server|Y <br/> Not Nano server|Volume, share, folder, file, system state/bare metal, and deduped volumes.|
|Servers (32-bit and 64-bit)|Windows Server 2012 R2 - Datacenter and Standard|Azure virtual machine (when workload is running as Azure virtual machine)|Y|Y|Volume, share, folder, file<br /><br />DPM must be running on at least Windows Server 2012 R2 to protect Windows Server 2012 deduped volumes.|
|Servers (32-bit and 64-bit)|Windows Server 2012 R2 - Datacenter and Standard|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y|Volume, share, folder, file, system state/bare metal)<br /><br />DPM must be running on Windows Server 2012 or 2012 R2 to protect Windows Server 2012 deduped volumes.|
|Servers (32-bit and 64-bit)|Windows Server 2012/2012 with SP1 - Datacenter and Standard|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Volume, share, folder, file, system state/bare metal<br /><br />DPM must be running on at least Windows Server 2012 R2 to protect Windows Server 2012 deduped volumes.|
|Servers (32-bit and 64-bit)|Windows Server 2012/2012 with SP1 - Datacenter and Standard|Azure virtual machine (when workload is running as Azure virtual machine)|Y|Y|Volume, share, folder, file<br /><br />DPM must be running on at least Windows Server 2012 R2 to protect Windows Server 2012 deduped volumes.|
|Servers (32-bit and 64-bit)|Windows Server 2012/2012 with SP1 - Datacenter and Standard|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y|Volume, share, folder, file, system state/bare metal<br /><br />DPM must be running on at least Windows Server 2012 R2 to protect Windows Server 2012 deduped volumes.|
|Servers (32-bit and 64-bit)|Windows Server 2008 R2 SP1 - Standard and Enterprise|Physical server<br /><br />On-premises Hyper-V virtual machine|Y<br /><br />You need to be running SP1 and install [Windows Management Frame 5.1](https://www.microsoft.com/download/details.aspx?id=54616)|Y<br /><br />You need to install [Windows Management Frame 5.1](https://www.microsoft.com/download/details.aspx?id=54616)|Volume, share, folder, file, system state/bare metal|
|Servers (32-bit and 64-bit)|Windows Server 2008 R2 SP1 - Standard and Enterprise|Azure virtual machine (when workload is running as Azure virtual machine)|Y<br /><br />You need to install [Windows Management Frame 5.1](https://www.microsoft.com/download/details.aspx?id=54616)|Y<br /><br />You need to be running SP1 and install [Windows Management Frame 5.1](https://www.microsoft.com/download/details.aspx?id=54616)|Volume, share, folder, file|
|Servers (32-bit and 64-bit)|Windows Server 2008 R2 SP1 - Standard and Enterprise|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y<br /><br />You need to install [Windows Management Frame 5.1](https://www.microsoft.com/download/details.aspx?id=54616)|Y<br /><br />You need to be running SP1 and install [Windows Management Frame 5.1](https://www.microsoft.com/download/details.aspx?id=54616)|Volume, share, folder, file, system state/bare metal|
|Servers (32-bit and 64-bit)|Windows Server 2008 R2|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Volume, share, folder, file, system state/bare metal|
|Servers (32-bit and 64-bit)|Windows Server 2008 R2|Azure virtual machine (when workload is running as Azure virtual machine)|N|N|Volume, share, folder, file|
|Servers (32-bit and 64-bit)|Windows Server 2008 R2|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|N|N|Volume, share, folder, file, system state/bare metal|
|Servers (32-bit and 64-bit)|Windows Server 2008 SP2|Physical server<br /><br />On-premises Hyper-V virtual machine|N|N|Volume, share, folder, file, system state/bare metal|
|Servers (32-bit and 64-bit)|Windows Server 2008 SP2|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y|Volume, share, folder, file, system state/bare metal|
|Servers (32-bit and 64-bit)|Windows Storage Server 2008 SP2|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Volume, share, folder, file, system state/bare metal|
|SQL Server|SQL Server 2017|Physical server <br /><br /> On-premises Hyper-V virtual machine <br /> <br /> Azure virtual machine <br /><br /> Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y (UR5 Onwards)|All deployment scenarios: database|
|SQL Server|SQL Server 2016 SP1|Physical server <br /><br /> On-premises Hyper-V virtual machine <br /> <br /> Azure virtual machine <br /><br /> Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y (UR4 onwards)|All deployment scenarios: database|
|SQL Server|SQL Server 2016|Physical server <br /><br /> On-premises Hyper-V virtual machine <br /> <br /> Azure virtual machine <br /><br /> Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y (UR2 Onwards)|All deployment scenarios: database|
|SQL Server|SQL Server 2014|Azure virtual machine (when workload is running as Azure virtual machine)|Y|Y|All deployment scenarios: database|
|SQL Server|SQL Server 2014|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y|All deployment scenarios: database|
|SQL Server|SQL Server 2012 with SP2|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|All deployment scenarios: database|
|SQL Server|SQL Server 2012 with SP2|Azure virtual machine (when workload is running as Azure virtual machine)|Y|Y|All deployment scenarios: database|
|SQL Server|SQL Server 2012 with SP2|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y |All deployment scenarios: database|
|SQL Server|SQL Server 2012, SQL Server 2012 with SP1|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|All deployment scenarios: database|
|SQL Server|SQL Server 2012, SQL Server 2012 with SP1|Azure virtual machine (when workload is running as Azure virtual machine)|Y|Y |All deployment scenarios: database|
|SQL Server|SQL Server 2012, SQL Server 2012 with SP1|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y|All deployment scenarios: database|
|SQL Server|SQL Server 2008 R2|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|All deployment scenarios: database|
|SQL Server|SQL Server 2008 R2|Azure virtual machine (when workload is running as Azure virtual machine)|Y|Y|All deployment scenarios: database|
|SQL Server|SQL Server 2008 R2|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y|All deployment scenarios: database|
|SQL Server|SQL Server 2008|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|All deployment scenarios: database|
|SQL Server|SQL Server 2008|Azure virtual machine (when workload is running as Azure virtual machine)|Y|Y|All deployment scenarios: database|
|SQL Server|SQL Server 2008|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y|All deployment scenarios: database|
|Exchange|Exchange 2016|Physical server<br/><br/> On-premises Hyper-V virtual machine|Y|Y|Protect (all deployment scenarios): Standalone Exchange server, database under a database availability group (DAG)<br /><br />Recover (all deployment scenarios): Mailbox, mailbox databases under a DAG<br/><br/> Backup of Exchange over ReFS not supported |
|Exchange|Exchange 2016|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y|Protect (all deployment scenarios): Standalone Exchange server, database under a database availability group (DAG)<br /><br />Recover (all deployment scenarios): Mailbox, mailbox databases under a DAG<br/><br/> Backup of Exchange over ReFS not supported |
|Exchange|Exchange 2013|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect (all deployment scenarios): Standalone Exchange server, database under a database availability group (DAG)<br /><br />Recover (all deployment scenarios): Mailbox, mailbox databases under a DAG<br/><br/> Backup of Exchange over ReFS not supported |
|Exchange|Exchange 2013|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y|Protect (all deployment scenarios): Standalone Exchange server, database under a database availability group (DAG)<br /><br />Recover (all deployment scenarios): Mailbox, mailbox databases under a DAG<br/><br/> Backup of Exchange over ReFS not supported |
|Exchange|Exchange 2010|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect (all deployment scenarios): Standalone Exchange server, database under a database availability group (DAG)<br /><br />Recover  (all deployment scenarios):  Mailbox, mailbox databases under a DAG<br/><br/> Backup of Exchange over ReFS not supported |
|Exchange|Exchange 2010|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y|Protect (all deployment scenarios): Standalone Exchange server, database under a database availability group (DAG)<br /><br />Recover (all deployment scenarios):  Mailbox, mailbox databases under a DAG<br/><br/> Backup of Exchange over ReFS not supported |
|SharePoint|SharePoint 2016|Physical server<br /><br />On-premises Hyper-V virtual machine<br /><br />Azure virtual machine (when workload is running as Azure virtual machine)<br /><br />Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y (UR2 Onwards)|Protect (all deployment scenarios):  Farm,  frontend web server content<br /><br />Recover (all deployment scenarios):  Farm, database, web application, file or list item, SharePoint search, frontend web server<br /><br />|
|SharePoint|SharePoint 2013|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect (all deployment scenarios):  Farm,  frontend web server content<br /><br />Recover (all deployment scenarios):  Farm, database, web application, file or list item, SharePoint search, frontend web server<br /><br />|
|SharePoint|SharePoint 2013|Azure virtual machine (when workload is running as Azure virtual machine) - DPM 2012 R2 Update Rollup 3 onwards|Y|Y|Protect (all deployment scenarios):  Farm, SharePoint search, frontend web server content<br /><br />Recover (all deployment scenarios):  Farm, database, web application, file or list item, SharePoint search, frontend web server<br /><br />|
|SharePoint|SharePoint 2013|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y|Protect (all deployment scenarios):  Farm, SharePoint search, frontend web server content<br /><br />Recover (all deployment scenarios):  Farm, database, web application, file or list item, SharePoint search, frontend web server<br /><br />|
|SharePoint|SharePoint 2010|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect (all deployment scenarios): Farm, SharePoint search, frontend web server content<br /><br />Recover (all deployment scenarios): Farm, database, web application, file or list item, SharePoint search, frontend web server|
|SharePoint|SharePoint 2010|Azure virtual machine (when workload is running as Azure virtual machine)|Y|Y|Protect (all deployment scenarios): Farm, SharePoint search, frontend web server content<br /><br />Recover (all deployment scenarios): Farm, database, web application, file or list item, SharePoint search, frontend web server|
|SharePoint|SharePoint 2010|Windows virtual machine in VMware (protects workloads running in Windows virtual machine in VMware)|Y|Y|Protect (all deployment scenarios): Farm, SharePoint search, frontend web server content<br /><br />Recover (all deployment scenarios): Farm, database, web application, file or list item, SharePoint search, frontend web server|
|Hyper-V host - DPM protection agent on Hyper-V host server, cluster, or VM|Windows Server 2016|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect: Hyper-V computers, Hyper-V VMs hosted on Cluster Shared Volumes (CSVs)<br /><br />Recover: Virtual machines, item-level recovery of files and folders, volumes, and virtual hard drives.|
|Hyper-V host - DPM protection agent on Hyper-V host server, cluster, or VM|Windows Server 2012 R2 - Datacenter and Standard|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect: Hyper-V computers, Hyper-V VMs hosted on Cluster Shared Volumes (CSVs)<br /><br />Recover: Virtual machines, item-level recovery of files and folders, volumes, and virtual hard drives.|
|Hyper-V host - DPM protection agent on Hyper-V host server, cluster, or VM|Windows Server 2012 - Datacenter and Standard|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect: Hyper-V computers, Hyper-V VMs hosted on Cluster Shared Volumes (CSVs)<br /><br />Recover: Virtual machine, Item-level recovery of files and folder, volumes, virtual hard drives|
|Hyper-V host - DPM protection agent on Hyper-V host server, cluster, or VM|Windows Server 2008 R2 SP1 - Enterprise and Standard|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect: Hyper-V computers, Hyper-V VMs hosted on Cluster Shared Volumes (CSVs)<br /><br />Recover: Virtual machines, item-level recovery of files and folders, volumes, and virtual hard drives.|
|Hyper-V host - DPM protection agent on Hyper-V host server, cluster, or VM|Windows Server 2008 SP2|Physical server<br /><br />On-premises Hyper-V virtual machine|N|N|Protect: Hyper-V computers, Hyper-V VMs hosted on Cluster Shared Volumes (CSVs)<br /><br />Recover: Virtual machines, item-level recovery of files and folders, volumes, and virtual hard drives.|
|Linux|Linux running as Hyper-V guest|On-premises Hyper-V virtual machine|Y|Y|Hyper-V must be running on Windows Server 2012 R2 or Windows Server 2016. Protect: Entire virtual machine<br /><br />Recover: Entire virtual machine <br/><br/> For a complete list of supported Linux distributions and versions, see the article, [Linux on distributions endorsed by Azure](/azure/virtual-machines/linux/endorsed-distros).|
|VMware VMs | VMware server 5.5, 6.0, or 6.5 | On-premises Hyper-V virtual machine | Y | N | VMware VMs on Cluster Shared Volumes (CSVs), NFS, and SAN storage. <br/>Item-level recovery of files and folders available only for Windows. VMware vApps not supported. |
|VMware VMs | [VMware vSphere 6.7](back-up-VMware.md)| On-premises Hyper-V virtual machine | Y (Applicable for DPM 2019 and later) | N | VMware VMs on Cluster Shared Volumes (CSVs), NFS, and SAN storage. <br/>Item-level recovery of files and folders available only for Windows. VMware vApps not supported. |

::: moniker-end

## Cluster support

DPM can protect data in the following clustered applications:

- File servers

- SQL Server

- Hyper-V

    > [!NOTE]
    > If you're protecting a Hyper-V cluster using scaled-out DPM protection, you can't add secondary protection for the protected Hyper-V workloads.

- Exchange Server - DPM can protect non-shared disk clusters for supported Exchange Server versions (cluster continuous replication) and can also protect Exchange Server configured for local continuous replication.

- SQL Server

    ::: moniker range="sc-dpm-2016"

    > [!NOTE]
    > DPM doesn't support the protection of SQL Server databases hosted on Cluster Shared Volumes (CSVs).

    ::: moniker-end

    ::: moniker range=">=sc-dpm-2019"

    > [!NOTE]
    > DPM 2019 UR2 and later supports the protection of SQL Server databases, hosted on Cluster Shared Volumes (CSVs).

    ::: moniker-end

DPM can protect cluster workloads that are in the same domain as the DPM server, and in a child or trusted domain. If you want to protect data source in untrusted domains or workgroups, you'll need to use NTLM or certificate authentication for a single server or certificate authentication only for a cluster.

## Next steps

[Get ready to deploy DPM servers](plan-dpm-deployment.md)
