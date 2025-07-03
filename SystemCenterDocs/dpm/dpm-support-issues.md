---
description: This article explains the supported deployment options for Data Protection Manager.
ms.topic: concept-article
author: jyothisuri
ms.author: jsuri
ms.service: system-center
keywords:
ms.date: 11/01/2024
title: What's supported and what isn't for DPM
ms.subservice: data-protection-manager
ms.assetid: 29d977b5-56de-4bc4-ba0b-2d45d02516a4
ms.custom: engagement-fy23, UpdateFrequency.5, engagement-fy24
---

# What's supported and what isn't for DPM?

This article summarizes some of the common support information you might need when deploying and maintaining a System Center - Data Protection Manager.

## <a name="BKMK_Install"></a>Installation and deployment issues

### DPM deployment options

**Issue**: DPM can be installed in physical and virtual environments.

**More information**: DPM can be installed as follows:

- As a standalone physical server - DPM can't be deployed in a physical cluster, but you can manage multiple DPM servers from a single location using Central Console in Operations Manager.

- As an on-premises virtual machine - You can deploy DPM as a Hyper-V virtual machine as a single server or virtual machine cluster. You can install DPM in the same way as a physical installation. For detailed information, see the row [DPM installed as Hyper-V VM](install-dpm.md#setup-prerequisites) in the Setup prerequisites table.

::: moniker range="<=sc-dpm-2019"

- As an Azure virtual machine - You can install DPM 2019 as an Azure virtual machine. There are many restrictions in this deployment. For detailed information, see the row [DPM as an Azure virtual machine](install-dpm.md#setup-prerequisites) in the Setup prerequisites table.

- As a Windows virtual machine in VMware - You can install DPM 2019 on a Windows virtual machine in a VMware environment. In this configuration, DPM can protect Microsoft workloads running as Windows virtual machines in VMware.

::: moniker-end

::: moniker range="sc-dpm-2022"

- As an Azure virtual machine - You can install DPM 2022 as an Azure virtual machine. There are many restrictions in this deployment. For detailed information, see the row [DPM as an Azure virtual machine](install-dpm.md#setup-prerequisites) in the Setup prerequisites table.

- As a Windows virtual machine in VMware - You can install DPM 2022 on a Windows virtual machine in a VMware environment. In this configuration, DPM can protect Microsoft workloads running as Windows virtual machines in VMware.

::: moniker-end

::: moniker range="sc-dpm-2025"

- As an Azure virtual machine - You can install DPM 2025 as an Azure virtual machine. There are many restrictions in this deployment. For detailed information, see the row [DPM as an Azure virtual machine](install-dpm.md#setup-prerequisites) in the Setup prerequisites table.

- As a Windows virtual machine in VMware - You can install DPM 2025 on a Windows virtual machine in a VMware environment. In this configuration, DPM can protect Microsoft workloads running as Windows virtual machines in VMware.

::: moniker-end

### Sharing a library between different DPM versions isn't supported

**Issue**: Different versions of DPM (for example, DPM 2019 and DPM 2022) can't function as clients sharing the same library.

**Workaround**: None. All DPM servers sharing a library must be running the same version of DPM.

::: moniker range="sc-dpm-2016"

### Upgrading System Center 2010 directly to System Center 2016 isn't supported

**Issue**: Upgrade isn't supported.

**Workaround**: You'll need to upgrade to DPM 2012 R2 first.

::: moniker-end

::: moniker range="<=sc-dpm-2022"

### Performing item level recovery from Disk to Tape (D2T) for a Hyper-V VM fails with error 1001 
**Issue**: Item level recovery from tape for Hyper-V VM is not supported for the Disk to Tape (D2T) configuration for DPM 2016 to 2022.

**Workaround**: Restore the Hyper-V VM as a folder or configure Disk To Disk To Tape (D2D2T) for the VM.

::: moniker-end

### DPM doesn't run on the Turkish language version of Windows Server operating systems

**Issue**: No language support

**Workaround**: None

### DPM can't run on a server running a 32-bit operating system

**Issue**: Operating system limitation.

**Workaround**: Install on 64-bit only. For a full list of system requirements, see [Preparing your environment for System Center Data Protection Manager](prepare-environment-for-dpm.md).

### Underscore isn't supported in the SQL Server name

**Issue**: If you specify a remote SQL Server that has an underscore in the name during DPM installation, the installation might fail.

**Workaround**: Specify a SQL Server name that doesn't include the underscore `_` character.

### NTFS compression isn't supported on DPM volumes

**Issue**: NTFS not supported.

**Workaround**: None

### Renaming the DPM server isn't supported

**Issue**: Renaming not supported.

**Workaround**: None

### Moving the DPM server domain isn't supported

**Issue**: Moving the DPM server to a different domain after deployment isn't supported.

**Workaround**: None

### DPM on a domain controller can only protect local data sources

**Issue**: Deployment not supported.

**Workaround**: If you want to install the DPM protection agent on other computers to protect them, don't install DPM on a domain controller.

### DPM can't use SQL Server running on a domain controller

**Issue**: Database deployment not supported.

**Workaround**: If you want to use a remote instance of SQL Server as your DPM database, ensure that the SQL Server Instance isn't running on a domain controller.

::: moniker range="<=sc-dpm-2016"

### You can't install DPM 2016 on SQL 2016 SP1 (or a later release)

**Issue**: Installation on SQL 2016 SP1 (or a later release) isn't supported.

**Workaround**: None.

::: moniker-end

### Moving protected servers with DPM secondary servers

Moving protected servers between DPM servers that are under secondary protection isn't supported. To illustrate this, we've the following:

- Server1

- Server2

- DPM1 acting as the primary DPM server

- DPM2 acting as another primary DPM server

- DPM3 acting as a secondary server for DPM1 and DPM2

Where:

- Server1 is protected by DPM1

- Server2 is protected by DPM2

- DPM3 is a secondary server for DPM1 and DPM2 (and thus protects Server1 and Server2)

The following occurs:

- **Scenario 1**

    - DPM1 fails or is removed from the infrastructure.

    - You now want to protect Server1 with DPM2 (with DPM3 acting as the secondary server).

- **Scenario 2**

    - DPM1 fails or is removed from the infrastructure.

    - You now want to protect Server1 with DPM3.

Both scenarios are unsupported. You can only select one of the following options:

- **Option 1** - Use **Switch Protection** on DPM3 for Server1 and leave DPM3 in this mode going forward. Note that in this scenario you can't add secondary protection for Server1 on another DPM server when you're using the switched protection mode.

- **Option 2** - Rebuild DPM1 with the same name and restore the DPM database. This allows DPM to resume primary protection.

- **Option 3** - Move protection for Server1 to a new DPM server (DPM4) that DPM3 doesn't know about.

## <a name="BKMK_Storage"></a>Storage issues

### References to old tape libraries aren't removed from the DPM database

**Issue**: Obsolete tape libraries are still enumerated and listed in DPM PowerShell cmdlets such as get-dpmlibrary.

**Workaround**: None

### Virtual tape library support

::: moniker range="<=sc-dpm-2016"

**Issue**: Are virtual tape libraries supported?

**Workaround**: Virtual tape libraries configured with a virtual fiber channel adapter are only supported if you're running Data Protection Manager 2012 R2 UR3 or later with certified hardware. For the current list of supported hardware, see [Compatible Tape Libraries for System Center DPM 2012 and later](./dpm-compatible-tape-libraries.md). To check if your tape library is supported by the virtual fiber channel adapter, contact your tape hardware vendor, and ask them to [verify tape library compatibility](identify-compatible-tape-libraries.md).

::: moniker-end

::: moniker range="sc-dpm-2019"

**Issue**: Are virtual tape libraries supported?

**Workaround**: Virtual tape libraries configured with a virtual fiber channel adapter are supported on DPM 2019 or later with certified hardware. For the current list of supported hardware, see [Compatible Tape Libraries](dpm-compatible-tape-libraries.md). To check if your tape library is supported by the virtual fiber channel adapter, contact your tape hardware vendor and ask them to [verify tape library compatibility](identify-compatible-tape-libraries.md).

::: moniker-end

::: moniker range=">=sc-dpm-2022"

**Issue**: Are virtual tape libraries supported?

**Workaround**: Virtual tape libraries configured with a virtual fiber channel adapter are supported on DPM with certified hardware. For the current list of supported hardware, see [Compatible Tape Libraries](dpm-compatible-tape-libraries.md). To check if your tape library is supported by the virtual fiber channel adapter, contact your tape hardware vendor and ask them to [verify tape library compatibility](identify-compatible-tape-libraries.md).

::: moniker-end

### USB or removable drives can't be used in the DPM storage pool

**Issue**: USB and removable storage such as Firewire.

**Workaround**: None. This isn't supported due to a limitation with Windows dynamic disks.

### Data on CSVs

**Issue**: DPM only supports the protection of Hyper-V virtual machines on Cluster Shared Volumes (CSVs). Protection of other workloads hosted on Cluster Shared Volumes (CSVs) isn't supported.

::: moniker range="<=sc-dpm-2019"
Protection of SQL Server database stored on Cluster Shared Volume (CSV) is supported with [DPM 2019 UR2](what-s-new-in-dpm.md?view=sc-dpm-2019&preserve-view=true) and later.
::: moniker-end

::: moniker range="sc-dpm-2022"
Protection of SQL Server database stored on Cluster Shared Volume (CSV) is supported with [DPM 2022](what-s-new-in-dpm.md?view=sc-dpm-2022&preserve-view=true).
::: moniker-end

::: moniker range="sc-dpm-2025"
Protection of SQL Server database stored on Cluster Shared Volume (CSV) is supported with [DPM 2025](what-s-new-in-dpm.md?view=sc-dpm-2025&preserve-view=true).
::: moniker-end

**Workaround**: None.

### BitLocker

**Issue**: Is enabling BitLocker on DPM Storage Pool supported?

**Workaround**: Don't enable BitLocker before adding the disk to the storage pool. You can enable the BitLocker once you add the disk to the storage pool.

## <a name="BKMK_Dedup"></a>Deduplication issues

### Deduplicated volumes support

::: moniker range="<=sc-dpm-2019"

  >[!NOTE]
  >Deduplication support for DPM depends on the operating system support. Also, the [Data Deduplication](/windows-server/storage/data-deduplication/install-enable) server role must be installed on the DPM server to back up the volume with deduplication enabled.

::: moniker-end

**For NTFS Volumes:**

::: moniker range="sc-dpm-2016"

| Operating system of protected server | Operating system of DPM server | DPM version | Dedupe support  |
|------------------------------------------|------------------------------------|-----------------|--------------------|
| Windows Server 2016                      | Windows Server 2016                | DPM 2016        | Y               |
| Windows Server 2012 R2                   | Windows Server 2016                | DPM 2016        | Y                 |
| Windows Server 2012                     | Windows Server 2016                | DPM 2016        | Y                 |
| Windows Server 2016                      | Windows Server 2012 R2                | DPM 2016        | Y\*\*              |
| Windows Server 2012 R2                   | Windows Server 2012 R2                | DPM 2016        | Y                  |
| Windows Server 2012                      | Windows Server 2012 R2               | DPM 2016        | Y                  |

- **When protecting a WS 2019 NTFS deduped volume with DPM 2019 on a WS 2016 or a WS 2016 NTFS deduped volume with DPM 2016 on a WS 2012 R2, the backups and restores will be non-deduped. This means that the backups will consume more space on the DPM server than the original NTFS deduped volume.

::: moniker-end

::: moniker range="sc-dpm-2019"

| Operating system of protected server | Operating system of DPM server | DPM version | Dedupe support  |
|------------------------------------------|------------------------------------|-----------------|--------------------|
| Windows Server 2019                      | Windows Server 2019                | DPM 2019        | Y                  |
| Windows Server 2016                      | Windows Server 2019                | DPM 2019        | Y\*                |
| Windows Server 2012 R2                   | Windows Server 2019                | DPM 2019        | N                  |
| Windows Server 2012                      | Windows Server 2019                | DPM 2019        | N                  |
| Windows Server 2019                      | Windows Server 2016                | DPM 2019        | Y\*\*              |
| Windows Server 2016                      | Windows Server 2016                | DPM 2019        | Y                  |
| Windows Server 2012 R2                   | Windows Server 2016                | DPM 2019        | Y                  |
| Windows Server 2012                      | Windows Server 2016                | DPM 2019        | Y                  |

- *When protecting a WS 2016 NTFS Deduped Volume with DPM 2019 running on WS 2019, the recoveries may be affected. We've a fix for doing recoveries in a non-deduped way, which will be part of the later versions of DPM 2019. Reach out to DPM support if you need this fix on DPM 2019 UR2.

- **When protecting a WS 2019 NTFS deduped volume with DPM 2019 on a WS 2016 or a WS 2016 NTFS deduped volume with DPM 2016 on a WS 2012 R2, the backups and restores will be non-deduped. This means that the backups will consume more space on the DPM server than the original NTFS deduped volume.

**Issue**: If you upgrade the protected server operating system from Windows Server 2016 to Windows Server 2019, then the backup of NTFS deduped volume gets affected due to changes in dedupe logic.  

**Workaround**: Fix will be available in the future update rollup of DPM 2019. Reach out to DPM support in case you need this fix for DPM 2019 UR2.

**For ReFS Volumes:**

> [!NOTE]
>We've identified a few issues with backup of deduplicated ReFS volumes. We are working on fixing these and will update this section as soon as we've a fix available. Until then, we are removing the support for backup of deduplicated ReFS volumes from 2019 UR1.
>
>DPM 2019 UR1 and later continue to support protection and recovery of normal ReFS volumes.

::: moniker-end

::: moniker range="sc-dpm-2022"

  >[!NOTE]
  >- Deduplication support for DPM depends on operating system support. Also, the [Data Deduplication](/windows-server/storage/data-deduplication/install-enable) server role must be installed on the DPM server to back up the volume with deduplication enabled.
  >- We've identified a few issues with backup of deduplicated ReFS volumes. We are working on fixing these and will update this section as soon as we've a fix available.

| Operating system of protected server | Operating system of DPM server | DPM version | Dedupe support |
|---|---|---|---|
| Windows Server 2022 | Windows Server 2022 | DPM 2022 | Y |
| Windows Server 2019 | Windows Server 2022 | DPM 2022 | Y |
| Windows Server 2016 | Windows Server 2022 | DPM 2022 | Y\* |
| Windows Server 2022 | Windows Server 2019 | DPM 2022 | N |
| Windows Server 2019 | Windows Server 2019 | DPM 2022 | Y |
| Windows Server 2016 | Windows Server 2019 | DPM 2022 | Y\* |

- *Deduped NTFS volumes in Windows Server 2016 Protected Servers are non-deduplicated during restore.

::: moniker-end

::: moniker range="sc-dpm-2025"

  >[!NOTE]
  >- Deduplication support for DPM depends on operating system support. Also, the [Data Deduplication](/windows-server/storage/data-deduplication/install-enable) server role must be installed on the DPM server to back up the volume with deduplication enabled.
  >- We've identified a few issues with backup of deduplicated ReFS volumes. We are working on fixing these and will update this section as soon as we've a fix available.

| Operating system of protected server | Operating system of DPM server | DPM version | Dedupe support |
|---|---|---|---|
| Windows Server 2025 | Windows Server 2025 | DPM 2025 | Y |
| Windows Server 2022 | Windows Server 2025 | DPM 2025 | Y |
| Windows Server 2019 | Windows Server 2025 | DPM 2025 | Y\* |
| Windows Server 2025 | Windows Server 2022 | DPM 2025 | N |
| Windows Server 2022 | Windows Server 2022 | DPM 2025 | Y |
| Windows Server 2019 | Windows Server 2022 | DPM 2025 | Y\* |

- *Deduped NTFS volumes in Windows Server 2019 Protected Servers are non-deduplicated during restore.

::: moniker-end

### Windows deduplication isn't always supported on volumes hosting .VHD or .VHDX files

**Issue**: Dedupe support

**Workaround**: Deploy DPM as a virtual machine.

You can enable deduplication for DPM storage when it runs in a Hyper-V virtual machine and stored backup data to VHDs in shared folders on Windows File Servers with data deduplication enabled. For more information about this scenario, read [Deduplicating DPM storage](deduplicate-dpm-storage.md).

### The Dedup file system can't be protected to a secondary DPM server

**Issue**: After a dedup file system is protected by a primary DPM server, it can't be protected to a secondary DPM server.

**Workaround**: None.

### Item-level recovery not supported

**Issue**: If you're protecting virtual machines that contain deduped volumes, you can't perform item level recovery (ILR) from those VHD/VHDX files.

**Workaround**: Restore the .VHD/VHDX file that contains the deduped volume to a Windows Server that has the Data Deduplication role installed. Mount the .VHD file in disk management and copy out the desired files.

## <a name="BKMK_ClientServer"></a>Client and server protection issues

::: moniker range="<=sc-dpm-2016"

### Support parameters for protecting computers running client operating systems with DPM

**Issue**: The following protection scenarios are supported:

- Windows 10 clients can be protected with DPM 2019.
   >[!NOTE]
   > Windows 10 on ARM client isn't supported for protection using DPM.

- Windows 8.1 clients can be protected with DPM 2012 R2 and DPM 2016.

- Windows 7 clients can be protected with DPM 2012 R2 and DPM 2016.

**Workaround**: Ensure you're running the right version of DPM.

::: moniker-end

::: moniker range="sc-dpm-2019"

### Support parameters for protecting computers running client operating systems with DPM

**Issue**: The following protection scenarios are supported:

- Windows 10 clients can be protected with DPM 2019.
   >[!NOTE]
   > Windows 10 on ARM client isn't supported for protection using DPM.

**Workaround**: Ensure you're running the right version of DPM.

::: moniker-end

::: moniker range="sc-dpm-2022"

### Support parameters for protecting computers running client operating systems with DPM

**Issue**: Support for backing up Windows clients with DPM.

**Workaround**: DPM 2022 can back up Windows 10 and Windows 11 client computers. For information about supported workloads, see [What can DPM back up](/system-center/dpm/dpm-protection-matrix?view=sc-dpm-2022&preserve-view=true).

::: moniker-end

::: moniker range="sc-dpm-2025"

### Support parameters for protecting computers running client operating systems with DPM

**Issue**: Support for backing up Windows clients with DPM.

**Workaround**: DPM 2025 can back up Windows 10 and Windows 11 client computers. For information about supported workloads, see [What can DPM back up](/system-center/dpm/dpm-protection-matrix?view=sc-dpm-2025&preserve-view=true).

::: moniker-end

### Support for protecting computers running server operating systems with DPM

::: moniker range="<=sc-dpm-2016"
**Issue**: The following protection scenarios are supported:

- Windows Server 2012 R2 can be protected with DPM 2012 R2 and later.

- Windows Server 2012 or 2012 with SP1 can be protected with DPM 2012 R2 and later.

- Windows Server 2008 R2 with SP1, Windows Server 2008 R2 can be protected with DPM 2012 R2 and DPM 2016.

- Windows Server 2008 and Storage Server 2008 can be protected with DPM 2012 R2 running [Update Rollup 2](/archive/blogs/) and DPM 2016.

**Workaround**: Ensure you're running the right version of DPM.

::: moniker-end

::: moniker range="sc-dpm-2019"

**Issue**: Support for backing up Windows Server with DPM.

**Workaround**: DPM 2019 can back up Windows Server 2019 and 2016. For information about supported workloads, see [What can DPM back up](/system-center/dpm/dpm-protection-matrix?view=sc-dpm-2019&preserve-view=true).

::: moniker-end

::: moniker range="sc-dpm-2022"
**Issue**: Support for backing up Windows Server with DPM.

**Workaround**: DPM 2022 can back up Windows Server 2022, 2019, and 2016. For information about supported workloads, see [What can DPM back up](/system-center/dpm/dpm-protection-matrix?view=sc-dpm-2022&preserve-view=true).

::: moniker-end

::: moniker range="sc-dpm-2025"
**Issue**: Support for backing up Windows Server with DPM.

**Workaround**: DPM 2025 can back up Windows Server 2025, 2022, and 2019. For information about supported workloads, see [What can DPM back up](/system-center/dpm/dpm-protection-matrix?view=sc-dpm-2025&preserve-view=true).

::: moniker-end

### DPM can't protect SOFS shares

**Issue**: DPM can't protect shares on SOFS.

**Workaround**: Ensure shares you want to protect aren't located on SOFS.

## File server issues

::: moniker range="<=sc-dpm-2019"

### File Server end user recovery (EUR) isn't available when using Modern Backup Storage (MBS)

**Description**: If you use Modern Backup Storage (MBS) with DPM 2016 or later, File Server EUR isn't available.

**Workaround**: None. File Server EUR isn't supported when using MBS.

::: moniker-end

::: moniker range="sc-dpm-2022"

### File Server end-user recovery (EUR) isn't available when using Modern Backup Storage (MBS)

**Description**: File Server end user recovery (EUR) isn't available with DPM 2022 since it uses Modern Backup Storage.

**Workaround**: None. File Server EUR isn't supported when using MBS.

::: moniker-end

::: moniker range="sc-dpm-2025"

### File Server end-user recovery (EUR) isn't available when using Modern Backup Storage (MBS)

**Description**: File Server end user recovery (EUR) isn't available with DPM 2025 since it uses Modern Backup Storage.

**Workaround**: None. File Server EUR isn't supported when using MBS.

::: moniker-end

## <a name="BKMK_Data"></a>Data protection issues

### DPM doesn't back up shared VHDX

**Issue**: DPM can't back up VMs using shared drives (which are potentially attached to other VMs) as the Hyper-V VSS writer can't back up volumes that are backed up by shared VHDs.

**Workaround**: To avoid potential data loss, use another method to back up data on the shareable VHD.

### Protection might fail when changing the path of a data source

**Issue**: When you protect a shared folder, the path to the shared folder includes the logical path on the volume. If you move the shared folder, protection will fail. In addition, if you change the path of a protected data source on a volume that uses the Encrypting File System (EFS) and the new file path exceeds 5120 characters, data protection will fail.

**Workaround**: If you must move a protected shared folder, remove it from its protection group and then add it to protection after the move. For an encrypted volume, ensure that the new file path of the protected data source uses fewer than 5120 characters.

### Change the domain of a protected resource

**Issue**: You can't change the domain of a protected computer and continue protection without disruption. In addition, you can't change the domain of a protected computer and associate the existing replicas and recovery points with the computer when it's reprotected.

**Workaround**: We recommend that you don't change the domain of a protected computer. If you must change the domain of a protected computer, then first remove the data sources on the computer from protection. Then protect the data source on the computer after it has a new domain.

### Change the name of a protected resource

**Issue**: You can't change the name of a protected computer and continue protection without disruption. Also, you can't change the name of a protected computer and associate the existing replicas and recovery points with the computer when it's reprotected.

**Workaround**: We recommend that you don't change the name of a protected computer. If you must change the name of a protected computer, then first remove the data sources on the computer from protection. Then protect the data source on the computer after it has a new name.

### Change the time zone of a protected resource

**Issue**: Ensure that you update the time zone correctly if you change it for a protected resource.

**Workaround**: DPM automatically identifies the time zone of a protected computer during the installation of the protection agent. If a protected computer is moved to a different time zone after protection is configured, ensure that you change the computer time in the Control Panel. Then update the time zone in the DPM database.

### Some data types aren't supported

**Issue**: DPM doesn't support the following data types:

- Hard links

- Reparse points, including DFS links and junction points

- Mount point metadata - A protection group can contain data with mount points. In this case, DPM protects the mounted volume that is the target of the mount point, but it doesn't protect the mount point metadata. When you recover data containing mount points, you'll need to manually recreate your mount point hierarchy.

- Data in mounted volumes within mounted volumes

- Recycle Bin

- Paging files

- System Volume Information folder. To protect the system information of a computer, you'll need to select the computer's system state as the protect group member.

- Non-NTFS volumes

- Files containing hard links or symbolic links from Windows Vista.

- Files with any of the following combination of attributes:

    - Encryption and reparse

    - Encryption and Single Instance Storage (SIS)

    - Encryption and case-sensitivity

    - Encryption and sparse

    - Case-sensitivity and SIS

    - Compression and SIS

**Workaround**: None

### Limitations on protecting computers in workgroups and untrusted domains

**Issue**: DPM can protect workloads in the same domain as the DPM server or in child and trusted domains. You can also protect the following workloads in workgroups and untrusted domains using NTLM or certificate authentication:

- SQL Server

- File Server

- Hyper-V

These workloads can be running on a single server or in a cluster configuration.

**Workaround**: If you want to protect a workload that isn't in a trusted domain, see [Prepare computers in workgroups and untrusted domains](prepare-environment-for-dpm.md) for exact details of what's supported and what authentication is required.

### Short-term backup to tape isn't supported

**Issue**: DPM doesn't support short-term backup (incremental backup) to tape for workload data (Exchange, SQL Server, SharePoint, Hyper-V). Only file data (volumes, shares, folders) can be backed up incrementally.

**Workaround**: Use disk or a combination of disk and cloud storage (Azure Backup) for short-term backup of these workloads.

### Multiple long-term tape goals that use dataset-copy jobs fail if you only have a single tape drive

**Issue**: DPM doesn't support multiple long-term backup goals if you only have a single tape drive.

**Workaround**: Add a second tape drive to DPM or to the tape library.

### Backing up data on User Profile Disks (UPDs) isn't supported

**Issue**: Data on file shares hosting User Profile Disks (UPDs) can't be protected by DPM.

**Workaround**: None.

## <a name="BKMK_Exchange"></a>Exchange protection issues

### Disk-to-tape backup isn't supported for Exchange DAG

**Issue**: DPM doesn't support short-term or long-term disk-to-tape (D2T) backup for Exchange DAG workloads.

**Workaround**: Use disk-to-disk-to-tape (D2D2T) for Exchange DAG workloads.

## <a name="BKMK_Sharepoint"></a>SharePoint protection issues

::: moniker range="<=sc-dpm-2016"

### AlwaysOn not supported

**Issue**: From DPM 2012 R2 Update 5 onwards, DPM can protect SharePoint farm SQL Server databases that have AlwaysOn enabled.

**Workaround**: None.

::: moniker-end

::: moniker range="sc-dpm-2019"

### AlwaysOn not supported

**Issue**: DPM 2019 protects SharePoint farm SQL Server databases that have AlwaysOn enabled.

**Workaround**: None.

::: moniker-end

::: moniker range="sc-dpm-2022"

### AlwaysOn support

**Issue**: DPM 2022 protects SharePoint farm SQL Server databases that have AlwaysOn enabled.

**Workaround**: None.

::: moniker-end

::: moniker range="sc-dpm-2025"

### AlwaysOn support

**Issue**: DPM 2025 protects SharePoint farm SQL Server databases that have AlwaysOn enabled.

**Workaround**: None.

::: moniker-end

## <a name="BKMK_SQL"></a>SQL Server protection issues

::: moniker range="<=sc-dpm-2019"

### SQL Server 2016 support

**Issue**: You can protect SQL Server 2016 with DPM 2019 and later.

**Workaround**: Run the correct DPM version.

::: moniker-end

::: moniker range="sc-dpm-2022"

### SQL distributed availability group using Managed Instance Links

**Issue**: DPM cannot protect a SQL DAG when using [Managed Instance Links](/azure/azure-sql/managed-instance/managed-instance-link-feature-overview?view=azuresql).

**Workaround**: [Use Automated backups in Azure SQL Managed Instance](/azure/azure-sql/managed-instance/automated-backups-overview?view=azuresql).

### SQL Server 2022 support

**Issue**: You can protect SQL Server 2022 with DPM 2022 UR1.

**Workaround**: Run the correct DPM version.

::: moniker-end

### AlwaysOn support

**Issue**: AlwaysOn is supported in DPM.

**Workaround**: None.

### AlwaysOn recovery to original location isn't supported

**Issue**: When DPM is protecting SQL Server with AlwaysOn enabled, data recovery to the original location isn't supported.

**Workaround**: None.

### DPM can't protect SQL Server on scale-out file servers (SOFS)

**Issue**: DPM can't protect SQL Server databases hosted on Windows Server SOFS.

**Workaround**: Move the SQL Server databases off the SOFS.

### DPM can't protect SQL Server DAG or AG, where the role name on failover cluster is different from the named AG on SQL.

**Issue**: DPM can't protect SQL Server Distributed Availability Group (DAG) or Availability Group (AG), where the role name on failover cluster is different from the named AG on SQL.

**Workaround**: The role name for SQL Server DAG or AG on failover cluster must be the same as the SQL server availability group or distributed availability group name on SQL and vice versa.

## <a name="BKMK_VM"></a>Hyper-V and virtual machine protection issues

### Linux virtual machines backed up with file-consistent snapshots only

**Issue**: You can back up Linux virtual machines using DPM. Only file-consistent snapshots are supported.

**Workaround**: None.

### Backup of Hyper-V servers and clusters in trusted and untrusted domains

**Issue**: To back up Hyper-V server clusters, they must be located in the same domain as the DPM server or in a trusted or child domain. You can back up servers and clusters in an untrusted domain or workload using NTLM or certificate authentication for a single server or certificate authentication only for a cluster.

**Workaround**: None

### Backing up virtual machine data on pass-through disks isn't supported

Issue: DPM doesn't support the backup of virtual machine data on pass-through disks that present volumes to the virtual machine or that use a remote VHD.

Workaround: We recommend that in this scenario you use host-level backup of the VHD files using DPM and install an agent on the virtual machine to back up data that isn't visible on the host.

### Secondary DPM protection of a Hyper-V cluster isn't supported for a scaled-out DPM server deployment

**Issue**: When protecting a Hyper-V cluster using scaled-out DPM protection, you can't add secondary protection for the protected Hyper-V workloads.

**Workaround**: None

::: moniker range="<=sc-dpm-2016"

### Backup on Hyper-V Replica servers

**Issue**: Support for backup up of primary and replica (secondary) virtual machines depends on the DPM version as summarized in this table.

|DPM versions|**Windows Server 2012** - **Host operating system <br/> on replica (secondary/tertiary) server**|**Windows Server 2012 R2** - **Host operating system <br/> on replica (secondary/tertiary) server**|**Windows Server 2012** <br/> **Host operating system on primary server**|**Windows Server 2012 R2** <br/> **Host operating system on primary server**|
|-|-------------------------------------------------|---------------------------------------|-------------------------------------------------------------|--------------------------|
|DPM 2012, 2012 with SP1|Not supported|Not supported|Supported|Not supported|
|DPM 2012 R2|Not supported|Supported|Supported|Supported|

**Workaround**: Run a supported version of DPM for your scenario.

::: moniker-end

## DPM and Azure

### DPM as an Azure virtual machine

**Issue**: DPM can run as an Azure virtual machine. Be aware of these limitations:

- On-premises DPM servers can't protect Azure-based workloads.

- DPM running as an infrastructure as a service (IaaS) virtual machine, in Azure, can protect some workloads running as Azure virtual machines. For details, see the [DPM protection support matrix](dpm-protection-matrix.md).

- DPM running as an Azure virtual machine can't protect on-premises workloads.

**Workaround**: For more information about this scenario, see [Install DPM as an Azure virtual machine](install-dpm.md#setup-prerequisites).
