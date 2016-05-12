---
title: How to migrate a virtual machine in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e9b5c25-679b-44d0-895f-ec3f7ca70699
---
# How to migrate a virtual machine in VMM
This procedure describes how to migrate a virtual machine in [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)]. To perform a migration, you can use any of the following actions:

-   **Run the Migrate VM Wizard**—By using this wizard, you can select a destination virtual machine host for the migration, specify the path that stores the virtual machine files, attach the virtual machine to any of the virtual networks that are found on the selected host, and, if a storage area network \(SAN\) transfer is available, select a network transfer instead.

-   **Run the Migrate Storage Wizard**— By using this wizard, you can move the files for a virtual machine to a different storage location on the same host.

-   **Drag the virtual machine onto a host**—When you drag a virtual machine to a host, [!INCLUDE[vmm12short](Token/vmm12short_md.md)] uses automatic placement to place the virtual machine on the most suitable volume on the host. The placement is based on available space.

-   **Drag the virtual machine onto a host group**—When you drag the virtual machine to a host group, [!INCLUDE[vmm12short](Token/vmm12short_md.md)] uses automatic placement to place the virtual machine on the most suitable host that is available in the host group, which is based on the virtual machine requirements and the host ratings. The virtual machine is placed on the most suitable volume on the host. The placement is based on available space. During automatic placement, the host rating process identifies the most suitable volume on each host. For more information, see [Understanding virtual machine placement and ratings in VMM](Understanding-virtual-machine-placement-and-ratings-in-VMM.md).

Note the following before you begin migration:

-   If a correctly configured SAN is available, [!INCLUDE[vmm12short](Token/vmm12short_md.md)] automatically uses SAN to perform transfers. However, if you use the Migrate Virtual Machine Wizard to perform a transfer, you can override the SAN usage and perform a local area network \(LAN\) transfer.

-   If you migrated a virtual machine that is connected to SAN storage, the virtual machine cannot reconnect to the SAN unless the destination host also has access to that SAN. [!INCLUDE[vmm12short](Token/vmm12short_md.md)] cannot detect if a virtual machine is connected to a SAN or if the destination host is connected to the same SAN, and therefore cannot provide a warning. You must ensure that the new host is configured to enable the virtual machine to reconnect to the SAN before you migrate the virtual machine.

-   One method to convert a VMware ESX virtual machine to a Microsoft Hyper\-V virtual machine is to migrate the virtual machine from ESX Server host to a Hyper\-V host. Before you migrate a virtual machine from a ESX server to a Hyper\-V host, ensure that the source ESX Server host has the **OK** status in [!INCLUDE[vmm12short](Token/vmm12short_md.md)], and that the virtual machine is turned off. If the host has **OK \(Limited\)** status, additional security configuration is required to enable file transfers to the Hyper\-V host. You must provide credentials for the ESX Server host; in addition, if you manage your VMware infrastructure in secure mode, a certificate and public key might be required. Alternatively, you can perform a virtual\-to\-virtual \(V2V\) conversion on the virtual machine files to convert a VMware virtual machine to a Hyper\-V virtual machine. For more information, see [How to use VMM to convert VMware virtual machines to Hyper-V &#40;V2V&#41;](How-to-use-VMM-to-convert-VMware-virtual-machines-to-Hyper-V--V2V-.md).

-   If you change the permissions for a virtual machine through the file system, and then migrate the virtual machine, [!INCLUDE[vmm12short](Token/vmm12short_md.md)] re\-creates the access control list \(ACL\). All changes that were made outside [!INCLUDE[vmm12short](Token/vmm12short_md.md)] will be lost.

-   If you attempt to migrate a virtual machine on a Hyper\-V host soon after you have removed a checkpoint from the virtual machine, the migration might fail. If you attempt a migration before Hyper\-V has finished deleting the checkpoint, the migration fails, and you must repair the virtual machine by using the **Undo** option. To avoid this issue, you can ensure that the checkpoint has been deleted, or you can wait for Hyper\-V to delete it for you. To ensure that a checkpoint has been deleted, do the following:

    1.  In the VMM console, in **Virtual Machines** view, click the virtual machine, and then click **Stop** in the **Actions** pane.

    2.  On the host, open Hyper\-V Manager. Click **Start**, point to **Administrative Tools**, and then click **Hyper\-V Manager**.

    3.  In the **Status** column, **Merge in progress** indicates that the checkpoint has not been deleted. Wait until this operation has finished before you migrate the virtual machine.

## Migrating a virtual machine
Use the following procedure to migrate a virtual machine by using the Migrate VM Wizard.

#### To migrate a virtual machine by using the wizard

1.  In **Virtual Machines** view, browse to the host on which the virtual machine is deployed in the navigation pane.

2.  In the results pane, select the virtual machine, and then click **Migrate Virtual Machine** in the **Actions** pane.

3.  On the **Select Host** wizard page, select the destination host.

4.  To get additional information about the host, select the host, and view the tabs in the details area:

    -   **Details**—Indicates the status of the host, the operating system, and the type and status of virtualization software. Lists the virtual machines on the host.

    -   **Rating Explanation**—Lists the factors that resulted in a 0 star rating.

    -   **SAN Explanation** or **Deployment and Transfer Explanation**—Lists the factors that make a SAN transfer unavailable. In addition, the **Deployment and Transfer Explanation** tab provides an explanation if fast file copy cannot be used. Fast file copy is based on the Windows Offloaded Data Transfers \(ODX\) feature introduced in [!INCLUDE[winblue_server_2](Token/winblue_server_2_md.md)]. For information about ODX, see [Windows Offloaded Data Transfers Overview](http://technet.microsoft.com/library/hh831628.aspx).

5.  In the **Select Path** page, accept the default path, or click **Browse** and browse to the folder in which you want to store the configuration files for the virtual machine, and then click **OK**. Note the following:

    1.  If the target host is a part of a failover cluster that has Cluster Shared Volumes \(CSV\) enabled, you can store the virtual machine on a CSV Logical Units \(LUs\) and associated Number \(LUN\) that is already in use by other highly available virtual machines \(HAVMs\). With CSV, multiple HAVMs can share the same LUN. The migration of one HAVM does not affect others that are sharing the same LUN. [!INCLUDE[vmm12short](Token/vmm12short_md.md)] also supports multiple HAVMs per LUN for VMware environments that are configured with VMware VMFS LUNs.

    2.  If you selected a path other than a default virtual machine path and want to store other virtual machines on that path, select the **Add this path to the list of host default paths** check box to add the path to the default paths on the host.

        If you use a network transfer, you have the option to specify separate storage locations for each virtual hard disk \(.vhd or .vhdx\) file for the virtual machine. By default, all .vhd or .vhdx files are stored in the same location that is specified for the virtual machine.

    3.  If SAN transfers are enabled for this deployment, the virtual machine by default is transferred to the host over the SAN. If you do not want to perform a SAN transfer, select **Transfer over the network even if a SAN transfer is available**. If SAN transfers are not available for this deployment, that option is not available.

6.  On the **Select Networks** wizard page, modify the networks, and then attach them to **None** or to any of the virtual networks that are found on the selected host.

    > [!NOTE]
    > Networks area lists each of the virtual network adapters that are currently attached to the virtual machine. Network adapters default to **None** if you selected **None** in the hardware configuration or to the best matching virtual network according to the network matching rules.

7.  On the **Select Virtual SAN** wizard page, select the applicable virtual SANs from the drop\-down list for each listed virtual HBA. When you have finished, click **Next**.

8.  On the **Summary** wizard page, review your settings. To change settings, click **Previous**.

    To start the virtual machine after you deployed it, select the **Start the virtual machine immediately after deploying it to the host** check box.

    > [!NOTE]
    > Click **View Script** to view the Windows PowerShell cmdlets that perform the migration.

9. To begin deploying the virtual machine, click **Move**.

    To review the progress and results of the operation, open the **Jobs** workspace. By default, the workspace opens when the wizard closes. To open this workspace at any time, click **Jobs** on the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] console toolbar.

Use the following procedure to migrate a virtual machine by using a drag\-and\-drop operation.

#### To migrate a virtual machine by using a drag\-and\-drop operation

1.  In **Virtual Machines** view, browse to the virtual machine's current host in the navigation pane.

2.  In the results pane, click the virtual machine and, while you hold down the mouse button, drag the virtual machine to either the host of choice or to the host group of choice in the navigation pane.

3.  When you release the mouse button, the system attempts to migrate the virtual machine by using one of the following methods:

    -   If you dragged the virtual machine to a host, the system evaluates the host's suitability for the virtual machine and attempts to migrate the virtual machine if the host is found suitable.

    -   If you dragged the virtual machine to a host group, the system rates each host in the host group and attempts to migrate the virtual machine to the most suitable of those hosts. For the migration to succeed, a virtual machine path must be configured on the host for the recommended volume.

> [!NOTE]
> If you encounter difficulties using drag\-and\-drop, log out of [!INCLUDE[vmm12short](Token/vmm12short_md.md)], and then log back in and try again. Also try restarting the virtual machine and then try again.

## See Also
[Overview: migrating virtual machines and storage](Overview--migrating-virtual-machines-and-storage.md)
[Migrating virtual machines and storage in VMM](Migrating-virtual-machines-and-storage-in-VMM.md)
[Managing virtual machines with VMM](Managing-virtual-machines-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


