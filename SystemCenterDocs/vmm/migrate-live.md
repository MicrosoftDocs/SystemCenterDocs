---
ms.assetid: c4e5dc66-173a-4e8a-bace-a00a0d8e704c
title: Run a live migration in the VMM fabric
description: This article describes how to run a live migration in the VMM fabric
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 08/30/2024
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy23, engagement-fy24
---


# Run a live migration in the VMM fabric




This article describes how to run a live migration of virtual machines (VMs) or VM storage in the System Center Virtual Machine Manager (VMM) fabric. VMM provides live migration support between standalone Hyper-V hosts or between cluster hosts that have live migration enabled. [Learn more](migrate.md#live-migration).

## Migrate a VM between two standalone hosts

To migrate a virtual machine from one standalone Hyper-V host to another standalone Hyper-V host, the VM configuration files and virtual hard disk must be located on an SMB 3.0 file share.

1.  In **VMs and Services** > **All Hosts**, select the standalone source host from which you want to migrate.
2.  Select the host and in **VMs**, select the running VM that you want to migrate. Start the machine if it's not running.
3.  In **Virtual Machine**, select **Migrate Virtual Machine** to start the Migrate Virtual Machine Wizard.
4.  In **Select Host**, review the destination hosts and their associated transfer types. The **Live** transfer type appears if both hosts are configured to connect to the same SMB 3.0 file share.
5.  Select the destination host where the transfer type is **Live** and select **Next**.
6.  In **Summary**, select **Move**. To track the job status, open the **Jobs** workspace.
7. To verify that the virtual machine was migrated, check the **VMs** list on the destination host to ensure the VM is running.


## Migrate a VM between clusters
You can migrate a VM between clusters using shared storage or with no shared infrastructure.

Select the required tab for steps for live migration with shared storage or with no shared infrastructure:

# [Live migration with shared storage](#tab/SharedStorage)

When you migrate a VM between clusters, note that the VM temporarily loses its high availability status. Therefore, a host failure during the migration causes the virtual machine to become unavailable. For live migration with shared storage, you must use SMB 3.0 file shares as the storage location. As the storage doesn't have to be migrated, the time in which high availability status can't be guaranteed is short.

1.  In **VMs and Services** > **All Hosts**, select the cluster node from which you want to migrate.
2.  In **VMs**, select the running VM that you want to migrate. Start the machine if it's not running.
3.  In **Virtual Machine**, select **Migrate Virtual Machine** to start the Migrate Virtual Machine Wizard.
4.  In **Select Host**, review the destination hosts and their associated transfer types. The **Live** transfer type is available for any destination cluster nodes that are configured to connect to the same SMB 3.0 file share on which the VM was originally created.
5.  Select a node on a different cluster and select **Next**.
6.  In **Summary**, select **Move**. To track the job status, open the **Jobs** workspace.
7. To verify that the virtual machine was migrated, check the **VMs** list on the destination node to ensure the VM is running.


>[!NOTE]
> When you run live migration on VMs from an older cluster version to a newer version, if the [*Msvm_CompatibilityVector*](/windows/win32/hyperv_v2/msvm-compatibilityvector) value isn't updated, migration within the new cluster will be blocked.
>
>To fix this issue, restart the VM. VM restart updates the *Msvm_CompatibilityVector* values according to the new cluster version.

# [Live migration with no shared infrastructure](#tab/NoSharedInfra)

When you migrate a VM between clusters, note that the VM temporarily loses its high availability status. For live migration with no shared infrastructure, you must use two different SMB 3.0 shares. First, synchronize the source and destination virtual hard disks completely, then initiate the live migration for the virtual machine. [Read more](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831435(v=ws.11)) about virtual machine storage migration.

Follow these steps:

1.  In **VMs and Services** > **All Hosts**, select the cluster node from which you want to migrate.
2.  In **VMs**, select the running VM that you want to migrate. Start the machine if it's not running.
3.  In **Virtual Machine**, select **Migrate Virtual Machine** to start the Migrate Virtual Machine Wizard.
     >[!NOTE]
     > The Live (VSM) transfer type is available for any destination cluster nodes that are configured to connect to a different SMB 3.0 file share from the one on which the VM was originally created.

4.  Select a node on a different cluster, and select **Next**.
5.  In **Summary**, select **Move**. To track the job status, open the **Jobs** workspace.
6.  To verify that the virtual machine was migrated, check the **VMs** list on the destination node to ensure the VM is running.

---

## Migrate storage between two locations on a standalone host

> [!NOTE]
> You can't live migrate storage for a shared VHDX file. You can move the other VM files and perform normal live migration.
> To move the shared VHDX file to another location, you must shut down the VMs and then move the file.

You can run a live migration of VM storage between locations on standalone hosts. You can move the entire virtual machine, which includes virtual hard disks (VHDs) and configuration information, or move only specific VHDs to a different location.

1.  In **VMs and Services** > **All Hosts**, select the standalone host where the VM is located.
2.  In **VMs**, select the running VM for which you want to migrate storage. Start the machine if it's not running.
3.  In **Virtual Machine**, select **Migrate Storage** to start the Migrate Virtual Machine Wizard.
4.  In **Select Path** > **Storage location**, select one of the default storage locations on the host. Or select **Browse** to view all possible storage destinations. Select the destination SMB 3.0 file share or location on the local hard disk and select **OK**.

    If you specify an SMB 3.0 file share in the **Storage location** list, ensure that you use the fully qualified domain name (FQDN) of the destination server in the share path. For example, instead of *\\\fileserver1\smbshare*, use *\\\fileserver1.contoso.com\smbshare*.

5.  Optionally, select **Add this path to the list of default storage locations on the host**, and select **Next**.
6.  On the **Summary** page, select **Move**. Track the progress in **Jobs**.


## Run live migrations concurrently

You can run live migration on multiple VMs so that two migrations occur at the same time on the same host. Note that:

- You can't select multiple VMs for a live migration. You need to manually start each migration.
- You can specify how many concurrent migrations to run. The default setting is two, which is the number of simultaneous live migrations and storage migrations that are enabled in Hyper-V. For example, a host can participate in one outgoing live migration plus one incoming, two outgoing live migrations, or two incoming live migrations.
- Live migrations and live storage migrations are independent. You can perform two live migrations and two live storage migrations simultaneously. VMM considers live virtual machine and storage migration (live VSM) as one live migration and one storage migration.
- You can view concurrent migrations in progress in Hyper-V Manager > **Actions** > **Hyper-V Settings** > **Server** >  **Live Migrations** and **Storage Migrations**. In **Jobs**, verify that the migrations occur simultaneously.


## Improve live migration speed

On Hyper-V hosts, you can increase live migration speed using compression using SMB as the transport or both. The compression method uses algorithms that reduce the data that is transmitted over the wire. The SMB method can allow for faster data transfer.

By default, faster live migration is enabled to use the compression method. You can disable, enable, or change the method of faster live migration by changing the live storage migration settings, either at the Hyper-V host level or for each live migration instance.

Change live migration settings as follows:

1.  In Hyper-V Manager, select  **Actions** > **Hyper-V Settings** >  **Server** > **Live Migration**, and select **Advanced Features**.
2.  In **Migration settings** > **Live migration settings**, do one of the following:

    -   To disable faster live migration, select **Standard live migration**.
    -   To use compression for faster live migration, select **Use compression**.
    -   To use SMB for faster live migration, select **Use SMB as Transport**.
