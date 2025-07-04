---
ms.assetid: 6c26db7b-d282-4d74-9456-fe2de97f7786
title: Set up MAC address pools in the VMM networking fabric
description: This article describes how to create and manage MAC address pools in the VMM fabric.
author: jyothisuri
ms.author: jsuri
ms.date: 08/21/2024
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy23, engagement-fy24
---

# Set up MAC address pools in the VMM fabric


This article provides information about System Center Virtual Machine Manager (VMM) default MAC addresses and describes how to create and manage a custom MAC address pool.

VMM uses static MAC address pools to automatically generate and assign MAC address to VMs. This article describes default MAC address pools in the VMM fabric and explains how to create custom pools.

Default MAC address pool settings:

**MAC pool name** | **Environment** | **Default range**
--- | --- | ---
**Default MAC address pool** | Hyper-V | 00:1D:D8:B7:1C:00 – 00:1D:D8:F4:1F:FF
**Default VMware MAC address pool** | ESX/ESXi | 00:50:56:00:00:00 – 00:50:56:3F:FF:FF

## Before you start

Before you create a custom MAC pool, ensure that:

- If you want to divide one of the default pools into smaller custom pools, you must first delete the default MAC address pool or the default VMware MAC address pool. You must delete the default pool to avoid duplicate MAC address assignments.
- The first three octets of the beginning and ending MAC address must be the same.
- You must enter a valid hexadecimal value between 00 and FF.
- The ranges that you specify can't overlap.
- The address range must not have the multi-cast bit set to 1. For example, you can't use addresses that start with X1, X3, X5, X7, X9, XB, XD, or XF, where X is any value.
- To avoid conflicts with addresses reserved by Microsoft, VMware, and Citrix, don't use the following prefixes:
	- Reserved for Microsoft: 00:03:FF; 00:0D:3A; 00:12:5A; 00:15:5D; 00:17:FA; 00:50:F2; 00:1D:D8 (except for the 00:1D:D8:B7:1C:00 – 00:1D:D8:F4:1F:FF range that is reserved for VMM)
	- Reserved for VMware: 00:05:69; 00:0C:29; 00:1C:14; 00:50:56 (except for the 00:50:56:00:00:00 – 00:50:56:3F:FF:FF range that is reserved as the default VMware static range)

## Create a custom pool


1. Select **Fabric** > **Networking** > **MAC Address Pools** > **Home** > **Show** > **Fabric Resources** > **Create** > **Create MAC Pool**.
2. In **Create MAC Address Pool Wizard** > **Name and Host Group**, specify a name and description. In **Host Group**, select the host groups that must use the pool.
3. In **MAC Address Range**, specify the start and end addresses.
4. In **Summary**, review the settings and select **Finish**. When the job shows as **Completed**, verify pool in **MAC Pools**.

## Release IP addresses

In some circumstances, you might want to remove addresses from the MAC pool. For example, if a host that was assigned an IP address during bare metal deployment is removed from VMM management or if a VM goes into a missing state because it was removed outside VMM.

1. Select **Fabric** > **Networking** > **MAC Address Pools** > **Home** > **Show** > **Fabric Resources**.
2. In **MAC Pools**, select the pool you want to modify > **Properties**.
3. In **Inactive addresses**, select the addresses you want to release.

## Next steps

Learn about [creating an IP address pool](network-pool.md).
