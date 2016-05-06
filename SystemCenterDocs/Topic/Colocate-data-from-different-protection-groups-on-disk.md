---
title: Colocate data from different protection groups on disk
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e76c5e69-90c5-4d2c-aa13-c96d78c8c418
---
# Colocate data from different protection groups on disk
Colocation allows you to locate data from different protection groups on the same disk or tape storage. Since [!INCLUDE[dpm2012long](../Token/dpm2012long_md.md)] requires you must to have one replica volume and one recovery point volume per protected data source, colocation enables you to have multiple data sources mapping on a single replica and recovery point volume. This enables you to store data more efficiently.

Note that you can only collocate data on volumes created using the storage pool disks. You can’t collocate data on custom volumes.

[!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] supports co\-location for the following data sources:

-   Hyper\-V virtual machines

-   Client computers

-   SQL Server databases

Note the following:

-   You enable colocation when you configure a protection group. If DPM supports colocation for the data source you are protecting, a checkbox allowing you to enable colocation appears on the Review Disk Allocation page of the Create New Protection Group Wizard.

-   Colocated data sources share a volume, and recovery points. Removing the recovery point for any one of the co\-located data sources, will mean losing recovery points of the other data sources sharing this volume.

-   You can look at the size allocated to each volume and the number of data sources co\-located on each volume by clicking **Modify** on the Review Disk Allocation Page. Each row in the table represents one volume. Click **Collocated Protection** to see the data sources that share that volume.

## Colocating Hyper\-V data
[!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] increases the scale supported for Hyper\-V virtual machines. The 250 GB colocation size in [!INCLUDE[sc2012](../Token/sc2012_md.md)] is not sufficient when you protect large scale deployments of Hyper\-V virtual machines. For example, if the virtual machine is 100 GB in size, DPM will be able to put one virtual machine in a volume. [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] supports protecting up to 800 virtual machines on one DPM server. This requires increasing the colocation limits to 450 GB. You can do this by editing the following registry keys:

|||
|-|-|
|Key|HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Microsoft Data Protection Manager\\Collocation\\HyperV|
|Value|CollocatedReplicaSize|
|Data|**Enter value in bytes**|
|Type|DWORD|

|||
|-|-|
|Key|HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Microsoft Data Protection Manager\\Collocation\\HyperV|
|Value|DSCollocationFactor|
|Data|**Enter a number between 1 and 8**<br /><br />The recommended value is 3.|
|Type|DWORD|

Collocation will reduce the number of volumes that will be required on DPM server to support the scale of 800 Hyper V data sources.

## Colocating data that isn’t currently colocated
When you enable colocation for a data source that isn’t currently colocated, DPM first tries to add the inactive data source to an existing replica volume that has the required space for reprotecting the inactive data source. If DPM does not find space on an existing replica volume, it creates a new volume and then copies data from the inactive replica to the selected replica volume in the destination protection group.

After copying the data to the destination protection group, the member data source at the destination protection group is marked as Inconsistent and a consistency check is recommended.

The recovery points associated with the old replica will be deleted according to the retention range of the new protection group. After the last recovery point has been pruned, the old replica volume will be deleted.

## Removing colocation
When you remove colocation from a data source, a new volume will be created and the data source will be added to it. If the volume has other data sources on it, all of which are inactive, only then the volume will be reused for one of the data sources. The old recovery points will be pruned as per the data source with the longest retention period.

The following examples take you through various scenarios to explain this behavior.

**Scenario 1:** Assume data source DS1 was protected on a co\-located protection group PG1 that had a retention range of 3 days. If you were to remove DS1 from PG1 and re\-protect it as a part of another protection group PG2 that has a retention range of 5 days, at the time of pruning the recovery points of PG1, the retention range of PG2 will take precedence as long as there are recovery points for DS1 on the recovery point volume.

**Scenario 2:** Assume protection group PG1 with retention range of 3 days has five data sources DS1 to DS5. Of these data sources DS1 is moved to PG2 that has a retention range of 4 days and DS3 is moved to PG3 that has a retention range of 5 days. Pruning of the recovery points for PG1 will follow the retention range of PG3 until there are no more recovery points of DS3 left. Then it will follow the retention range of PG2, if there are any recovery points of DS1 remaining. Finally when the recovery points of DS1 and DS3 are all pruned off, the retention range schedule will revert to PG1’s schedule.

## Stop protecting colocated data
You can stop protection for co\-located data sources like you would for any data source using the Modify Protection Group Wizard and removing the data source from the protection group.

-   If you stop protection with the **Retain Data** option, DPM will retain the recovery points of the selected data sources as long as the retention range of the data source is not exceeded. After the retention range has been exceeded, DPM will remove the recovery points as part of its daily pruning job. However, the replica of that data source will be preserved until the replica volume is eliminated or the data sources that coexisted with the deleted data source are deleted from protection.

-   If you re\-protect the data source that you removed from a protection group in another protection group, the pruning schedule will depend on which of the protection groups has a longer retention range.

-   If you stop protection without **Retain Data**, DPM will remove the records of that data source from the DPMDB. The replica volume space that was used by the replica of those data sources will be made available for co\-locating more data sources in the same protection group.

-   If you try to restore a database that was once co\-located and then later removed, the status of the replica will show as **Inconsistent**. To handle this situation, run a consistency check on the replica. This will allow you to proceed with the recovery.

