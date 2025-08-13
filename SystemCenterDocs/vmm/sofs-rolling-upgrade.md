---
ms.assetid: 599241ef-28b7-4a9c-ad1f-d2c79f5dd784
title: Run a Rolling Upgrade of a SOFS Cluster to Windows Server in VMM
description: This article describes how to do a rolling upgrade of a SOFS cluster in the VMM storage fabric.
ms.date: 04/22/2025
author: jyothisuri
ms.author: jsuri
ms.topic: upgrade-and-migration-article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy24
---

# Run a rolling upgrade of a SOFS cluster to Windows Server in VMM

This article describes how to do a rolling upgrade of a SOFS cluster in the VMM storage fabric.

::: moniker range="sc-vmm-2016"
Cluster rolling upgrade was introduced in Windows Server 2016. It enables you to upgrade the operating system of cluster nodes in a scale-out file server (SOFS) cluster, or Hyper-V cluster, without stopping workloads running on the nodes. [Read more](/windows-server/failover-clustering/cluster-operating-system-rolling-upgrade#requirements) about rolling upgrade requirements and architecture.
::: moniker-end

::: moniker range=">sc-vmm-2016"
Cluster rolling upgrade enables you to upgrade the operating system of cluster nodes in a scale-out file server (SOFS) cluster, or Hyper-V cluster, without stopping workloads running on the nodes. [Read more](/windows-server/failover-clustering/cluster-operating-system-rolling-upgrade#requirements) about rolling upgrade requirements and architecture.
::: moniker-end

This article describes how to perform a cluster rolling upgrade of SOFS managed in the System Center Virtual Machine Manager (VMM) fabric. Here's what the upgrade does:

- **Creates a template**: Creates a template of the node configuration by combining the appropriate physical computer profile with the node configuration settings detailed in the upgrade wizard.

- **Migrates workloads**: Migrates workloads off the node so that workload operations aren't interrupted.

- **Removes node**: Puts the node into maintenance mode and then removes it from the cluster. This removes all VMM agents, virtual switch extensions, and so forth, from the node.
::: moniker range=">=sc-vmm-2016 <=sc-vmm-2022"
- **Provisions the node**: Provisions the node running Windows Server 2016, and configures it according to the saved template.
:::moniker-end
::: moniker range="sc-vmm-2025"
- **Provisions the node**: Provisions the node running Windows Server 2025/2022/2019, and configures it according to the saved template.
:::moniker-end
- **Returns the node to VMM**: Brings the node back under VMM management and installs the VMM agent.

- **Returns the node to the cluster**: Adds the node back into the SOFS cluster, brings it out of the maintenance mode, and returns virtual machine workloads to it.

## Before you start

Here are some considerations before you start running a rolling upgrade:

- The cluster must be managed by VMM.
::: moniker range="sc-vmm-2016"
- The cluster must be running Windows Server 2012 R2 or later.
::: moniker-end
::: moniker range=">=sc-vmm-2019 <=sc-vmm-2022"
- The cluster must be running Windows Server 2016 or later.
::: moniker-end
::: moniker range="sc-vmm-2025"
- The cluster must be running Windows Server 2019 or later.
::: moniker-end
- The cluster must meet the [requirements](sofs-bare-metal.md#before-you-start) for bare metal deployment. The only exception is that the physical computer profile doesn't need to include network or disk configuration details. During the upgrade, VMM records the node's network and disk configuration and uses that information instead of the computer profile.

- You can upgrade nodes that weren't originally provisioned using bare metal as long as those nodes meet bare metal requirements such as BMC. You'll need to provide this information in the upgrade wizard.
:::moniker range=">=sc-vmm-2016 <=sc-vmm-2022"
- The VMM library needs a virtual hard disk configured with Windows Server 2016.
:::moniker-end
:::moniker range="sc-vmm-2025"
- The VMM library needs a virtual hard disk configured with Windows Server 2025/2022/2019.
:::moniker-end

## Run the upgrade

To run the upgrade, follow these steps:

1. Select **Fabric** > **Storage** > **File Servers**. Right-click the SOFS > **Upgrade Cluster**.

2. In the Upgrade Wizard > **Nodes**, select the nodes you want to upgrade or **Select All**. Select **Physical computer profile**, and select the profile for the nodes.

3. In **BMC Configuration**, select the Run As account with permissions to access the BMC or create a new account. In **Out-of-band management protocol**, select the protocol that the BMCs use. To use DCMI, select **IPMI**. DCMI is supported even though it's not listed. Ensure that the correct port is listed.

4. In **Deployment Customization**, review the nodes to upgrade. If the wizard couldn't figure out all the settings, it displays a **Missing Settings** alert for the node. For example, if the node wasn't provisioned by bare metal, BMC settings might not be complete. Fill in the missing information as below:
    - Enter the BMC IP address if required. You can also change the node name. Don't clear **Skip Active Directory check for this computer name** unless you're changing the node name and you want to ensure the new name isn't in use.
    - In the network adapter configuration, you can specify the MAC address. Do this if you're configuring the management adapter for the cluster, and you want to configure it as a virtual network adapter. It's not the MAC address of the BMC. If you choose to specify static IP settings for the adapter, select a logical network and an IP subnet if applicable. If the subnet contains an address pool, you can select **Obtain an IP address corresponding to the selected subnet**. Otherwise, enter an IP address within the logical network.
:::moniker range=">=sc-vmm-2016 <=sc-vmm-2022"
5. In **Summary**, select **Finish** to begin the upgrade. If the wizard finishes, the node upgrades successfully so that all the SOFS nodes are running Windows Server 2016 or later. The wizard upgrades the cluster functional level to Windows Server 2016.
:::moniker-end
:::moniker range="sc-vmm-2025"
5. In **Summary**, select **Finish** to begin the upgrade. If the wizard finishes, the node upgrades successfully so that all the SOFS nodes are running Windows Server 2019 or later. The wizard upgrades the cluster functional level to Windows Server 2025.
:::moniker-end

::: moniker range="sc-vmm-2016"
If you need to update the functional level of a SOFS that was upgraded outside VMM, you can do that by right-clicking the **Files Servers** > **SOFS name** > **Update Version**. This might be necessary if you upgraded the SOFS nodes before adding it to the VMM fabric, but SOFS is still functioning as a Windows Server 2012 R2 or later cluster.
::: moniker-end

::: moniker range=">=sc-vmm-2019 <=sc-vmm-2022"
If you need to update the functional level of a SOFS that was upgraded outside VMM, you can do that by right-clicking the **Files Servers** > SOFS name > **Update Version**. This might be necessary if you upgraded the SOFS nodes before adding it to the VMM fabric, but SOFS is still functioning as a Windows Server 2016 or later cluster.
::: moniker-end

::: moniker range="sc-vmm-2025"
If you need to update the functional level of a SOFS that was upgraded outside VMM, you can do that by right-clicking the **Files Servers** > SOFS name > **Update Version**. This might be necessary if you upgraded the SOFS nodes before adding it to the VMM fabric, but SOFS is still functioning as a Windows Server 2019 or later cluster.
::: moniker-end
