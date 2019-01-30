---
description: This article explains how to upgrade your DPM installation to version 2019.
manager:  vvithal
ms.topic:  include
author:  JYOTHIRMAISURI
ms.author: v-jysur
ms.prod:  system-center
keywords:
ms.date:  1/30/2019
title:  include file
ms.technology:  data-protection-manager
ms.assetid: 31fd4dc7-3f1c-476d-8224-0111db09c11c
---

## Upgrade to DPM 2019

You can install System Center - 2019  Data Protection Manager (DPM) on Windows Server 2016 or 2019.

You can upgrade to DPM 2019 from the following versions:
-  DPM 2016
-  DPM 1801
-  DPM 1807

 Before you upgrade to or install DPM 2019, read the [Installation prerequisites](../dpm/install-dpm.md#setup-prerequisites).


## Upgrade path for DPM 2019
If you upgrade from DPM 2016 to DPM 2019, make sure your installation has the following necessary updates:

- If you are upgrading from DPM 2016, then first upgrade to DPM 2016 Update Rollup 6 or later. You can download the Update Rollups from Windows Update.
- Upgrade the DPM server to DPM 2019.
- Update the agents on the protected servers.
- Upgrade the DPM Remote Administrator on all production servers.
- Backups continue without rebooting your production server.


### Upgrade steps for DPM

1. To install DPM, double-click Setup.exe to open the System Center 2019 wizard.
2. Under Install, click Data Protection Manager to start the setup wizard. Agree to the license terms and conditions and follow the setup wizard.

 For instructions on installing DPM, see the article, [Installing DPM](../dpm/install-dpm.md).

## Migrate the DPM database during upgrade

You may want to move the DPM Database as part of an upgrade. For example:
- You are merging instances of SQL Server.
- You are moving to a remote more powerful SQL server.
- You want to add fault tolerance by using a SQL Server cluster; or you want to move from a remote SQL server to a local SQL server or vice versa.

DPM 2019 setup allows you to migrate the DPM database to different SQL Servers during an upgrade.

### Possible database migration scenarios

The following scenarios exist when upgrading DPM 2016/1801/1807 to DPM 2019 using a:

1. Local instance and migrating to a remote instance of SQL Server during setup.
2. Remote instance and migrating to a local instance of SQL Server during setup.
3. Local instance and migrating to a remote SQL Server Cluster instance during setup.
4. Local instance and migrating to a different local instance of SQL Server during setup.
5. Remote instance and migrating to a different remote instance of SQL Server during setup.
6. Remote instance and migrating to a remote SQL Server Cluster instance during setup.

### Prepare for a database migration

If you want to use a new SQL server to migrate the DPM database, before you upgrade DPM, be sure both SQL Servers have the same:
- SQL Server requirements
- Setup configuration
- Firewall rules
- DPM Support files (sqlprep)

Once you have the new instance of SQL Server installed and prepared for DPM use, you must make a backup of the current DPM database and restore it on the new SQL Server.

### Pre-upgrade steps: Backup and restore DPM 2016/1801/1807database to a new SQL instance

This example prepares a remote SQL Server cluster to use in a migration.

1. On the System Center Data Protection Manager server or on the remote SQL Server hosting the DPM database, start **Microsoft SQL Management Studio** and connect to the SQL instance hosting the current DPM DPMDB.
2. Right-click the DPM database, and under **Tasks**, select the **Back Up…** option.

      ![Select Backup](../dpm/media/upgrade-to-dpm-2016/dpm-2016-select-backup.png)

3. Add a backup destination and file name, and then select **OK** to start the backup.

      ![Confirm](../dpm/media/upgrade-to-dpm-2016/dpm-2016-confirm.png)

4. After the backup is complete, copy the output file to the remote SQL Server.  If this is a SQL Cluster, copy it to the active node hosting the SQL instance you want to use in the DPM upgrade.  Before you can restore the DPM database, you must copy it to the Shared Cluster disk.
5. On the Remote SQL Server, start **Microsoft SQL Management Studio** and connect to the SQL instance you want to use in the DPM upgrade.  If this is a SQL Cluster, do this on the Active node that you copied the DPM backup file to.  The backup file should now be located on the shared cluster disk.
6. Right-click the Databases icon, then select the **Restore Database…** option. This starts the restore wizard.

      ![Select restore database](../dpm/media/upgrade-to-dpm-2016/dpm-2016-select-restore-database.png)        

7. Select **Device** under **Source**, and then locate the database backup file that was copied in the previous step and select it. Verify the restore options and restore location, and then select **OK** to start the restore. Fix any issue that arise until the restore is successful.

      ![Restore database](../dpm/media/upgrade-to-dpm-2016/dpm-2016-restore-database.png)

8. After the restore is complete, the restored database will be seen under **Databases** with the original name. This database will be used during the upgrade. You can exit **Microsoft SQL Management Studio** and start the upgrade process on the original DPM server.

      ![Select DPMDB](../dpm/media/upgrade-to-dpm-2016/dpm-2016-select-dpmdb.png)

9. If the new SQL server is a remote SQL server, install the SQL management tools on the DPM server. The SQL management tools must be the same version matching the SQL server hosting the DPMDB.

### Start upgrade to migrate DPMDB to a different SQL Server

> [!NOTE]
> If sharing a SQL instance, run the DPM installations (or upgrades) sequentially. Parallel installations may cause errors.

1. After the pre-migration preparation steps are complete, start the DPM 2019 Installation process.  DPM Setup shows the information about current instance of SQL server pre-populated. This is where you can select a different instance of SQL server, or change to a Clustered SQL instance used in the migration.

      ![DPM setup](../dpm/media/upgrade-to-dpm-2016/dpm-2016-data-protection-manager-setup.png)

2. Change the SQL Settings to use the instance of SQL server you restored the DPM Database to. If it’s a SQL cluster, you must also specify a separate instance of SQL Server  used for SQL reporting. It's presumed that firewall rules and SQLPrep are already ran. You have to enter correct credentials and then click the **Check and Install** button.

      ![Install database](../dpm/media/upgrade-to-dpm-2016/dpm-2016-install-database.png)

3. Prerequisite check should succeed, click **Next** to continue with the upgrade.

      ![Prerequisites check](../dpm/media/upgrade-to-dpm-2016/dpm-2016-prerequisites-check.png)

4. Continue with the wizard options and complete the setup.

5. After the setup is complete, the corresponding database name on the instance specified will now be *DPMPB_DPMServerName*. Because this may be shared with other DPM servers, the naming convention for the DPM database will now be: *DPM2016$DPMDB_DPMServerName*

## Add storage for Modern Backup Storage

To store backups efficiently, DPM 2019 uses Volumes. Disks can also be used to continue storing backups.

### Add volumes and disks
If you run DPM 2019 on Windows Server, you can use volumes to store backup data. Volumes provide storage savings and faster backups. You can give the volume a friendly name, and you can change the name. You apply the friendly name while adding the volume, or later by selecting the **Friendly Name** column of the desired volume. You can also use PowerShell to add or change friendly names for volumes.

To add a volume in the administrator console:

1. In the DPM Administrator console, select the **Management** feature > **Disk Storage** > **Add**.

2. In the **Add Disk Storage** dialog, select an available volume > click **Add** > type a friendly name for the volume > click **OK**.

      ![Add volume](../dpm/media/upgrade-to-dpm-2016/dpm-2016-add-volume.png)

If you want to add a disk, it must belong to a protection group with legacy storage. Those disks can only be used for those protection groups. If the DPM server doesn't have sources with legacy protection, the disk won't appear.
See the topic, [Adding disks to increase legacy storage](#adding-disks-to-increase-legacy-storage), for more information on adding disks. You can't give disks a friendly name.


### Assign Workloads to Volumes

DPM 2019 allows the user to specify the types of workloads to be assigned to specific volumes. For example, expensive volumes that support high IOPS can be configured to store only the workloads that require frequent, high-volume backups like SQL with Transaction logs.
To update the properties of a volume in the storage pool on a DPM server, use the PowerShell cmdlet, *Update-DPMDiskStorage*.

**Update-DPMDiskStorage**

**Syntax**

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

The changes made through PowerShell are reflected in the UI.


## Protect data sources
To begin protecting data sources, create a Protection Group. The following procedure highlights changes or additions to the **New Protection Group** wizard.

To create a Protection Group:

1. In the DPM Administrator Console, select the **Protection** feature.

2. On the tool ribbon, click **New**.

    The **Create new Protection Group** wizard opens.

  ![Create protection group](../dpm/media/upgrade-to-dpm-2016/dpm-2016-protection-wiz.png)

3. Click **Next** to advance the wizard to the **Select Protection Group Type** screen.
4. On the **Select Protection Group Type** screen, select the type of Protection Group to be created and then click **Next**.

  ![Choose server or client](../dpm/media/upgrade-to-dpm-2016/dpm-2016-protection-group-screen2.png)

5. On the **Select Group Members** screen, in the **Available members** pane, DPM lists the members with protection agents. For the purposes of this example, select volume D:\ and E:\ to add them to the **Selected members** pane. Once you have chosen the members for the protection group, click **Next**.

  ![Select group members for protection group](../dpm/media/upgrade-to-dpm-2016/dpm-2016-protection-screen3.png)

6. On the **Select Data Protection Method** screen, type a name for the **Protection group**, select the protection method(s) and click **Next**.
    If you want short term protection, you must use Disk backup.

  ![Select data protection method](../dpm/media/upgrade-to-dpm-2016/dpm-2016-protection-screen4.png)

7. On the **Specify Short-Term Goals** screen specify the details for **Retention Range** and **Synchronization Frequency**, and click **Next**. If desired, click **Modify** to change the schedule when recovery points are taken.

  ![Select data protection method](../dpm/media/upgrade-to-dpm-2016/dpm-2016-protection-screen5.png)

 The **Review Disk Storage Allocation** screen provides details about the selected data sources, their size, the **Space to be Provisioned**, and **Target Storage Volume**.

  ![Review Disk Storage Allocation](../dpm/media/upgrade-to-dpm-2016/dpm-2016-protection-screen6.png)

  The storage volumes are determined based on the workload volume allocation (set using PowerShell) and the available storage. You can change the storage volumes by selecting other volumes from the drop-down menu. If you change the **Target Storage**, the **Available disk storage** dynamically changes to reflect the **Free Space** and **Underprovisioned Space**.

  The **Underprovisioned Space** column in **Available disk storage**, reflects the amount of additional storage needed if the data sources grow as planned. Use this value to help plan your storage needs to enable smooth backups. If the value is zero, then there are no potential problems with storage in the foreseeable future. If the value is a number other than zero, then you do not have sufficient storage allocated  - based on your protection policy and the data size of your protected members.

  ![Underallocated disk storage](../dpm/media/upgrade-to-dpm-2016/dpm-2016-underprovision-storage.png)

The remainder of the New Protection Group wizard is unchanged from earlier version. Continue through the wizard to complete creation of your new protection group.

## Migrate legacy storage to Modern Backup Storage
After upgrading to DPM 2019 and the operating system to Windows Server 2016/2019, you can update your existing protection groups to the new DPM 2016 features. By default, protection groups are not changed, and continue to function as they were configured in earlier version of your DPM. You can optionally update protection groups to use Modern Backup Storage is optional. To update the protection group, stop protection of all data sources with **Retain Data** option, and add the data sources to a new protection group. DPM begins protecting these data sources the new way.

Use the following steps:

1. In the Administrator Console, select the **Protection** feature, and in the **Protection Group Member** list, right-click the member, and select **Stop protection of member...**.

  ![Stop protection](../dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

  The **Remove from Group** dialog opens.

2. In the **Remove from Group** dialog, review the used disk space and the available free space in the storage pool. The default is to leave the recovery points on the disk and allow them to expire per their associated retention policy. Click **OK**.

    If you want to immediately return the used disk space to the free storage pool, select **Delete replica on disk**. This will delete the backup data (and recovery points) associated with that member.

    ![Retain data](../dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. Create a new protection group that uses Modern Backup Storage, and include the unprotected data sources.


## Add Disks to increase legacy storage

If you want to use legacy storage with DPM 2019, it may become necessary to add disks to increase legacy storage. To add disk storage:

1. On the Administrator Console, click **Management**.

2. Select **Disk Storage**.

3. On the tool ribbon click **Add**.

    The **Add Disk Storage** dialog opens.

    ![Add disks](../dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. In the **Add Disk Storage** dialog, click **Add disks**.

    DPM provides a list of available disks.

5. Select the disks, click **Add** to add the disks, and click **OK**.

## New PowerShell cmdlets

For DPM 2016, two new cmdlets: [Mount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787159.aspx) and [Dismount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787158.aspx) are available. Click the cmdlet name to see its reference documentation.


## Enable Cloud Protection

You can back up a DPM server to Azure. The high level steps are:
- Create an Azure subscription,
- Register the server with the Azure Backup service,
- Download vault credentials and the Azure Backup Agent,
- Configure the server's vault credentials and backup policy,

For more information on backing up DPM to the cloud, see the article, [Preparing to backup workloads to Azure with DPM](https://azure.microsoft.com/documentation/articles/backup-azure-dpm-introduction).
