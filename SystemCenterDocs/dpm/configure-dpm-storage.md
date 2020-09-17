---
description: Learn about the new features when you upgrade to DPM 2016 and later. This article also provides an overview of how to upgrade your DPM installation.
manager: vvithal
ms.topic: article
author: v-anesh
ms.author: v-anesh
ms.prod: system-center
keywords:
ms.date: 09/17/2020
title: Configure DPM storage
ms.technology: data-protection-manager
ms.assetid: 5a9e1b8d-cf29-45ce-9b9a-2a63d65c9fd6
---


## Configure DPM Storage

Windows Storage Spaces allows you to pool multiple physical disks together into one logical drive. It provides an easy way to create software-defined storage using a server's local storage resources. Follow the steps in the procedures below to set up MBS with tiered storage. Follow the procedures in the sequence, as listed below:

> [!NOTE]
> Migrate your current backups to a temporary volume using [Volume Migration](add-storage.md#migrate-data-to-newly-created-volumes), in case you wish to modify your existing storage to tiered storage.

1. Prepare physical disks and create Windows Storage Pool
2. Create tiered storage with required resiliency option.
3. Add volume to DPM storage
4. Migrate your data back to the newly created volumes using volume migration, done before to step 1.

   > [!NOTE]
   > Applicable only if you have migrated your earlier backups before step 1.

### Preparing physical disks and Create Windows Storage Pool

#### Initialize Disks

Based on the resiliency option that you have selected, calculate the number of HDDs ad SSDs required. The new disks attached to server needs to be initialized first, before the disks can be added to the storage pool. If the disks that you are using are more than 2TB in size it will be converted to a GPT Disk.

To Initialize the disk, follow these steps:

1. Open  **Server Manager**.
2. Click  **File and Storage Services**.
3. Click  **Volumes** and then **Disks Pools**.
4. Right-click the disks and select **Initialize**
5. Select **Yes** to initialize the disk and convert it to GPT disk.
6. Repeat the steps for the remaining disks that needs to be initialized.

   ![Using Server Manager](./media/add-storage/using-server-manager.png)

#### Check Primordial pool

By default, available disks are included in a pool that is named the _primordial_ pool. If no primordial pool is listed under  **Storage Pools**, this indicates that the storage does not meet the requirements for Storage Spaces. Make sure that the disks meet the requirements that are outlined in the prerequisites section.

Run the following command to view the physical disks available in the primordial pool:

```PowerShell
Get-StoragePool -IsPrimordial $true | Get-PhysicalDisk | Where-Object CanPool -eq $True
```

**Example:**
```
PS C:\\> Get-StoragePool -IsPrimordial $true | Get-PhysicalDisk | Where-Object CanPool -eq $True

Number FriendlyName      SerialNumber MediaType   CanPool OperationalStatus HealthStatus Usage         Size
------ ------------      ------------ ---------   ------- ----------------- ------------ -----         ----
4      Msft Virtual Disk              Unspecified True    OK                Healthy      Auto-Select   5 TB
3      Msft Virtual Disk              Unspecified True    OK                Healthy      Auto-Select   5 TB
2      Msft Virtual Disk              Unspecified True    OK                Healthy      Auto-Select   5 TB
1      Msft Virtual Disk              Unspecified True    OK                Healthy      Auto-Select 750 GB

```

![Check Primordial Pool](./media/add-storage/check-primordial-pool.png)

#### Create a Storage pool

You need to create new Storage Pool with logical sector size of 4K. Follow the steps below to configure the new storage pool. We are creating the storage volume with single disk initially.

Run the following command to create the storage pool

```PowerShell
New-StoragePool –FriendlyName DPMPool –StorageSubsystemFriendlyName (Get-StorageSubSystem).FriendlyName –PhysicalDisks (Get-PhysicalDisk –CanPool $True) -LogicalSectorSizeDefault 4096 -FaultDomainAwarenessDefault PhysicalDisk
```

**Example:**

```
PS C:\> New-StoragePool -FriendlyName DPMPool -StorageSubsystemFriendlyName (Get-StorageSubSystem).FriendlyName -PhysicalDisks
(Get-PhysicalDisk -CanPool $True) -LogicalSectorSizeDefault 4096 -FaultDomainAwarenessDefault PhysicalDisk


FriendlyName OperationalStatus HealthStatus IsPrimordial IsReadOnly     Size AllocatedSize
------------ ----------------- ------------ ------------ ----------     ---- -------------
DPMPool      OK                Healthy      False        False      15.73 TB          1 GB

```
![Create Storage Pool](./media/add-storage/create-storage-pool.png)

#### Set mediaType to SSD or HDD to the disks


By default, Windows would automatically detect the type of disk that is attached and list it as either SSD or HDD. In case if the *MediaType* is set as *Unspecified* use the following command to set the appropriate *MediaType* manually.

> [!NOTE]
> It is important that you know which disk is SSD and set the MediaType correctly. You can use Size of the disk as one of the identifiers.

1. Run the following command to check the MediaType

   ```PowerShell
   Get-PhysicalDisk|FTDeviceID,BusType,MediaType,Size,UniqueId
   ```

   Example:
   ```
   PS C:\> Get-PhysicalDisk | FT DeviceID, BusType, MediaType, Size, UniqueId

   DeviceID BusType MediaType            Size UniqueId
   -------- ------- ---------            ---- --------
   0        SAS     Unspecified  136365211648 60022480E16E85F23C2C3B8BED321866
   4        SAS     Unspecified 5497558138880 60022480DB4A64573FEC4C9C82BB48EB
   3        SAS     Unspecified 5497558138880 60022480183A590476AA8940A84C8E9D
   2        SAS     Unspecified 5497558138880 60022480965A3579C3EB929E0BA39776
   1        SAS     Unspecified  805306368000 600224802D66666E313C92E116E2ADA1
   ```

   ![Set Media Type](./media/add-storage/set-mediatype.png)


2. In the above example we need to assign SSD to disk with DeviceID as 1 and HDD to disks 2,3,4.

   To set MediaType run the following commands
   ```PowerShell
   Set-PhysicalDisk -UniqueId "600224802D66666E313C92E116E2ADA1" -MediaType SSD
   Set-PhysicalDisk -UniqueId "60022480965A3579C3EB929E0BA39776" -MediaType HDD
   Set-PhysicalDisk -UniqueId "60022480183A590476AA8940A84C8E9D" -MediaType HDD
   Set-PhysicalDisk -UniqueId "60022480DB4A64573FEC4C9C82BB48EB" -MediaType HDD
   ```

   ![Assign SSD](./media/add-storage/assign-ssd.png)

3. Ensure that the MediaType is set correctly. Run the following command
   ```PowerShell
   Get-PhysicalDisk | FT DeviceID, BusType, MediaType, Size, UniqueId
   ```

   Example:
   ```
   PS C:\> Get-PhysicalDisk | ft Deviceid, BusType, MediaType, Size, UniqueID

   Deviceid BusType MediaType            Size UniqueID
   -------- ------- ---------            ---- --------
   0        SAS     Unspecified  136365211648 60022480E16E85F23C2C3B8BED321866
   4        SAS     HDD         5497558138880 60022480DB4A64573FEC4C9C82BB48EB
   3        SAS     HDD         5497558138880 60022480183A590476AA8940A84C8E9D
   2        SAS     HDD         5497558138880 60022480965A3579C3EB929E0BA39776
   1        SAS     SSD          805306368000 600224802D66666E313C92E116E2ADA1
   ```

   ![Correct Media Type](./media/add-storage/correct-media-type.png)


#### Disable Write-Back Cache

Disable Write-Back Cache to disable auto caching at storage pool level (needed only for tiered storage).

To do this, go to PowerShell and execute the following commands:
```PowerShell
Set-StoragePool -FriendlyName DPMPool -WriteCacheSizeDefault 0
```

![Disable Write Back Cache](./media/add-storage/disable-write-back.png)


### Create tiered storage volume

Before creating the tired storage, you need to plan the column size.

- The column size determines how the data is written across the physical disks in the storage pool and also dictates the number of physical disks that need to be added to the storage pool before a Virtual disk can be expand at a later time.
- The more columns (up to 8) the better the overall performance but if you need to add physical disks later it needs to be in multiples of the column size.
- By default, when you create the virtual disk or volume the column size will be automatically determined based on the number of disk available in the storage pool.
- The default setting is used while creating new virtual disk or volume using Server Manager or when you don't specify the column size while using _New-StorageTier_ cmdlet.
- To change the default setting you can run the following commands.

  Run the following command to find the current column size settings.
  ```PowerShell
  Get-ResiliencySetting
  ```

  Example:

  ![Get Resiliency Setting](./media/add-storage/get-resiliency.png)

To change the column size setting run the following command.

For Mirror
```PowerShell
Get-StoragePool DPMPool | Set-ResiliencySetting -Name Mirror -NumberOfColumnsDefault 1
```

For Parity
```PowerShell
Get-StoragePool DPMPool | Set-ResiliencySetting -Name Parity -NumberOfColumnsDefault 3
```


#### Simple Tiered Volume (No Resiliency)

To create the simple tiered volume (no resiliency), follow the steps below.

1. Create SSD Tier by running following command.
   ```PowerShell
   New-StorageTier -StoragePoolFriendlyName DPMPool -FriendlyName SSDTier -MediaType SSD -ResiliencySettingName Simple -NumberOfColumns 1 -PhysicalDiskRedundancy 0 -FaultDomainAwareness PhysicalDisk
   ```

   ```
   PS C:\> New-StorageTier -StoragePoolFriendlyName DPMPool -FriendlyName SSDTier -MediaType SSD -ResiliencySettingName Simple -NumberOfColumns 1 -PhysicalDiskRedundancy 0 -FaultDomainAwareness PhysicalDisk

   FriendlyName TierClass MediaType ResiliencySettingName FaultDomainRedundancy Size FootprintOnPool StorageEfficiency
   ------------ --------- --------- --------------------- --------------------- ---- --------------- -----------------
   SSDTier      Unknown   SSD       Simple                0                     0 B             0 B

   ```

   ![Create SSD Tier](./media/add-storage/create-ssd-tier.png)

2. Create HDD tier by running following command.
   ```PowerShell
   New-StorageTier -StoragePoolFriendlyName DPMPool -FriendlyName HDDTier -MediaType HDD -ResiliencySettingName Simple -NumberOfColumns 1 -PhysicalDiskRedundancy 0 -FaultDomainAwareness PhysicalDisk
   ```

   ```
   PS C:\> New-StorageTier -StoragePoolFriendlyName DPMPool -FriendlyName HDDTier -MediaType HDD -ResiliencySettingName Simple -NumberOfColumns 1 -PhysicalDiskRedundancy 0 -FaultDomainAwareness PhysicalDisk

   FriendlyName TierClass MediaType ResiliencySettingName FaultDomainRedundancy Size FootprintOnPool StorageEfficiency
   ------------ --------- --------- --------------------- --------------------- ---- --------------- -----------------
   HDDTier      Unknown   HDD       Simple                0                     0 B             0 B
   ```

   ![Create HDD Tier](./media/add-storage/create-hdd-tier.png)

   ![HDD Tier Volume](./media/add-storage/hdd-tier-volume.png)

3. Create new volume using the SSD tier and HDD tier created.

   > [!NOTE]
   > You need use storge tier size slightly lower than the actual size at it may exceed the physical capacity of the pool. You can resize (extend) the tier later by reviewing the section titled [Extending tiered volume](#Extending-tiered-volume) section.

   ```PowerShell
   New-Volume -StoragePoolFriendlyName DPMPool -FriendlyName DPMVol -FileSystem ReFS -StorageTierFriendlyNames SSDTier,HDDTier -StorageTierSizes 745GB,14TB
   ```

   ![SSD and HDD Tier](./media/add-storage/ssd-hdd-tier.png)

4. You can verify the performance tier and capacity tier used for the newly created volume by running following command.
   ```PowerShell
   Get-StorageTier
   ```

   ```
   PS C:\> Get-StorageTier

   FriendlyName           TierClass   MediaType ResiliencySettingName FaultDomainRedundancy   Size FootprintOnPool StorageEfficiency
   ------------           ---------   --------- --------------------- ---------------------   ---- --------------- -----------------
   Microsoft_SSD_Template Unknown     SSD       Mirror                1                       0 B             0 B
   DPMVol-HDDTier         Capacity    HDD       Simple                0                      14 TB           14 TB           100.00%
   DPMVol-SSDTier         Performance SSD       Simple                0                     745 GB          745 GB           100.00%
   SSDTier                Unknown     SSD       Simple                0                       0 B             0 B
   HDDTier                Unknown     HDD       Simple                0                       0 B             0 B
   Microsoft_HDD_Template Unknown     HDD       Mirror                1                       0 B             0 B
   ```

   ![Performance Tier](./media/add-storage/performance-tier.png)

The end result as seen in Server Manager. You can see the volume in Windows disk management and is ready to add it to the DPM Storage pool.

![Windows Disk Volume](./media/add-storage/window-disk-volume.png)


### Add volume(s) to DPM storage

Follow these steps:

1. In the DPM Management console \> **Disk Storage** , click **Rescan**.
2. In **Add Disk Storage** , click **Add**.
3. After the volumes are added, you can give them a friendly name.
4. Click **OK** to format the volumes to ReFS, so DPM can use them as MBS.

   ![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-7.png)

## Disable Write Auto Tiering at file system level

We recommend to disable Write Auto Tiering file system level so that the entire performance tier is available for DPM to store ReFS metadata.

> [!NOTE]
> You can skip this step if more than 10% of SSD is used in the performance tier. This can be disabled later if there is a performance degradation in terms of backup speeds.

Follow the steps below to disable write auto caching:

1. Open PowerShell.
2. Run the following command to view current setting:
   ```PowerShell
   fsutil behavior query disableWriteAutoTiering <driveLetter:>

   0 - Enable write auto tiering on the given volume (default)
   1 - Disable write auto tiering on the given volume
   ```
3. Run the following command to disable write caching:
   ```PowerShell
   fsutil behavior set disableWriteAutoTiering <driveLetter:> 1
   ```

   Example:
   ```
   fsutil behavior set disableWriteAutoTiering E: 1
   ```

   ![Disable Write Caching](./media/add-storage/disable-auto-tier.png)

### Extending tiered volume

Before you resize a volume, make sure you have enough capacity in the storage pool to accommodate its new, larger footprint. For example, when resizing a three-way mirror volume from 1 TB to 2 TB, its footprint would grow from 3 TB to 6 TB. For the resize to succeed, you would need at least (6 - 3) = 3 TB of available capacity in the storage pool.

The virtual disk that uses storage tiers, you can resize each tier separately using the **Resize-StorageTier** cmdlet.

### Step 1 – Resize the virtual disk

Get the names of the storage tiers by following the associations from the virtual disk.
```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier | Select FriendlyName
```

Then, for each tier, provide the new size in the **-Size** parameter.

```PowerShell
Get-StorageTier <FriendlyName> | Resize-StorageTier -Size <Size>
```

> [!TIP]
> If your tiers are different physical media types (such as **MediaType = SSD** and **MediaType = HDD** ) you need to ensure you have enough capacity of each media type in the storage pool to accommodate the new, larger footprint of each tier.

When you resize the **StorageTier** (s), the **VirtualDisk** and **Disk** follow automatically and are resized too.

### Step 2 – Resize the partition

Next, resize the partition using the **Resize-Partition** cmdlet. The virtual disk is expected to have two partitions: the first is Reserved and should not be modified; the one you need to resize has **PartitionNumber = 2** and **Type = Basic**.

Provide the new size in the **-Size** parameter. We recommend using the maximum supported size, as shown below.

```PowerShell
# Choose virtual disk
$VirtualDisk = Get-VirtualDisk <FriendlyName>

# Get its partition
$Partition = $VirtualDisk | Get-Disk | Get-Partition | Where PartitionNumber -Eq 2

# Resize to its maximum supported size
$Partition | Resize-Partition -Size ($Partition | Get-PartitionSupportedSize).SizeMax

```
For an existing tiered storage volume, you may want to maximize the storage capacity usage. The below steps will allow you to extent the DPMVOL-HDDParityTier to maximum capacity based on the available free space in the storage pool.

Lets start by showing the current size of the storage tiers and the virtual disk before we resize the storage tier.

**Get-StorageTier**

![Get StorageTier](./media/add-storage/get-storage-tier.png)

**Get-VirtualDisk**

![Get VirtualDisk](./media/add-storage/get-virtual-disk.png)

Get the current sizes of the storage tier (dpmvol-HHDParityTier) we want to resize, then extend it and explain each command.

 ![StorageTier Sizes](./media/add-storage/storage-tier-size.png)

#### Commands used to extend the tiers.

```
Get-StorageTier -friendlyname dpmvol-HDDParityTier (Show Capacity Tier Size)

FriendlyName       TierClass   MediaType     ResiliencySettingName FaultDomainRedundancy Size FootprintOnPool StorageEfficiency
------------       ---------   ---------     --------------------- --------------------- ---- --------------- -----------------
DPMVOL-HDDParityTier Capacity  HDD           Parity                1                     8 TB           12 TB             66.67%
```

```
$sizepartytier=Get-StorageTier -friendlyname dpmvol-HDDParityTier (Save size in bytes as a variable)
$sizepartytier.Size
8796093022208  (This is current size of the tier in bytes)

```

```
Get-StorageTierSupportedSize -friendlyname HDDParityTier -ResiliencySettingName Parity   (Show Tier Max Size in bytes)

SupportedSizes TierSizeMin   TierSizeMax     TierSizeDivisor
-------------- -----------   -----------     ---------------
{}              536870912   1939177734144    536870912

```

```
$sizefree=Get-StorageTierSupportedSize -friendlyname HDDParityTier -ResiliencySettingName Parity (Save free capacity as a variable)

$sizefree.TierSizeMax
1939177734144     (This is available free space in that tier)

```

```
$maxsize=$sizepartytier.size+$sizefree.TierSizeMax    (Calculate the new size)
$maxsize
10735270756352   (This will be the new size in bytes after the resize)

```

```
resize-storagetier -friendlyname dpmvol-HDDParityTier -size $maxsize   (Extend tier to max calculated size and display new size)

Get-StorageTier -friendlyname dpmvol-HDDParityTier

FriendlyName      TierClass   MediaType ResiliencySettingName FaultDomainRedundancy    Size      FootprintOnPool StorageEfficiency
------------      ---------   --------- --------------------- ---------------------    ----      ---------------  -----------------
DPMVOL-HDDParityTier Capacity   HDD      Parity               1                       9.76 TB        14.65 TB            66.67%

```

The result as seen in Server Manager. You can see the volume in Windows disk management along with the new free space added and is ready to be extended.

![Extend Disk Volume](./media/add-storage/extend-disk-volume.png)

**Extend volume using GUI**

![Extend Volume GUI](./media/add-storage/extend-volume-gui.png)

![Extend Virtual Disk](./media/add-storage/extend-virtual-disk.png)

![Related Virtual Disks](./media/add-storage/related-virtual-disks.png)

#### Extend the DPM Volume

You can now extend the volume in Windows Disk Management

![Extend DPM Volume](./media/add-storage/extend-dpm-volume.png)

After extending the volume you can see the new size in Powershell also.

```PowerShell
Get-Volume -friendlyname DPMVOL
```

![Get Volume](./media/add-storage/get-volume.png)
