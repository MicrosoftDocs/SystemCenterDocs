---
ms.assetid:
title: Release Notes for System Center DPM
description: Release notes about the DPM 2016, 1801, 1807 and 2019 releases.
author: rayne-wiselman
ms.author: raynew
manager: carmonm
ms.date: 01/28/2020
ms.custom: na
ms.prod: system-center
ms.technology: data-protection-manager
ms.topic: article
---

# System Center DPM Release Notes

::: moniker range="sc-dpm-2019"

This article lists the release notes for System Center 2019 - Data Protection Manager (DPM).

::: moniker-end

::: moniker range="sc-dpm-1807"

This article lists the release notes for System Center 1807 - Data Protection Manager (DPM).

::: moniker-end

::: moniker range="sc-dpm-1801"

This article lists the release notes for System Center 1801 - Data Protection Manager (DPM).

::: moniker-end

::: moniker range="sc-dpm-2016"

This article lists the release notes for System Center 2016 - Data Protection Manager (DPM).

::: moniker-end

::: moniker range="sc-dpm-2019"

## DPM 2019 release notes

The following sections summarize the release notes for DPM 2019 and include the following known issues and workarounds.

### DPM console crashes due to MSDPM Service crash

**Description**: Presence of duplicate summary management jobs, after DPM upgrade, might lead to failure of any in-progress jobs at zero hours eventually leading to a crash. As a result, you might observe the following:

- Replica is inconsistent.
- Storage bloat caused due to non-deletions of recovery points.
- Outdated DPM reports.
- No clean-up for job history and garbage collection jobs.

**Workaround**:
1. Backup the current DPM database.
2. Open SQL management studio and connect to the SQL Instance hosting the DPMDB for this server.
3. Run the following query, and check if you have two or more summary manager jobs scheduled, and see which the older schedule was:
   ```
    SELECT SCH.ScheduleId, SCH.JobDefinitionId, jd.CreationTime
    FROM tbl_JM_JobDefinition JD
    JOIN tbl_SCH_ScheduleDefinition SCH
    ON JD.JobDefinitionId = SCH.JobDefinitionId
    WHERE JD.Type = '282faac6-e3cb-4015-8c6d-4276fcca11d4'        
    AND JD.IsDeleted = 0
    AND SCH.IsDeleted = 0
    ```
4. If you have more than one row returned, take the resulting ScheduleID and JobDefinitionID of the older entry and mark them as deleted.
   ```
    update tbl_SCH_ScheduleDefinition
    set IsDeleted = 1
    where ScheduleId = ‘ScheduleID '               --- Replace with Your ScheduleID
    update dbo.tbl_JM_JobDefinition
    set IsDeleted = 1
    where JobDefinitionId = ‘JobDefinitionID'             --- Replace with Your JobDefinitionID
   ```
5. Delete the SQL job that is matching the ScheduleID under the SQL Server Agent – JOBS. Once deleted, the crash at zero hours would be resolved.

   ScheduleId is the SQL Jobs under SQL agent:
   ```
   UPDATE MSDB.dbo.sysjobs
   SET Enabled = 0
   WHERE [Name] LIKE ‘ScheduleID’  --- Replace with Your ScheduleID  
   ```

### Hyper-V VMs are protected twice on VM upgrade

**Description**: When upgrading a Hyper-V VM from Windows Server 2012 R2 to Windows Server 2016, two versions of the VM appear in the Create Protection Group wizard.

**Workaround**: For the protected VMs which are about to be upgraded, make sure to stop protection with retain data before upgrading the VM. Then, upgrade the VM and reprotect it in a new protection group. While configuring reprotection, do a refresh on the VM host for DPM to detect the VM upgrade and protect it as RCT VM.

### Restoration of a previous version for an upgraded Hyper-V VM causes future recovery points to fail

**Description**: When you upgrade a protected 2012 R2 Hyper-V VM to the 2016 version, then stop protecting the VM (but retain data), and then re-enable protection, if you then recover a 2012 R2 copy at the original location, further backups might fail.

**Workaround**: After recovery, change the VM version to 2016, then run a consistency check.

### Bare Metal Recovery protection failures

**Description**: If you configure Bare Metal Recovery (BMR) protection, the BMR protection job might fail with the message that the replica size is not sufficiently large.

**Workaround**: Use the following registry path to change the default replica size for BMR data sources. Open the registry editor and increase the replica size for the following key:

**HKLM\Software\Microsoft\Microsoft Data Protection Manager\ConfigurationReplicaSizeInGBForSystemProtectionWithBMR (DWORD)**

### DPM database protection stops in case of upgrade scenarios

**Description**: When you upgrade DPM, database name might change in some scenarios.

**Workaround**: If you are protecting a DPM database, ensure to enable the protection for the new DPM database. Once the DPM upgrade is validated, you can remove protection for the previous DPM database.

### Hyper-V RCT - recover as files for D-T backup fails

**Description**: Recovery of Hyper-V RCT VMs as files created directly on tape (D-T) fails. D-D-T backups does not exhibit this issue.

**Workaround**: Use Alternate Location Recovery as a VM, and then transfer those files to the desired location.

>[!NOTE]
> This feature is fixed in DPM 2019 UR1. You can upgrade to DPM 2019 UR1 <add link to KB article> to fix this issue.

### DPM 2019 does not support file server end user recovery with Modern Backup Storage (MBS)

**Description**: DPM 2019 does not support end user recovery with Modern Backup Storage (MBS).

**Workaround**: None. File Server EUR is not supported when using MBS.

### DPM 1801/1807 servers cannot be managed by DPM 2019 central console

**Description**: With DPM 2019 central console you cannot manage any DPM 1801 or DPM 1807 servers.

**Workaround**: Upgrade your DPM server to version 2019.

::: moniker-end

::: moniker range="sc-dpm-1807"

## DPM 1807 Release notes

To view the list of bugs that have been fixed in DPM 1807, refer to [KB article 4339950](https://support.microsoft.com/help/4339950).

The following issues exist in the 1807 release.

### Hyper-V VMs are protected twice on VM upgrade

**Description**: When upgrading a Hyper-V VM from Windows Server 2012 R2 to Windows Server 2016, two versions of the VM appear in the Create Protection Group Wizard.

**Workaround**: For the VMs that haven't been upgraded, stop protection with Retain Data. Upgrade the VM, and create a new protection group. Then refresh the data sources, and protect the VMs. When you reapply protection, the VMs are protected using Resilient Change Tracking (RCT).


### Agent installation fails on Windows Server 2008, Windows Server 2008 R2

**Description**: When protecting Windows Server 2008, or Windows Server 2008 R2, installing the agent can fail.

**Workaround**: Upgrade the Windows Management Framework (WMF) on the production server to 4.0. Download the WMF from [https://www.microsoft.com/download/details.aspx?id=40855](https://www.microsoft.com/download/details.aspx?id=40855). Install WMF and then install the agent.

### Restoring a previous version of an upgraded Hyper-V VM causes future recovery points to fail.

**Description**: If you upgrade a protected 2012 R2 Hyper-V VM to the 2016 version, then stop protecting the VM (but retain data), and then re-enable protection, if you then recover a 2012 R2 copy at the original location, further backups may fail.

**Workaround**: After recovery, change the VM Version to 2016, then run a Consistency Check.

### Bare Metal Recovery protection failures

**Description**: If you configure Bare Metal Recovery (BMR) protection, the BMR protection job may fail with the message that the replica size is not sufficiently large.

**Workaround**: Use the following registry path to change the default replica size for BMR data sources. Open the registry editor and increase the replica size for the following key:

**HKLM\Software\Microsoft\Microsoft Data Protection Manager\ConfigurationReplicaSizeInGBForSystemProtectionWithBMR (DWORD)**

### Reprotecting the DPM database after upgrading to DPM 2016 or 1801

**Description**: When you upgrade from System Center DPM 2012 R2 to System Center Data Protection Manager 2016 or 1801, the DPM database name can change in some scenarios.

**Workaround**: If you are protecting a DPM database, be sure to enable protection for the new DPM database. Once the DPM upgrade is validated, you can remove protection for the old DPM database.

### Recovery Points not being pruned, leading to an accumulation of Recovery Points
**Description:** DPM prunes recovery points older than the retention range. During the pruning process, DPM calculates the storage consumed by those recovery points to be pruned. Storage calculation delays pruning.

**Workaround:** Configure DPM to skip calculating the size of recovery points to be pruned. As a result, the pruning script runs faster, and prunes all recovery points older than the retention range, relieving any storage pressures. The storage consumed per data source isn't updated until DPM finishes pruning. The storage consumption per volume continues to reflect the correct values.
Use a PowerShell script to turn on size calculation. The following script runs complete size calculations.

**Location:** Program Files\Microsoft System Center 2016\DPM\DPM\bin\Manage-DPMDSStorageSizeUpdate.ps1

**Script:** ```Manage-DPMDSStorageSizeUpdate.ps1 -ManageStorageInfo [StopSizeAutoUpdate | StartSizeAutoUpdate | GetSizeAutoUpdateStatus | UpdateSizeInfo ] [-UpdateSizeForDS <FilePath>] [-UpdatedDSSizeReport <FilePath>] [-FailedDSSizeUpdateFile <FilePath>]```

- **ManageStorageInfo:** - Specifies the kind of operation needed.

    - ***StopSizeAutoUpdate:*** Stops the size calculations completely. Both UI and Powershell will not report sizes.

    - ***StartSizeAutoUpdate:*** Resumes the size calculations. Immediately after enabling size calculations, use ```UpdateSizeInfo``` (in the following options) to recalculate sizes for all the datasources, until which sizes reported in PowerShell and UI may not be correct.

    - ***GetSizeAutoUpdateStatus:*** Tells whether size calculations are enabled or disabled.

    - ***UpdateSizeInfo:*** Triggers the size calculation and reports the size consumed by datasource. As this can be a long-running operation, use it only when needed, for scenarios such as billing. During this time, backups may fail with vhd mount errors.

- **UpdateSizeForDS:** Path to a text file with a list of Datasource IDs for which size needs to be calculated, with a datasourceID on each line. When not passed, size calculation is triggered for all the datasources.
    Use after using ```UpdateSizeInfo``` in ```ManageStorageInfo```.
    To get the Datasource IDs of specific datasources, use ``` Get-DPMProtectionGroup | Get-DPMDatasource | Format-table -Property Computer,name,ObjectType,Id```.

- **UpdatedDSSizeReport:** Path to a file that stores the updated datasource sizes. When not passed sizes.csv, a file is created in the execution directory.
    Use after ```UpdateSizeInfo``` in ```ManageStorageInfo```.

- ***FailedDSSizeUpdateFile:*** Path to a file to store the Datasource IDs for the datasources for which the storage consumption couldn’t be calculated. This may happen due to reasons as ongoing backups. When not passed failedDS.txt file is created in the execution directory. This file can be given as input to “UpdateSizeForDS” to update the sizes of all the datasources.
    This should be used after using ```UpdateSizeInfo``` in ```ManageStorageInfo```.

### Hyper-V RCT - recover as files for D-T backup fails

**Description**: Recovery of Hyper-V RCT VMs as files created directly on tape (D-T) fails. D-D-T does not exhibit this issue.

**Workaround**: Use Alternate Location Recovery as a VM, and then transfer those files to the desired location.


### File Server end user recovery (EUR) not available when using Modern Backup Storage (MBS)

**Description**: If you use Modern Backup Storage (MBS) with DPM 2016, File Server end-user recovery is not available.

**Workaround**: None. File Server EUR is not supported when using MBS.

::: moniker-end

::: moniker range="sc-dpm-1801"

## DPM 1801 Release notes

The following bugs have been fixed in the DPM 1801 release:

- Upgrading the DPM agent on the production server causes an unexpected reboot.
- Consistency checks for Hyper-V VMs transferred more data than the size of the VMs.

The following issues exist in the 1801 release.

### Silent Installation of System Center DPM with SQL Server 2008

**Description**: DPM 2016 RTM won't silently install on SQL Server 2008.

**Workaround**: Deploy DPM 2016 RTM on a version of SQL Server higher than 2008, or use the DPM 2016 Setup user interface.

## Remove-DPMDiskStorage cmdlet may delete volumes with active or inactive backups

**Description**: If the volume's datasources are being backed up (actively or inactively), when the [Remove-DPMDiskStorage](https://docs.microsoft.com/powershell/systemcenter/systemcenter2016/dataprotectionmanager/vlatest/Remove-DPMDiskStorage) cmdlet is used to remove volumes from DPM, the datasources can be removed too.

**Workaround**: Before using the cmdlet to remove the volumes, make sure the volume's datasources aren't in use (actively or inactively).

### DPM 2016 on Windows Server 2016 hangs

**Description**: Memory consumption on the DPM Server increases continuously until it reaches 90%. Memory consumption slows the DPM server.

**Workaround**: Upgrade DPM to DPM UR2 and install [KB4013429](https://support.microsoft.com/help/4013429/windows-10-update-kb4013429) to fix this issue.


### Hyper-V VMs are protected twice on VM upgrade

**Description**: When upgrading a Hyper-V VM from Windows Server 2012 R2 to Windows Server 2016, two versions of the VM appear in the Create Protection Group Wizard.

**Workaround**: For the VMs that haven't been upgraded, stop protection with Retain Data. Upgrade the VM, and create a new protection group. Then refresh the data sources, and protect the VMs. When you reapply protection, the VMs are protected using Resilient Change Tracking (RCT).

### Agent installation fails on Windows Server 2008, Windows Server 2008 R2

**Description**: When protecting Windows Server 2008, or Windows Server 2008 R2, installing the agent can fail.

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
**Description:** DPM prunes recovery points older than the retention range. During the pruning process, DPM calculates the storage consumed by those recovery points to be pruned. Storage calculation delays pruning.

**Workaround:** Configure DPM to skip calculating the size of recovery points to be pruned. As a result, the pruning script runs faster, and prunes all recovery points older than the retention range, relieving any storage pressures. The storage consumed per data source isn't updated until DPM finishes pruning. The storage consumption per volume continues to reflect the correct values.
Use a PowerShell script to turn on size calculation. The following script runs complete size calculations.

**Location:** Program Files\Microsoft System Center 2016\DPM\DPM\bin\Manage-DPMDSStorageSizeUpdate.ps1

**Script:** ```Manage-DPMDSStorageSizeUpdate.ps1 -ManageStorageInfo [StopSizeAutoUpdate | StartSizeAutoUpdate | GetSizeAutoUpdateStatus | UpdateSizeInfo ] [-UpdateSizeForDS <FilePath>] [-UpdatedDSSizeReport <FilePath>] [-FailedDSSizeUpdateFile <FilePath>]```

- **ManageStorageInfo:** - Specifies the kind of operation needed.

    - ***StopSizeAutoUpdate:*** Stops the size calculations completely. Both UI and Powershell will not report sizes.

    - ***StartSizeAutoUpdate:*** Resumes the size calculations. Immediately after enabling size calculations, use ```UpdateSizeInfo``` (in the following options) to recalculate sizes for all the datasources, until which sizes reported in PowerShell and UI may not be correct.

    - ***GetSizeAutoUpdateStatus:*** Tells whether size calculations are enabled or disabled.

    - ***UpdateSizeInfo:*** Triggers the size calculation and reports the size consumed by datasource. As this can be a long-running operation, use it only when needed, for scenarios such as billing. During this time, backups may fail with vhd mount errors.

- **UpdateSizeForDS:** Path to a text file with a list of Datasource IDs for which size needs to be calculated, with a datasourceID on each line. When not passed, size calculation is triggered for all the datasources.
    Use after using ```UpdateSizeInfo``` in ```ManageStorageInfo```.
    To get the Datasource IDs of specific datasources, use ``` Get-DPMProtectionGroup | Get-DPMDatasource | Format-table -Property Computer,name,ObjectType,Id```.

- **UpdatedDSSizeReport:** Path to a file that stores the updated datasource sizes. When not passed sizes.csv, a file is created in the execution directory.
    Use after ```UpdateSizeInfo``` in ```ManageStorageInfo```.

- ***FailedDSSizeUpdateFile:*** Path to a file to store the Datasource IDs for the datasources for which the storage consumption couldn’t be calculated. This may happen due to reasons as ongoing backups. When not passed failedDS.txt file is created in the execution directory. This file can be given as input to “UpdateSizeForDS” to update the sizes of all the datasources.
    This should be used after using ```UpdateSizeInfo``` in ```ManageStorageInfo```.

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


::: moniker range="sc-dpm-2016"

## System Center DPM 2016 Release Notes

### Silent Installation of System Center DPM with SQL Server 2008

**Description**: DPM 2016 RTM won't silently install on SQL Server 2008.

**Workaround**: Deploy DPM 2016 RTM on a version of SQL Server higher than 2008, or use the DPM 2016 Setup user interface.

## Remove-DPMDiskStorage cmdlet may delete volumes with active or inactive backups

**Description**: If the volume's datasources are being backed up (actively or inactively), when the [Remove-DPMDiskStorage](https://docs.microsoft.com/powershell/systemcenter/systemcenter2016/dataprotectionmanager/vlatest/Remove-DPMDiskStorage) cmdlet is used to remove volumes from DPM, the datasources can be removed too.

**Workaround**: Before using the cmdlet to remove the volumes, make sure the volume's datasources aren't in use (actively or inactively).


### DPM 2016 on Windows Server 2016 hangs

**Description**: Memory consumption on the DPM Server increases continuously until it reaches 90%. Memory consumption slows the DPM server.

**Workaround**: Upgrade DPM to DPM UR2 and install [KB4013429](https://support.microsoft.com/help/4013429/windows-10-update-kb4013429) to fix this issue.


### Hyper-V VMs are protected twice on VM upgrade

**Description**: When upgrading a Hyper-V VM from Windows Server 2012 R2 to Windows Server 2016, two versions of the VM appear in the Create Protection Group Wizard.

**Workaround**: For the VMs that haven't been upgraded, stop protection with Retain Data. Upgrade the VM, and create a new protection group. Then refresh the data sources, and protect the VMs. When you reapply protection, the VMs are protected using Resilient Change Tracking (RCT).

### Agent installation fails on Windows Server 2008, Windows Server 2008 R2

**Description**: When protecting Windows Server 2008, or Windows Server 2008 R2, installing the agent can fail.

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
**Description:** DPM prunes recovery points older than the retention range. During the pruning process, DPM calculates the storage consumed by those recovery points to be pruned. Storage calculation delays pruning.

**Workaround:** Configure DPM to skip calculating the size of recovery points to be pruned. As a result, the pruning script runs faster, and prunes all recovery points older than the retention range, relieving any storage pressures. The storage consumed per data source isn't updated until DPM finishes pruning. The storage consumption per volume continues to reflect the correct values.
Use a PowerShell script to turn on size calculation. The following script runs complete size calculations.

**Location:** Program Files\Microsoft System Center 2016\DPM\DPM\bin\Manage-DPMDSStorageSizeUpdate.ps1

**Script:** ```Manage-DPMDSStorageSizeUpdate.ps1 -ManageStorageInfo [StopSizeAutoUpdate | StartSizeAutoUpdate | GetSizeAutoUpdateStatus | UpdateSizeInfo ] [-UpdateSizeForDS <FilePath>] [-UpdatedDSSizeReport <FilePath>] [-FailedDSSizeUpdateFile <FilePath>]```

- **ManageStorageInfo:** - Specifies the kind of operation needed.

    - ***StopSizeAutoUpdate:*** Stops the size calculations completely. Both UI and Powershell will not report sizes.

    - ***StartSizeAutoUpdate:*** Resumes the size calculations. Immediately after enabling size calculations, use ```UpdateSizeInfo``` (in the following options) to recalculate sizes for all the datasources, until which sizes reported in PowerShell and UI may not be correct.

    - ***GetSizeAutoUpdateStatus:*** Tells whether size calculations are enabled or disabled.

    - ***UpdateSizeInfo:*** Triggers the size calculation and reports the size consumed by datasource. As this can be a long-running operation, use it only when needed, for scenarios such as billing. During this time, backups may fail with vhd mount errors.

- **UpdateSizeForDS:** Path to a text file with a list of Datasource IDs for which size needs to be calculated, with a datasourceID on each line. When not passed, size calculation is triggered for all the datasources.
    Use after using ```UpdateSizeInfo``` in ```ManageStorageInfo```.
    To get the Datasource IDs of specific datasources, use ``` Get-DPMProtectionGroup | Get-DPMDatasource | Format-table -Property Computer,name,ObjectType,Id```.

- **UpdatedDSSizeReport:** Path to a file that stores the updated datasource sizes. When not passed sizes.csv, a file is created in the execution directory.
    Use after ```UpdateSizeInfo``` in ```ManageStorageInfo```.

- ***FailedDSSizeUpdateFile:*** Path to a file to store the Datasource IDs for the datasources for which the storage consumption couldn’t be calculated. This may happen due to reasons as ongoing backups. When not passed failedDS.txt file is created in the execution directory. This file can be given as input to “UpdateSizeForDS” to update the sizes of all the datasources.
    This should be used after using ```UpdateSizeInfo``` in ```ManageStorageInfo```.


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
- To install DPM, see the article, [Install DPM](install-dpm.md).

- If you would like to consult planning information for your environment, see [Preparing your environment for System Center Data Protection Manager](prepare-environment-for-dpm.md).

- See these KBs for ReFS specific issues - [KB4016173](https://support.microsoft.com/en-us/help/4016173/fix-heavy-memory-usage-in-refs-on-windows-server-2016-and-windows-10), [KB4035951](https://support.microsoft.com/en-us/help/4035951/refs-volume-using-dpm-becomes-unresponsive-on-windows-server-2016).
