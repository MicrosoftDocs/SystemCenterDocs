---
title: View or modify storage pool settings
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 962f9a2d-df9e-45c7-a2be-ae1988ecc35e
---
# View or modify storage pool settings
In the **Management** view of the DPM Administrator Console, you can review and modify storage pool settings.

### View storage pool settings

1.  In the **Disks** workspace of the DPM Administrator Console, the total capacity and disk space allocated for all disks in the storage pool is displayed, and you can review the following information for each disk in the storage pool:

    -   Name

    -   Status: Healthy, unhealthy, or missing

    -   Used space: Space allocated for protection

    -   Unallocated space: Amount of unallocated space

    -   Protected data sources on this disk: A list of the data sources protected on the disk

2.  DPM automatically detects changes to the disk configuration in the storage pool but you can also manually rescan for changes by clicking **Rescan** in the **Actions** pane.

## View or modify disk allocations
When you create a protection group, DPM recommends and allocates disk space for your protection group in the storage pool. This allocated is based on the retention range, work load type and the size of the data to be protected. Generally, the recommended allocations provide sufficient storage for at least a couple of weeks of recovery points.We recommend that you accept these disk allocations for the protection group unless you’re sure they don’t meet your requirements. If you change the settings, you might get fewer recovery points than you wanted or DPM might allocate more disk space than is needed. If you do want to change the settings note the following:

-   Use the [Storage Calculators for DPM](http://go.microsoft.com/fwlink/?LinkID=180658) to help you figure out storage capacity requirements based on a set of input factors.

-   With data co\-location enabled, DPM will allocate fixed size volumes in the storage pool. For more information, see [Colocate data from different protection groups on disk](../Topic/Colocate-data-from-different-protection-groups-on-disk.md).

-   If you’re protecting only a subset of the data on the protected volume, you can calculate the size of the protected data so that DPM can adjust its recommendations for disk allocation. To compute the disk allocation using the size of the data on the protected volume, in the **ModifyDisk Allocation** dialog box, click **Calculate**.

-   If the data on the protected volume outgrows the initial allocations, DPM can try to automatically grow the volume by 25% if the option **Automatic grow the volumes** in the **Review Disk Allocation** page of the Create New Protection Group wizard is selected. If the auto\-grow operation fails, or if the option **Automatic grow the volumes** is not selected, DPM generates a “Recovery point volume threshold exceeded” or “Replica disk threshold exceeded” alert and provides guidance for increasing disk allocations appropriately.

-   To get more information about disk usage for a protection group, you can schedule and view a [Disk utilization reports \[DPM2012\_Web\]](assetId:///98bb5e67-2a5d-4cbe-9014-b2ee61a7685f).

-   Use the following table to help you understand disk allocation options.

    |Protection feature|Disk allocation options|Location|
    |----------------------|---------------------------|------------|
    |Replica volume|You can increase, but not decrease, the allocated disk space for the replicas.|DPM storage pool|
    |Recovery point volume|You can increase or decrease, the allocated space for recovery points.|DPM storage pool|
    |Change journal|You can increase, but not decrease, the allocated disk space for the change journal.|Protected volume on the file server or workstation|
    |Custom volume|DPM does not manage custom volumes.|Any disk attached to the DPM server|

If you still want to modify disk allocation settings do the following:

1.  In DPM Administrator Console, go to the **Protection** view.

2.  In the display pane, select the protection group for which you want to modify disk allocation.

3.  Click **Modify disk allocation**.

4.  On the **DPM Server** tab, type the amount of space you want to allocate for **Replica Volume** and for **Recovery Point Volume**, and click **OK**.

    > [!NOTE]
    > When creating a protection group, DPM helps to allocate optimal space. Click **Calculate** to have DPM allocate space based on a formula specific to a data source type. If you do not click **Calculate**, DPM allocates approximately two times the volume size for the replicas and recovery points.
    > 
    > Click **Shrink** to calculate the thresholds to which the recovery point volume size can shrink.

5.  If you are modifying disk allocation on a protected computer, on the **Protected Computer** tab, type the amount of space you want to allocate in the **Space Allocated** column, and click **OK**.

6.  After reviewing the disk allocation changes, click **OK**. Note that:

    -   If data co\-location is enabled on disk, click **Collocated Protection** to view co\-located replica details for each co\-located data source.

    -   The default disk space is 300 MB. You can increase, but not decrease, the space allocated for the change journal.

