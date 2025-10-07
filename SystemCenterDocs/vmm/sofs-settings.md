---
ms.assetid: aa0580cc-884b-42bc-8326-ff0b4291d703
title: Manage SOFS Settings in the VMM Fabric
description: This article describes how to manage SOFS settings in the VMM fabric
ms.date: 08/21/2025
author: Jeronika-MS
ms.author: v-gajeronika
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: engagement-fy24
---

# Manage SOFS settings in the VMM fabric

This article describes how to manage SOFS settings in the VMM fabric. You can manage scale-out file server (SOFS) in the System Center Virtual Machine Manager (VMM) fabric as follows:

- **Create storage pools**: Create storage pools from physical disks on SOFS nodes and allocate them.
- **Create file shares**: You can create file shares on a SOFS in the VMM fabric. You can set the storage type for a share as a storage pool, local pool, or volume.
- **QoS**: Set up a quality-of-service (QoS) policy for SOFS to control resources allocated to VMs.
:::moniker range=">=sc-vmm-2016 <=sc-vmm-2019"
- **Set a disk witness for a storage pool**: From VMM 2016, you can specify that the disk witness for a SOFS cluster must come from a particular storage pool. To do this, VMM creates a three-way mirror space and configures it as the disk witness for the cluster. The storage pool must have at least five physical disks.
:::moniker-end
:::moniker range=">=sc-vmm-2022"
- **Set a disk witness for a storage pool**: In VMM, you can specify that the disk witness for a SOFS cluster must come from a particular storage pool. To do this, VMM creates a three-way mirror space and configures it as the disk witness for the cluster. The storage pool must have at least five physical disks.
:::moniker-end

## Create storage pools

To create storage pools, follow these steps:

1. Select **Fabric** > **Storage** > **File Servers**. Right-click the SOFS server (not the nodes) and select **Manage Pools**.
2. In **Manage Pools of File Server**, select **New** to create a new pool or modify an existing one.
3. In **General**, specify a name and select a storage classification.
4. In **Physical Disks**, select the disks you want to include in the pool. Disks will be displayed in accordance with the SOFS settings. For example, a file server with shared storage might show SAS storage disks, or a file server using Storage Spaces Direct would show local disks attached to each node.
5. In **Default Settings**, retain the default settings unless you need to change for a specific reason.

	- **Fault domain**: When you select a fault domain, you specify how many copies of your data will be distributed across a cluster.

     > [!NOTE]
     > Fault domain isn't displayed for clusters configured with Storage Spaces Direct. These clusters have a fault domain of **Node** to indicate that copies of data are stored on multiple nodes in the cluster and data is available even if a specific node isn't.

	- **Interleave**: Interleave (along with the number of columns) specify the way in which data is written to physical disks.

6. Select **OK** to save the storage pool settings. After the job completes, verify the pools in **Fabric** > **Storage** > **Classifications and Pools**.

## Create a file share

To create a file share, follow these steps:

1. Select **Fabric** > **Storage** > **Home** > **Create File Share**.
2. In **Create File Share Wizard** > **Storage Type**, select the SOFS on which you want to create a share. Enter a name and description for the share and select the storage pool you want to use. If the CSV exists, select **Volume** and specify it. If the folder path exists, select **Local path** and specify it. The file share inherits the classification of the storage pool.
3. In **Capacity**, specify the file share size and type. Leave the default type unless the disk is used for backups or deduplication, in which case NTFS is recommended.
4. In **Capacity** > **Resiliency**, for ReFS, resilience must be mirror (two or three-way). For NTFS, it can be mirror or parity (single or dual). The default is a three-way mirror.
5. Enable deduplication if necessary. Change the unit size allocation if required, and optionally enable storage tiers.
6. In **Summary**, review the settings and select **Finish**. Verify the file share in **Fabric** > **Storage** > **File Servers** > **File Shares**.

## Set a storage QoS for a SOFS

To set a storage QoS, follow these steps:

:::moniker range=">=sc-vmm-2016 <=sc-vmm-2019"
 System Center VMM 2016 and later include storage QoS policies to solve the **noisy neighbor** problem. This problem is common in virtualized environments. When two virtual machines (VMs) share a resource, say a disk, there's always a chance that one VM's usage of the resource exceeds that of the other. This can affect the performance of an app running on the VM. Storage QoS ensures:
:::moniker-end
:::moniker range=">=sc-vmm-2022"
 System Center VMM includes storage QoS policies to solve the **noisy neighbor** problem. This problem is common in virtualized environments. When two virtual machines (VMs) share a resource, say a disk, there's always a chance that one VM's usage of the resource exceeds that of the other. This can affect the performance of an app running on the VM. Storage QoS ensures:
:::moniker-end
- **Mitigation of noisy neighbor issues**: Ensures that a single VM doesn't consume all the resources and starves the other VMs of storage bandwidth.
- **Monitor end-to-end storage performance**: When VMs are started on a SOFS, their performance is monitored.
- **Manage storage I/O in accordance with business needs**: Storage QoS policies define minimum and maximum limits for VMs and ensure they're met even in over-provisioned environments. If policies can't be met, alerts are issued.

## Set a storage QoS policy

To set a storage QoS policy, follow these steps:

1. Select **Fabric** > **Storage** > **QoS Policies** > **Create Storage QoS Policy**.
2. In **Create Storage QoS Policy Wizard** > **General**, specify a name and description for the policy.
3. In **Policy Settings**, select whether you want all the virtual hard disks for VMs to share resources equally or allocate resources per VM. If you choose to allocate per instance, you'll need to set a minimum and maximum IOPS. Then a virtual disk to which the policy is applied will receive the minimum and maximum limits.
4. In **Scope**, specify the file servers on which to apply the policy. You can apply the policy to multiple servers, which is useful when you migrate VMs across servers so that QoS policy settings remain the same.
5. In **Summary**, review the settings and select **Finish**. Verify the policy in **Fabric** > **Storage** > **QoS Policies**.


## Set a disk witness for the SOFS

To set a disk witness, follow these steps:

1. Select **Fabric** > **Storage** > **File Servers**. Right-click the SOFS server (not the nodes) and select **Properties**.
2. In **General**, select **Use disk witness for this file server from the specified pool** to indicate that the disk witness for the SOFS must come from a specific storage pool. VMM creates a three-way mirror space, and configures it as the disk witness for the cluster.

## Next steps

[Set QoS for storage resources](./manage-sofs-qos.md).
