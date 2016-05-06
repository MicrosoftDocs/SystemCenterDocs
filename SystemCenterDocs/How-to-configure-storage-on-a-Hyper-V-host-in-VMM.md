---
title: How to configure storage on a Hyper-V host in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fd77880c-3a53-4c7d-980f-ef392909bff9
---
# How to configure storage on a Hyper-V host in VMM
You can use the following procedures to configure storage on a Hyper\-V host that is already under management in [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)]. These procedures all use Hyper\-V host properties to configure the storage for a specific host:

-   [Creating a logical unit and assigning it to a host](./How-to-configure-storage-on-a-Hyper-V-host-in-VMM.md#BKMK_create_assign)

-   [Assigning a logical unit to a host](./How-to-configure-storage-on-a-Hyper-V-host-in-VMM.md#BKMK_assignLU)

-   [Removing a logical unit from a host](./How-to-configure-storage-on-a-Hyper-V-host-in-VMM.md#BKMK_remove)

-   [Creating an iSCSI session on a host](./How-to-configure-storage-on-a-Hyper-V-host-in-VMM.md#BKMK_iSCSI)

> [!IMPORTANT]
> The storage prerequisites for this topic are almost the same as those for hosts that you are preparing to bring together into a cluster. The one exception is that Multipath I\/O might not be necessary, depending on your configuration. Therefore, for prerequisites, see two sections in "Prerequisites: creating a cluster in VMM from existing servers": 
> [Host cluster prerequisites: Fibre Channel or iSCSI storage arrays](./Prerequisites--creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md#BKMK_arrays) \(although Multipath I\/O might not be necessary\)
> [Host cluster prerequisites: storage allocation and configuration](./Prerequisites--creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md#BKMK_storage_allocation)

**Account requirements** To complete these procedures, you must be a member of the Administrator user role or a member of the Delegated Administrator user role where the management scope includes the host group where the Hyper\-V host is located.

## <a name="BKMK_create_assign"></a>Creating a logical unit and assigning it to a host

#### To use Hyper\-V host properties to create a logical unit and assign it to the host

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers** > **All Hosts**.

3.  In the **Hosts** pane, right\-click the host that you want to configure, and then click **Properties**.

4.  In the *Host Name* **Properties** dialog box, click the **Storage** tab.

5.  To create a logical unit, follow these steps:

    1.  On the toolbar, next to **Disk**, click **Add**.

    2.  Next to the **Logical unit** list, click **Create Logical Unit**.

        The Create Logical Unit dialog box opens.

    3.  In the **Storage pool** list, click the desired storage pool.

    4.  In the **Name** box, enter a name for the logical unit. Use only alphanumeric characters.

    5.  Optionally, in the **Description** box, enter a description for the logical unit.

    6.  In the **Size \(GB\)** box, enter the size of the logical unit, in gigabytes.

    7.  When you are finished, click **OK**.

    The new logical unit is listed in the **Logical unit** list. At this point, the logical unit is created, but not assigned to any host. To assign the logical unit to the host, continue with this procedure.

6.  In the **Logical unit** list, verify that the logical unit that you just created is selected.

7.  In the **Format new disk** area, if you want to format the disk, select the **Format this volume as NTFS volume with the following settings** check box, and then do the following:

    1.  In the **Partition style** list, click **MBR** \(Master Boot Record\) or **GPT** \(GUID Partition Table\).

    2.  In the **Volume label** box, enter a volume label, for example **Finance Data**.

    3.  In the **Allocation unit size** list, either accept the default, or click a specific allocation unit size. \(Note that the values 512, 1024, 2048, 4096 and 8192 are in bytes.\)

    4.  Select or clear the **Quick format** check box. By default, the check box is selected. To prevent data loss, quick format formats the disk only if the disk is unformatted.

    5.  If desired, select the **Force format even if a file system is found** check box. By default, the check box is clear.

        > [!WARNING]
        > If you select this option, any existing data on the volume will be overwritten.

8.  In the **Mount point** area, select one of the following options:

    -   **Assign the following drive letter** \(the default\). If you select this option, click the desired drive letter.

    -   **Mount in the following empty NTFS folder**. If you select this option, click **Browse**, and then select the empty destination folder.

    -   **Do not assign a drive letter or drive path**

9. When you are finished, click **OK**.

    [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] registers the storage logical unit to the host and mounts the storage disk. To view the associated job information, open the **Jobs** workspace.

10. To verify that the logical unit was assigned, view the information on the **Storage** tab in the *Host Name* **Properties** dialog box. The newly assigned logical unit appears under **Disk**. Click the new disk to view the disk details.

    > [!TIP]
    > If the **Array** field is populated in the disk details, this indicates that the storage array is under [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management.

11. To perform further configuration of the disk, open Disk Management on the host. \(To open Disk Management, click **Start**, type **diskmgmt.msc** in the search box, and then press ENTER.\)

    The new disk appears in the list of disks as a basic disk. If you chose to format the disk, the disk is already formatted and online. You can right\-click the disk to see the available options, such as **Format** and **Change Drive Letter and Paths**.

## <a name="BKMK_assignLU"></a>Assigning a logical unit to a host

#### To use Hyper\-V host properties to assign a logical unit to a host

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers** > **All Hosts**.

3.  In the **Hosts** pane, right\-click the host that you want to configure, and then click **Properties**.

4.  In the *Host Name* **Properties** dialog box, click the **Storage** tab.

5.  To assign an existing logical unit to the host, on the toolbar, next to **Disk**, click **Add**.

6.  In the **Logical unit** list, click the logical unit that you want to assign to the host.

7.  Configure the format and mount point options, and then click **OK** to assign the logical unit to the host. For more information about these options and how to verify that the logical unit was assigned, see steps 7 through 11 of [Creating a logical unit and assigning it to a host](./How-to-configure-storage-on-a-Hyper-V-host-in-VMM.md#BKMK_create_assign), earlier in this topic.

    > [!NOTE]
    > If the logical unit has existing data, and you do not use the **Force Format** option, the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] job to assign the logical unit will complete with a warning. [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] assigns the logical unit to the host. You can format the disk later.

## <a name="BKMK_remove"></a>Removing a logical unit from a host

#### To remove a logical unit from a host

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers** > **All Hosts**.

3.  In the **Hosts** pane, right\-click the host that you want to configure, and then click **Properties**.

4.  In the *Host Name* **Properties** dialog box, click the **Storage** tab.

5.  Under **Disk**, click the logical unit that you want to remove, and then on the toolbar, click **Remove**.

    > [!NOTE]
    > For the Remove button to be enabled, the logical unit must be under [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management.

6.  Review the warning message, and then click **Yes** to remove the logical unit.

    > [!NOTE]
    > When you remove a logical unit, the volume and any data on the logical unit are not modified.

7.  Click **OK** to commit the changes.

    [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] unregisters the logical unit from the host. To view the associated job information, open the **Jobs** workspace.

## <a name="BKMK_iSCSI"></a>Creating an iSCSI session on a host

#### To create an iSCSI session on a host

1.  On the target host, in the Services snap\-in, make sure that the Microsoft iSCSI Initiator Service is started and set to Automatic.

2.  In the VMM console, open the **Fabric** workspace.

3.  In the **Fabric** pane, expand **Servers** > **All Hosts**.

4.  In the **Hosts** pane, right\-click the host that you want to configure, and then click **Properties**.

5.  In the *Host Name* **Properties** dialog box, click the **Storage** tab.

6.  Under **iSCSI Arrays**, see if the storage array is already listed. If it is not, on the toolbar, next to **iSCSI Array**, click **Add**.

    The Create New iSCSI Session dialog box opens.

7.  In the **Array** list, click the desired iSCSI storage array.

8.  To create an iSCSI session with the default settings, click **Create**.

    To create an iSCSI session with customized settings, select the **Use advanced settings** check box, and then do the following:

    1.  In the **Target portal** list, click the IP address and port number for the connection to the storage array.

    2.  In the **Target name** list, click the iSCSI Qualified Name \(IQN\) of the storage array.

    3.  In the **Initiator IP** list, click the IP address of the network card on the host that you want to use. The associated logical networks are also listed.

    4.  When you are finished, click **Create**.

    The array that you added appears under **iSCSI Arrays**. Click the array to view more details.

9. To create additional iSCSI sessions to the array, click **Create session**. In the **Create New iSCSI Session** dialog box, do either of the following:

    1.  Click **Create** to have [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] automatically determine the connection information. [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] creates the iSCSI session by matching the host initiator IP address subnets with the iSCSI target portal IP subnets.

    2.  Click **Use advanced settings** to manually select the target portal, target name and the initiator IP address, and then click **Create**.

## See Also
[Configuring Hyper-V host properties in VMM](./Configuring-Hyper-V-host-properties-in-VMM.md)
[Managing storage resources and capacity with VMM](./Managing-storage-resources-and-capacity-with-VMM.md)
[How to configure storage on a Hyper-V host cluster in VMM](./How-to-configure-storage-on-a-Hyper-V-host-cluster-in-VMM.md)
[Managing Hyper-V hosts and host clusters with VMM](./Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)
[Managing hosts and host clusters with VMM](./Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](./Managing-fabric-resources-with-VMM.md)


