---
ms.assetid: 2f7417df-02a3-4ab8-abb0-dcb2c421eed1
title: Migrate a virtual machine in the VMM fabric
description: This article describes how to migrate a VM in VMM
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Migrate a virtual machine in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager


This article describes how to migrate a VM in System Center 2016 - Virtual Machine Manager (VMM)

To perform a migration, you can do any of the following:


-   **Run the Migrate VM Wizard**: By using this wizard, you can select a destination virtual machine host for the migration, specify the path that stores the virtual machine files, attach the virtual machine to any of the virtual networks that are found on the selected host, and, if a storage area network (SAN) transfer is available, select a network transfer instead.

-   **Drag the virtual machine onto a host**: When you drag a virtual machine to a host, VMM uses automatic placement to place the virtual machine on the most suitable volume on the host. The placement is based on available space.

-   **Drag the virtual machine onto a host group**: When you drag the virtual machine to a host group, VMM uses automatic placement to place the virtual machine on the most suitable host that is available in the host group, which is based on the virtual machine requirements and the host ratings. The virtual machine is placed on the most suitable volume on the host. The placement is based on available space. During automatic placement, the [host rating process](manage-vm-overview.md#host-ratings) identifies the most suitable volume on each host.

Note the following before you begin migration:

-   If a correctly configured SAN is available, VMM automatically uses SAN to perform transfers. However, if you use the Migrate Virtual Machine Wizard to perform a transfer, you can override the SAN usage and perform a local area network (LAN) transfer.
-   If you migrated a virtual machine that is connected to SAN storage, the virtual machine cannot reconnect to the SAN unless the destination host also has access to that SAN. VMM cannot detect if a virtual machine is connected to a SAN or if the destination host is connected to the same SAN, and therefore cannot provide a warning. You must ensure that the new host is configured to enable the virtual machine to reconnect to the SAN before you migrate the virtual machine.
-   If you change the permissions for a virtual machine through the file system, and then migrate the virtual machine, VMM re-creates the access control list (ACL). All changes that were made outside VMM will be lost.

-   If you attempt to migrate a virtual machine on a Hyper-V host soon after you have removed a checkpoint from the virtual machine, the migration might fail. If you attempt a migration before Hyper-V has finished deleting the checkpoint, the migration fails, and you must repair the virtual machine by using the **Undo** option. To avoid this issue, you can ensure that the checkpoint has been deleted, or you can wait for Hyper-V to delete it for you. Verify deletion as follows:

    1.  In **Virtual Machines** click the virtual machine >  **Actions** > **Stop**.
    2. In Hyper-V Manage, **Status** > **Merge in progress** indicates that the checkpoint has not been deleted. Wait until this operation has finished before you migrate the virtual machine.

## Migrate a virtual machine with the wizard

1. In **Virtual Machines** view, browse to the host, select the VM, and in **Actions** click **Migrate Virtual Machine**.
2. In **Select Host** , select the destination host. You can check the tabs for more details about the host.
	- **Details** — Indicates the status of the host, the operating system, and the type and status of virtualization software. Lists the virtual machines on the host.
	- **Rating Explanation** — Lists the factors that resulted in a 0 star rating.
	- **SAN Explanation or Deployment and Transfer Explanation** — Lists the factors that make a SAN transfer unavailable. In addition, as of System Center 2016 Virtual Machine Manager, the Deployment and Transfer Explanation tab provides an explanation if fast file copy cannot be used. Fast file copy is a feature that was introduced in VMM, based on the Windows Offloaded Data Transfers (ODX) feature introduced in Windows Server 2012 R2. For information about ODX, see [Windows Offloaded Data Transfers Overview](https://technet.microsoft.com/en-us/library/hh831375(v=ws.11).aspx).
	
    	**Note: The Fast file copy feature is not utilized when migrating a VM from Host to Library.** 
	 
3. In **Select Path** page, accept the default path, or click **Browse** and browse to the folder in which you want to store the configuration files for the virtual machine, and then click **OK**. Note the following:

    - If the target host is a part of a failover cluster that has Cluster Shared Volumes (CSV) enabled, you can store the virtual machine on a CSV Logical Units (LUs) and associated Number (LUN) that is already in use by other highly available virtual machines (HAVMs). With CSV, multiple HAVMs can share the same LUN. The migration of one HAVM does not affect others that are sharing the same LUN. VMM also supports multiple HAVMs per LUN for VMware environments that are configured with VMware VMFS LUNs.
    - If you selected a path other than a default virtual machine path and want to store other virtual machines on that path, select the **Add this path to the list of host default paths** check box to add the path to the default paths on the host.
    - If you use a network transfer, you have the option to specify separate storage locations for each virtual hard disk (.vhd or .vhdx) file for the virtual machine. By default, all .vhd or .vhdx files are stored in the same location that is specified for the virtual machine.
    - If SAN transfers are enabled for this deployment, the virtual machine by default is transferred to the host over the SAN. If you do not want to perform a SAN transfer, select **Transfer over the network even if a SAN transfer is available**. If SAN transfers are not available for this deployment, that option is not available.

4.  In **Select Networks** , modify the networks, and then attach them to **None** or to any of the virtual networks that are found on the selected host. The networks area lists each of the virtual network adapters that are currently attached to the virtual machine. Network adapters default to **None** (if you selected **None** in the hardware configuration), or to the best matching virtual network according to the network matching rules.
5.  In **Select Virtual SAN**, select the applicable virtual SANs from the drop-down list for each listed virtual HBA. Then click **Next**.
6.  In **Summary**, review your settings. To start the VM after deployment click **Start the virtual machine immediately after deploying it to the host**. Click **View Script** to view the Windows PowerShell cmdlets that perform the migration.
7. To start migration, click **Move**. Review progress in **Jobs**.


## Migrate a VM with drag and drop

1.  In **Virtual Machines**, browse to the virtual machine's current host in the navigation pane.
2.  Click the VM and, while you hold down the mouse button, drag the virtual machine to either the host of choice or to the host group of choice in the navigation pane.
3.  When you release the mouse button, the system attempts to migrate the virtual machine by using one of the following methods:

    -   If you dragged the virtual machine to a host, the system evaluates the host's suitability for the virtual machine and attempts to migrate the virtual machine if the host is found suitable.
    -   If you dragged the virtual machine to a host group, the system rates each host in the host group and attempts to migrate the virtual machine to the most suitable of those hosts. For the migration to succeed, a virtual machine path must be configured on the host for the recommended volume.

If you encounter difficulties using drag-and-drop, log out of VMM, and then log back in and try again. You can also try restarting the virtual machine, and then try again.
