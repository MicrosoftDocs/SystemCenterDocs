---
ms.assetid: 0746e47e-407b-44d7-b83d-655df3f53fb8
title: Set up dynamic and power optimization in the VMM compute fabric
description: This article describes how to configure dynamic optimization and power optimization in the VMM fabric
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy23, engagement-fy24
---

# Set up dynamic and power optimization in VMM


Read this article to learn about enabling dynamic optimization (DO) and power optimization for virtual machines (VMs) in System Center Virtual Machine Manager (VMM). The article includes features overview, instructions for setting up BMC for power optimization, and describes how to enable and run these features.

:::moniker range="<=sc-vmm-2019"
>[!NOTE]
> - VMM supports dynamic optimization for Compute and Storage. Versions prior to VMM 2019 support DO for compute only. Use the following procedures, as applicable, for the version of VMM you are using.
> - VMM doesn’t support site aware clusters or stretched clusters. VMM doesn’t consider Hyper-V defined *site-specific fault domains* for dynamic optimization calculation.
:::moniker-end
:::moniker range=">=sc-vmm-2022"
>[!NOTE]
> - VMM supports dynamic optimization for Compute and Storage. Use the following procedures, as applicable, for the version of VMM you are using.
> - VMM doesn’t support site aware clusters or stretched clusters. VMM doesn’t consider Hyper-V defined *site-specific fault domains* for dynamic optimization calculation.
:::moniker-end

- **Dynamic optimization**: Using dynamic optimization, VMM performs live migration of VMs and VHDs within a host cluster. The migration is based on the settings you specify to improve load balancing among hosts and cluster shared storage (cluster shared volumes (CSVs), file shares) and to correct the placement issues for VMs.

  - **Compute Dynamic optimization** (Optimization of hosts) can be performed on hosts in a cluster to optimize host performance by migrating VMs across hosts. You can set the host performance thresholds to **CPU** and **Memory**.
:::moniker range="<=sc-vmm-2019"
   - **Storage Dynamic Optimization** (Optimization of disk space applicable for VMM 2019 and later) can be performed on cluster shared storage (CSVs, file shares) to optimize storage space availability by migrating Virtual Hard Disks (VHDs) across shared storage. You can set free storage space threshold on cluster shared storage.
   :::moniker-end
   :::moniker range=">=sc-vmm-2022"
   - **Storage Dynamic Optimization** (Optimization of disk space) can be performed on cluster shared storage (CSVs, file shares) to optimize storage space availability by migrating Virtual Hard Disks (VHDs) across shared storage. You can set free storage space threshold on cluster shared storage.
   :::moniker-end

- **Power optimization**: Power optimization is a feature of dynamic optimization that saves energy by turning off hosts that aren't needed to meet resource requirements within a cluster, and turns them back on when they're needed.
:::moniker range="<=sc-vmm-2019"
VMM supports compute dynamic optimization (both compute and storage in VMM 2019 and later) and power optimization on Hyper-V host clusters. Compute dynamic optimization and power optimization is also supported on VMware host clusters in the VMM fabric that support live migration.
:::moniker-end
:::moniker range=">=sc-vmm-2022"
VMM supports compute and storage dynamic optimization and power optimization on Hyper-V host clusters. Compute dynamic optimization and power optimization is also supported on VMware host clusters in the VMM fabric that support live migration.
:::moniker-end

## Before you start
Note the following information before you start using DO.

## Dynamic optimization

- Dynamic optimization and power optimization can be configured on host clusters that support live migration.
- Dynamic optimization can be configured on a host group to migrate virtual machines and virtual hard disks (VHDs) within host clusters with a specified frequency and aggressiveness. VM aggressiveness determines the amount of load imbalance that is required to initiate a migration during dynamic optimization.

::: moniker range=">=sc-vmm-2019"
- Disk space aggressiveness determines the amount of free storage space below disk space threshold that is required to migrate VHDs to other cluster shared storage during dynamic optimization.
::: moniker-end

- By default, virtual machines are migrated every 10 minutes with medium aggressiveness if automatic migration is enabled. When configuring frequency and aggressiveness for dynamic optimization, an administrator must factor in the resource cost of additional migrations against the advantages of balancing load among hosts/shared storage in a host cluster. By default, a host group inherits Dynamic Optimization settings from its parent host group.
- If you set up dynamic optimization on a host group without a cluster, it will have no effect.
- Dynamic optimization can be set up for clusters with two or more nodes. Storage dynamic optimization will need two or more shared storage files/volumes to be present in the cluster. If a host group contains standalone hosts or host clusters that don't support live migration, dynamic optimization isn't performed on those hosts. Any hosts that are in maintenance mode are also excluded from dynamic optimization. In addition, VMM only migrates highly available virtual machines that use shared storage. If a host cluster contains virtual machines that aren't highly available, those virtual machines aren't migrated during Dynamic Optimization.
- On-demand dynamic optimization is also available for individual host clusters using the Optimize Hosts/Optimize Disk space  action in the VMs and Services workspace. It can be performed without configuring dynamic optimization on host groups. After dynamic optimization is requested for a host cluster, VMM lists the virtual machines/VHDs that will be migrated for the administrator's approval. Optimize Hosts performs VM load balancing across hosts in a cluster, while Optimize disk space migrates VHDs across Shared storage in a cluster.

### Node fairness

::: moniker range="sc-vmm-2016"

Node fairness is a new feature in Windows Server 2016.

::: moniker-end

It identifies cluster nodes with light loads, and distributes VMs to those nodes to balance load. This is similar to VMM's dynamic optimization. To avoid potential performance issues, dynamic optimization and node fairness must not work together. To ensure this doesn't happen, VMM disables node fairness in all clusters in a host group for which dynamic optimization is set to automatic. If you enable node fairness outside the VMM console, VMM will turn it off the next time that dynamic optimization refreshes. If you do want to use node fairness, disable dynamic optimization and then manually enable node fairness.

## Power optimization

- For power optimization, the computers must have a baseboard management controller (BMC) that enables out-of-band management.
- Power optimization ensures that a cluster maintains a quorum if an active node fails. For clusters created outside VMM and added to VMM, Power Optimization requires more than four nodes. For each additional one or two nodes in a cluster, one node can be powered down. For instance:
	- One node can be powered down for a cluster of five or six nodes.
	- Two nodes can be powered down for a cluster of seven or eight nodes.
	- Three nodes can be powered down for a cluster of nine or ten nodes.
- When VMM creates a cluster, it creates a quorum disk and uses that disk as part of the quorum model. For clusters created by VMM, Power Optimization can be set up for clusters of more than three nodes. This means that the number of nodes that can be powered down is as follows:
	- One node can be powered down for a cluster of four or five nodes.
	- Two nodes can be powered down for a cluster of six or seven nodes.
	- Three nodes can be powered down for a cluster of eight or nine nodes.

## Configure BMC

For hosts with BMC that support IMPI 1.5/2.0, DCMI 1.0, or SMASH 1.0 over WS-Management, you can configure BMC settings as follows:

1. Create a Run As account with permissions to access the BMC on a host.
2. Select **Fabric** > **Servers** > **All Hosts** > host > **Properties** > **Hardware** > **Advanced** > **BMC Setting**.
3. To enable VMM management, select **This physical machine is configured for OOB management**.
4. In **This computer supports the specified OOB power management configuration provider**, select the supported management protocol. Enter the IP address of the BMC, and accept the default port offered by VMM. Select the Run As account and select **OK**.


## Enable dynamic and power optimization for a host group

1. Select **Fabric** > **Servers** > **All Hosts** and select the host group that you want to configure.

2. With the host group selected, select **Folder** > **Properties** group > **Properties**.

3. In the host group properties, select **Dynamic Optimization**.

4. In  **Specify dynamic optimization settings**, clear the **Use Dynamic Optimization settings from the parent host group** checkbox.
:::moniker range="sc-vmm-2016"
5. In **Aggressiveness**, select **High**, **Medium**, or **Low**.

   >[!NOTE]
   > In VMM 2019 and later, VM aggressiveness values are replaced from low/medium/high scale to integer scale 1 to 5.
   >
   > 1 is the lowest degree of aggressiveness, and 5 is the highest.
:::moniker-end

:::moniker range=">=sc-vmm-2019"
5. In **Aggressiveness**, select a value on an integer scale of 1 to 5, where 1 is the lowest degree of aggressiveness and 5 is the highest.
:::moniker-end

   VM aggressiveness determines the amount of load imbalance that is required to initiate a migration during dynamic optimization.

   Disk space aggressiveness determines the amount of free storage space below disk space threshold that is required to migrate VHDs to other cluster shared storage during dynamic optimization.
   ::: moniker range="sc-vmm-2016"
   When you configure frequency and aggressiveness for dynamic optimization, you must try to balance the resource cost of additional migrations against the advantages of balancing load among hosts in a host cluster. Initially, you might accept the default value of **Medium**. After you observe the effects of dynamic optimization in your environment, you can increase the aggressiveness.
   ::: moniker-end
   ::: moniker range=">=sc-vmm-2019"
   When you configure frequency and aggressiveness for dynamic optimization, you must try to balance the resource cost of additional migrations against the advantages of balancing load among hosts in a host cluster. Initially, you might accept the default value of **3**. After you observe the effects of dynamic optimization in your environment, you can increase the aggressiveness.
   ::: moniker-end
6. To help conserve energy by having VMM turn off hosts when they aren't needed and turn them on again when they're needed, configure power optimization for the host group. Power optimization is only available when virtual machines are being migrated automatically to balance load.

7. To periodically run dynamic optimization on qualifying host clusters in the host group, enter the following settings:

   1.  Select the **Automatically migrate virtual machines to balance load** checkbox to balance free storage space across shared storage.
   2. In **Frequency**, specify how often to run dynamic Optimization. You can enter any value between 10 minutes and 1440 minutes \(24 hours\).
:::moniker range="<=sc-vmm-2019"
8. Set thresholds for each of the compute and storage (applicable for VMM 2019 and later) resources listed. To change the units of the resources, go to  **Host group**> **Properties**  > **Host Reserves** and choose the unit from the dropdown menu.
:::moniker-end
:::moniker range=">=sc-vmm-2022"
8. Set thresholds for each of the compute and storage resources listed. To change the units of the resources, go to  **Host group**> **Properties**  > **Host Reserves** and choose the unit from the dropdown menu.
:::moniker-end
9. To turn on power optimization on the host group, select the **Enable power optimization** checkbox. Select **OK** again to save your changes.

    >[!NOTE]
    > If there is a mismatch of disk space warning levels between host groups having the same file share, it can result in multiple migrations to and from that file share and can impact storage DO performance. We recommend you to not do a file share across different host groups where storage dynamic optimization is enabled.

## Configure power optimization settings


1.  In the **Fabric**, navigate to the host group and open **Properties**.
2.  Select **Dynamic Optimization** > **Specify dynamic optimization settings** > **Settings**.
3.  In **Customize Power Optimization Schedule**, change the settings for any of these resources: CPU, memory, disk I/O, or network I/O.
4.  Under **Schedule**, select the hours when you want power optimization to be performed. Select a box to turn power optimization on or off for that hour. VMM applies the schedule according to the host time zone.

## Run dynamic optimization on-demand in a host cluster


You can run dynamic optimization on demand on a host cluster. To do this, dynamic optimization doesn't need to be configured on the parent host group.

1. Open **Fabric** > **Servers** > **Host Groups** and navigate to the host cluster.
2. To perform compute resource load balancing, select **Optimize hosts**. To perform storage load balancing across cluster shared storage, select **Optimize disks**.

    **To Optimize hosts**: VMM performs a dynamic optimization review to determine whether VHDs can be migrated to improve load balancing in the host cluster. If migration of VMs can improve load balancing, VMM displays a list of VMs that are recommended for migration, with the current and target hosts indicated. The list excludes any hosts that are in maintenance mode in VMM and any virtual machines that aren't highly available.

    **To Optimize Disk Space**: VMM performs a dynamic optimization review to determine whether VHDs can be migrated to meet the free storage space threshold (disk space) while considering aggressiveness set in the Dynamic Optimization page. Dynamic Optimization will only be triggered when any cluster shared storage violates the disk space threshold set. If migration of VHDs can help free the storage space threshold in shared storage in the cluster, VMM displays a list of VHDs that are recommended for migration, with the current and target storage space indicated. VHDs will only migrate to another shared storage with the same storage classification.

3. Select **Migrate**.

::: moniker range=">=sc-vmm-2019"

> [!NOTE]
> If VHDs are migrated between one storage type to another (for example, from a CSV to NAS file share), the storage migration will be slow. If the storage optimization does not return a list of VHDs to migrate even when the threshold and aggressiveness criteria are met:
>    - Check the HostVolumeID using Get-SCStorageVolume Cmdlet. If the HostVolumeID returns Null for the volume, refresh the VM and perform Storage Dynamic Optimization again.
>    - Check the DiskSpacePlacementLevel of the host group using the Get-SCHostReserve cmdlet. Set the DiskSpacePlacementLevel value equal to the value of Disk Space set in Host Reserve settings in the Dynamic Optimization wizard.

::: moniker-end

## Power on/off a computer in VMM

1. Select **Fabric** > **Servers** > **All Hosts** > host name.
2. On the **Host** tab, in the **Host** group, select **Power On** or **Power Off**. You can view information about power on and off events in the BMC logs (select **Hardware** > **Advanced** > **BMC Logs**).

## Next steps
Learn about [provisioning VMs](provision-vms.md).
