---
ms.assetid: c4e5dc66-173a-4e8a-bace-a00a0d8e704c
title: Run a live migration in the VMM fabric
description: This article describes how to run a live migration in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/07/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---


# Run a live migration in the VMM fabric




This article describes how to run a live migration of virtual machines (VMs) or VM storage, in the System Center - Virtual Machine Manager (VMM) fabric. VMM provides live migration support between standalone Hyper-V hosts, or between cluster hosts that have live migration enabled. [Learn more](migrate.md#live-migration).


## Migrate a VM between two standalone hosts

Migrate a virtual machine from one stand-alone Hyper-V host to another stand-alone Hyper-V host. The VM configuration files and virtual hard disk must be located on an SMB 3.0 file share.

1.  In **VMs and Services** > **All Hosts**, click the standalone source host from which you want to migrate.
2.  Click the host and in **VMs**, click the running VM that you want to migrate. Start the machine if it's not running.
3.  In **Virtual Machine**, click **Migrate Virtual Machine** to start the Migrate Virtual Machine Wizard.
4.  In **Select Host**, review the destination hosts and their associated transfer types. The **Live** transfer type appears if both hosts are configured to connect to the same SMB 3.0 file share.
5.  Click the destination host where the transfer type is **Live**, and then click **Next**.
6.  In **Summary**, click **Move**. To track the job status, open the **Jobs** workspace.
7. To verify that the virtual machine was migrated, check the **VMs** list on the destination host to make sure the VM is running.


## Migrate a VM between clusters

Migrate a VM between clusters. Note that the VM temporarily loses its high availability status. Therefore, a host failure during the migration causes the virtual machine to become unavailable. For live migration between clusters, you should use SMB 3.0 file shares as the storage location. Because the storage does not have to be migrated, the time in which high availability status cannot be guaranteed is very short.

1.  In **VMs and Services** > **All Hosts**, click the cluster node from which you want to migrate.
2.  In **VMs**, click the running VM that you want to migrate. Start the machine if it's not running.
3.  In **Virtual Machine**, click **Migrate Virtual Machine** to start the Migrate Virtual Machine Wizard.
4.  In **Select Host**, review the destination hosts and their associated transfer types. The **Live** transfer type is available for any destination cluster nodes that are configured to connect to the same SMB 3.0 file share on which the VM was originally created.
5.  Click a node on a different cluster, and then click **Next**.
6.  In **Summary**, click **Move**. To track the job status, open the **Jobs** workspace.
7. To verify that the virtual machine was migrated, check the **VMs** list on the destination node to make sure the VM is running.

## Migrate storage between two locations on a standalone host

> [!NOTE]
> You cannot live migrate storage for a shared VHDX file.  You can move the other VM files and perform normal live migration.

> To move the shared VHDX file to another location, you must shut down the VMs and then move the file.

You can run a live migration of VM storage between locations on standalone hosts. You can move the entire virtual machine, which includes virtual hard disks (VHDs) and configuration information, or move only specific VHDs to a different location.

1.  In **VMs and Services** > **All Hosts**, click the standalone host where the VM is located.
2.  In **VMs**, click the running VM for which you want to migrate storage. Start the machine if it's not running.
3.  In **Virtual Machine**, click **Migrate Storage** to start the Migrate Virtual Machine Wizard.
4.  In **Select Path** >  **Storage location**, click one of the default storage locations on the host. Or click **Browse** to view all possible storage destinations. Click the destination SMB 3.0 file share or location on the local hard disk, and then click **OK**.

    If you specify an SMB 3.0 file share in the **Storage location** list, ensure that you use the fully qualified domain name (FQDN) of the destination server in the share path. For example, instead of *\\\fileserver1\smbshare*, use *\\\fileserver1.contoso.com\smbshare*.

5.  Optionally, select **Add this path to the list of default storage locations on the host**, and then click **Next**.
6.  On the **Summary** page, click **Move**. Track progress in **Jobs**.


## Run live migrations concurrently

You can run live migration on multiple VMs so that two migrations occur at the same time on the same host. Note that:

- You can't select multiple VMs for a live migration. You need to manually start each migration.
- You can specify how many concurrent migrations to run. The default setting is two, which is the number of simultaneous live migration and storage migrations that are enabled in Hyper-V. For example, a host can participate in one outgoing live migration plus one incoming, two outgoing live migrations, or two incoming live migrations.
- Live migrations and live storage migrations are independent. You can perform two live migrations and two live storage migrations simultaneously. VMM considers live virtual machine and storage migration (live VSM) as one live migration and one storage migration.
- You can view concurrent migrations in progress in Hyper-V Manager > **Actions** > **Hyper-V Settings**> **Server** >  **Live Migrations** and **Storage Migrations**. In **Jobs**, verify that the migrations occur simultaneously.


## Improve live migration speed

On Hyper-V hosts, you can increase live migration speed using compression, by using SMB as the transport, or both. The compression method uses algorithms that reduce the data that is transmitted over the wire. The SMB method can allow for faster data transfer.

By default, faster live migration is enabled to use the compression method. You can disable, enable, or change the method of faster live migration by changing the live storage migration settings, either at the Hyper-V host level, or for each live migration instance.

Change live migration settings as follows:

1.  In Hyper-V Manager click  **Actions** > **Hyper-V Settings** >  **Server** > **Live Migration**, and then click **Advanced Features**.
2.  In **Migration settings** > **Live migration settings**, do one of the following:

    -   To disable faster live migration, click **Standard live migration**.
    -   To use compression for faster live migration, click **Use compression**.
    -   To use SMB for faster live migration, click **Use SMB as Transport**.
