---
ms.assetid: 20a0b182-231f-4483-a6cb-701f1b72b857
title: Allocate storage to VMM host groups
description: This article describes how to allocate block storage to VMM host groups
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/24/2023
ms.topic: article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy23
---

# Allocate storage to host groups



After block storage has been discovered and classified in the System Center - Virtual Machine Manager (VMM) fabric, you can allocate it to host groups. You can allocate an entire storage pool or a specific logical unit (LUN).

- **Allocate storage pools**: You can optionally allocate storage pools to host groups. If you do, you can:
     - Create and assign LUNs directly from Hyper-V hosts in the host group.
	 - Use the storage pool for rapid provisioning using SAN cloning or snapshots. During this process, you don't need to create LUNs because VMM requests a copy of an existing LUN during provisioning.

- **Allocate LUNs**:
	- You can assign LUNs for storage pools that are managed in the VMM fabric.
		- In order to allocate LUNs to host groups, there must be unassigned LUNs in the managed storage pools.
		- If you need additional LUNs, you can create them outside of VMM in your storage management tool, or you can provision them directly in VMM if the storage pool is allocated to a host group.


## Allocate a storage pool to a host group

1.  Select **Fabric** > **Storage** > **Allocate Capacity**, and then select the host group. If you're a delegate admin with scope restricted to host groups, right-click the host group > **Properties** > **Storage**.
2.  The total and available storage capacity information is displayed for the host group. The storage capacity information includes the total and available capacity for both local and remote storage, and total and available allocated storage. Select **Allocate Storage Pools**.
3. Select a storage pool > **Add**.

## Create a LUN in VMM

1. Ensure that you've allocated the storage pool to the host group, and select **Fabric** > **Storage** > **Create Logical Unit**.
2. Specify the storage pool, a name and description for the LUN, and the size. Select **OK** to create the LUN.
3. Verify that the LUN was created in **Fabric Resources** > **Classifications, Storage Pools, and Logical Units**.


## Allocate a LUN to a host group

1.  Select **Fabric** > **Storage** > **Allocate Capacity** > **Allocate Storage Capacity** and select the host group.
2.  Select **Allocate Logical Units**, select a unit > **Add**.

After LUNs are allocated to host groups, you can assign them to Hyper-V hosts and clusters.

## Next steps

After you set up Hyper-V hosts and clusters, learn about [provisioning VMs](provision-vms.md).
