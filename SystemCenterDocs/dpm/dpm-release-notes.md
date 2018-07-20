---
ms.assetid:
title: Release Notes for System Center DPM
description: Release notes about the DPM 2016 and 1801 releases.
author: markgalioto
ms.author: markgal
manager: carmonm
ms.date: 7/19/2018
ms.custom: na
ms.prod: system-center-2016
ms.technology: data-protection-manager
ms.topic: article
---

# Release Notes for System Center Data Protection Manager (DPM)

The following set of notes lists known issues and steps to mitigate the issue. These notes apply to System Center Data Protection Manager (DPM) 2016 and Semi Annual Channel releases. By default you see the notes for 2016, 1801, and 1807 releases. If you are only interested in the 2016 release, select 2016 in the version picker.

::: moniker range="sc-dpm-1807"
## Release notes for System Center DPM 1807

To view the release notes for DPM 1807, refer to [KB article](https://go.microsoft.com/fwlink/?linkid=2006248&&clcid=0x409) which provides a list of bugs that have been fixed.

::: moniker-end


::: moniker range="sc-dpm-1801"
## Release notes for System Center DPM 1801

The following bugs have been fixed in the DPM 1801 release:

- Upgrading the DPM agent on the production server causes an unexpected reboot.
- Consistency checks for Hyper-V VMs transferred more data than the size of the VMs.

::: moniker-end


::: moniker range="sc-dpm-2016"
## Release Notes for System Center DPM 2016

### Silent Installation of System Center DPM with SQL Server 2008

**Description**: You cannot silently install DPM 2016 RTM on SQL Server 2008.

**Workaround**: Deploy DPM 2016 RTM on a version of SQL Server higher than 2008, or use the DPM 2016 Setup user interface.

## Remove-DPMDiskStorage cmdlet may delete volumes with active or inactive backups

**Description**: If the volume's datasources are being backed up (actively or inactively) when the [Remove-DPMDiskStorage](https://docs.microsoft.com/powershell/systemcenter/systemcenter2016/dataprotectionmanager/vlatest/Remove-DPMDiskStorage) cmdlet is used to remove volumes from DPM, the datasources can be removed too.

**Workaround**: Prior to using the cmdlet to remove the volumes, ensure the volumes do not have datasources being actively or inactively backed up.


### DPM 2016 on Windows Server 2016 slowing down and hanging due to high memory consumption
**Description**: Memory consumption on the DPM Server increases continuously, reaching about 90%, leading to the DPM server slowing down.

**Workaround**: The issue was found to lie in the underlying layers. The issue is fixed with [KB4013429](https://support.microsoft.com/help/4013429/windows-10-update-kb4013429) and SC 2016 DPM UR2.


### Hyper-V VMs are protected twice on VM upgrade

**Description**: If you upgrade your Hyper-V VM from Windows Server 2012 R2 to Windows Server 2016 to enable Resilient Change Tracking (RCT), a new VM representing the upgraded VM may appear in the Create Protection Group Wizard. The 2016 version of the VM may appear in addition to the 2012 R2 version of the VM.

**Workaround**: For the VMs that have not been upgraded, stop protection with Retain Data. After upgrading the VM, create a new protection group. Then, refresh the data sources and protect the VMs. Reapplying protection protects the VMs using Resilient Change Tracking (RCT).

### Agent installation fails on Windows Server 2008, Windows Server 2008 R2

**Description**: If you are trying to protect Windows Server 2008, or Windows Server 2008 R2, agent installation may fail.
**Workaround**: Upgrade the Windows Management Framework (WMF) on the production server to 4.0. Download the WMF from [https://www.microsoft.com/download/details.aspx?id=40855](https://www.microsoft.com/download/details.aspx?id=40855). Install WMF and then install the agent.


### Restoring a previous version of an upgraded Hyper-V VM causes future recovery points to fail.

**Description**: If you upgrade a protected 2012 R2 Hyper-V VM to the 2016 version, then stop protecting the VM (but retain data), and then re-enable protection, if you then recover a 2012 R2 copy at the original location, further backups may fail.

**Workaround**: After recovery, change the VM Version to 2016, then run a Consistency Check.


### Bare Metal Recovery protection failures

**Description**: If you configure Bare Metal Recovery (BMR) protection, the BMR protection job may fail with the message that the replica size is not sufficiently large.

**Workaround**: Use the following registry path to change the default replica size for BMR data sources. Open the registry editor and increase the replica size for the following key:

**HKLM\Software\Microsoft\Microsoft Data Protection Manager\ConfigurationReplicaSizeInGBForSystemProtectionWithBMR (DWORD)**


### Reprotecting the DPM database after upgrading to DPM 2016

**Description**: When you upgrade from System Center DPM 2012 R2 to System Center Data Protection Manager 2016, the DPM database name can change in some scenarios.

**Workaround**: If you are protecting a DPM database, be sure to enable protection for the new DPM database. Once the DPM upgrade is validated, you can remove protection for the old DPM database.


### Recovery Points not being pruned, leading to an accumulation of Recovery Points
**Description:** DPM prunes the recovery points older than the retention range. During the pruning process, DPM calculates the storage consumed by the recovery points to be pruned. The storage calculation, which takes some time, delays pruning which can lead to storage pressures.

**Workaround:** You can configure DPM to skip calculating the size of the recovery points to be pruned. As a result, the pruning script runs faster and prunes all the recovery points older than the retention range, relieving any storage pressures. The storage consumed per data source will not be updated until DPM is finished pruning. The storage consumption per volume continues to reflect the correct values.
The size calculation can be turned back on when needed by running a PowerShell script. To suppress size calculations and do complete size calculations again, you can use the following script:

***Location:*** Program Files\Microsoft System Center 2016\DPM\DPM\bin\Manage-DPMDSStorageSizeUpdate.ps1

***Script:*** Manage-DPMDSStorageSizeUpdate.ps1 -ManageStorageInfo [StopSizeAutoUpdate | StartSizeAutoUpdate | GetSizeAutoUpdateStatus | UpdateSizeInfo ] [-UpdateSizeForDS <FilePath>] [-UpdatedDSSizeReport <FilePath>] [-FailedDSSizeUpdateFile <FilePath>]

  1. ***ManageStorageInfo:*** Specifies the kind of operation needed.

    ***StopSizeAutoUpdate:*** Stops the size calculations completely. Both UI and Powershell will not report sizes.

    ***StartSizeAutoUpdate:*** Resumes the size calculations. Immediately after enabling size calculations, please use “UpdateSizeInfo” (in the following options) to recalculate sizes for all the datasources, until which sizes reported in PowerShell and UI may not be correct.

   ***GetSizeAutoUpdateStatus:*** Tells whether size calculations are enabled or disabled.

   ***UpdateSizeInfo:*** This triggers the calculation of sizes and reports the size consumed by a datasource. This can be a long running operation, so please use it only when needed for scenarios as billing. Note that during this time, backups may fail with vhd mount errors.

  2. ***UpdateSizeForDS:*** Path to a text file with a list of Datasource IDs for which size needs to be calculated, with a datasourceID on each line. When not passed, size calculation is triggered for all the datasources.
    This may be used after using “UpdateSizeInfo” in “ManageStorageInfo”.
    To get the Datasource IDs of specific datasources, please use “Get-DPMProtectionGroup | Get-DPMDatasource | Format-table -Property Computer,name,ObjectType,Id”.

  3. ***UpdatedDSSizeReport:*** Path to a file which will store the updated sizes of the datasources when the script is run. When not passed sizes.csv file is created in the execution directory.
    This should be used after using “UpdateSizeInfo” in “ManageStorageInfo”.

  4. ***FailedDSSizeUpdateFile:*** Path to a file to store the Datasource IDs for the datasources for which the storage consumption couldn’t be calculated. This may happen due to reasons as ongoing backups. When not passed failedDS.txt file is created in the execution directory. This file can be given as input to “UpdateSizeForDS” to update the sizes of all the datasources.
    This should be used after using “UpdateSizeInfo” in “ManageStorageInfo”.


### Hyper-V RCT - recover as files for D-T backup fails

**Description**: Recovery of Hyper-V RCT VMs as files created directly on tape (D-T) fails. D-D-T backups will not exhibit this issue.

**Workaround**: Use Alternate Location Recovery as a VM, and then transfer those files to the desired location.


### File Server end user recovery (EUR) not available when using Modern Backup Storage (MBS)

**Description**: If you use Modern Backup Storage (MBS) with DPM 2016, File Server end-user recovery is not available.

**Workaround**: None. File Server EUR is not supported when using MBS.

### Error 4387 might appear while installing DPM

**Description**: While installing the Data Protection Manager, when you enter an SQL instance in the **Data Protection Manager Setup** > **Prerequisites check**> **Instance of SQL server** text box, error 4387 might appear.

**Workaround**: Perform the required actions as detailed in this [KB article](https://support.microsoft.com/en-in/help/956013/error-message-when-you-open-sql-server-configuration-manager-in-sql-se) and try the  DPM setup again.
::: moniker-end



## Next steps
To install DPM, see the article, [Install DPM](install-dpm.md).

If you would like to consult planning information for your environment, see [Preparing your environment for System Center 2016 Data Protection Manager](prepare-environment-for-dpm.md).
