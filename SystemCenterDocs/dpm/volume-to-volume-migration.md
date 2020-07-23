---
title:  System Center - Data Protection Manager volume to volume migration
description: This article describes volume to volume migration.
manager: vvithal
ms.topic: article
author: v-anesh
ms.prod: system-center
keywords:
ms.date: 06/16/2020
ms.technology: data-protection-manager
ms.assetid: 6595b781-554d-4807-b035-d0eccd35deb3
ms.author: v-anesh
monikerRange: '>=sc-dpm-2019'
---

# Migrate datasources to new volumes

There are various reasons why a [volume migration](add-storage.md#migrate-data-to-newly-created-volumes) is required: the underlying storage in the old volume can have fragmentation, or the old volume would have reached the limit of maximum allowed storage size or you want to store your backups on a high-performance underlying storage.

DPM supports the following two options to migrate data to a new volume:

- **Full migration (default)**

  With this feature, all the data for a particular data source is migrated from current volume to the new volume. The time to complete the migration is based on the size of the protected data source, larger the data source, more time it takes to migrate to the other volume.

- **Optimized migration**

   > [!NOTE]
   > This option is applicable from DPM 2019 UR2 and later versions.

  The optimized volume to volume migration allows you to move data sources to the new volume much faster. The enhanced migration process migrates only the active backup copy (Active Replica) to the new volume. All the new recovery points are created on the new volume while existing recovery points are maintained on the existing volume and are purged as per the retention policy.

  To use this option, first add the registry key as per the details below:

  - **Key Path**: HKLM\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Configuration\DiskStorage <br>
  - **Type**: DWORD <br>
  - **Name**: OptimizedMigrate <br>
  - **Value**: 1

## Migrate datasource from one volume to the other volume using console

Follow these steps:

1. In the DPM Administrator Console, click **Protection**.

2. In the **Protection** workspace, select the datasource you want to migrate.

   ![Select target workload](./media/volume-volume-migration/move-disk-storage.png)

3. Click **Move Disk Storage**.

   ![Move disk storage](./media/volume-volume-migration/select-target-disk-storage.png)


4. Select the *target disk storage* that you want to migrate to, and click **OK**.

   ![Select target disk storage](./media/volume-volume-migration/select-workload.png)


   This begins the migration process. For monitoring scheduled jobs, you can open another DPM console in parallel, while the migration is in progress.

## Migrate datasource from one volume to the other volume using PowerShell

   Here is an example for migrating data source from one volume to the other volume using PowerShell:

```powershell
   #Create a modifiable Protection Group of the PG the datasource is in.
   $pg = Get-DPMProtectionGroup
   $mpg = Get-DPMModifiableProtectionGroup $pg[0]
   #Get the datasource you wish to migrate, and the volume you wish to migrate it to.
   $ds = Get-DPMDatasource $mpg
   $vols = Get-DPMDiskStorage -Volumes
   #Modify the disk allocation for the datasource, and save the PG.
   Set-DPMDatasourceDiskAllocation -ProtectionGroup $mpg -Datasource $ds[0] -TargetStorage $vols[0] -MigrateDatasourceDataFromDPM
   Set-ProtectionGroup $mpg
```

   These steps enable you to have more control over your storage while giving you the freedom to balance storage utilization across volumes.
