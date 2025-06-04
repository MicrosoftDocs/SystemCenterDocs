---
ms.assetid: e7d1bf48-453f-49a4-bb4f-e85bbf3fc302
title: Perform a rolling upgrade of a Hyper-V host cluster to Windows Server in VMM
description: This article provides guidance on upgrading Hyper-V host clusters
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.topic: article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: engagement-fy24
---

# Perform a rolling upgrade of a Hyper-V host cluster to Windows Server in VMM



Cluster rolling upgrade feature enables you to upgrade the operating system of cluster nodes without stopping Hyper-V workloads running on the nodes. [Read more](/windows-server/failover-clustering/cluster-operating-system-rolling-upgrade#requirements) about rolling upgrade requirements and architecture.

::: moniker range="sc-vmm-2019"

>[!NOTE]
> System Center 2019 Virtual Machine Manager (VMM) supports rolling upgrade of a Hyper-V host cluster from Windows Server 2016 to Windows Server 2019. Versions earlier to VMM 2019 support rolling upgrade to 2016 from 2012 R2. Use the following procedures as applicable for the version of VMM you're using and the upgrade version it supports.

::: moniker-end

::: moniker range="sc-vmm-2022"

>[!NOTE]
> System Center 2022 Virtual Machine Manager (VMM) supports rolling upgrade of a Hyper-V host cluster from Windows Server 2019 to Windows Server 2022. Use the following procedures as applicable for the version of VMM you're using and the upgrade version it supports.

::: moniker-end

::: moniker range="sc-vmm-2025"

>[!NOTE]
> System Center 2025 - Virtual Machine Manager (VMM) supports rolling upgrade of a Hyper-V host cluster from Windows Server 2022 to Windows Server 2025. Use the following procedures as applicable for the version of VMM you're using and the upgrade version it supports.

::: moniker-end

## Cluster rolling upgrade in VMM

System Center Virtual Machine Manager (VMM) supports using the rolling upgrade feature to upgrade Hyper-V clusters in the VMM fabric. You can upgrade an entire cluster or specific cluster nodes. Here's what the upgrade does:

- **Creates a template**: Creates a template of the node configuration by combining the appropriate physical computer profile with the node configuration settings detailed in the upgrade wizard.

- **Migrates workloads**: Migrates workloads off the node, so workload operations aren't interrupted.

- **Removes node**: Puts the node into maintenance mode and then removes it from the cluster. This removes all VMM agents, virtual switch extensions, and so forth, from the node.
::: moniker range=">=sc-vmm-2016 <=sc-vmm-2022"
- **Provisions the node**: Provisions the node running Windows Server 2016/2019, and configures it according to the saved template.
::: moniker-end
::: moniker range="sc-vmm-2025"
- **Provisions the node**: Provisions the node running Windows Server 2019/2022, and configures it according to the saved template.
::: moniker-end
- **Returns the node to VMM**: Brings the node back under VMM management and installs the VMM agent.

- **Returns the node to the cluster**: Adds the node back into the cluster, brings it out of the maintenance mode, and returns virtual machine workloads to it.

::: moniker range=">=sc-vmm-2019"

> [!NOTE]
> Ensure to install the latest updates on the VHD that you want to use as a physical computer profile.

::: moniker-end

## Prerequisites

Review the platform [restrictions and limitations](/windows-server/failover-clustering/cluster-operating-system-rolling-upgrade#restrictions--limitations) before you start cluster rolling upgrade.

::: moniker range="<=sc-vmm-2019"
- The cluster must be managed by VMM.
- The cluster must be running Windows Server 2012 R2 (in releases prior to 2019) or Windows Server 2016 (in VMM 2019).
- The cluster must meet the [requirements](hyper-v-bare-metal.md#before-you-start) for bare metal deployment. The only exception is that the physical computer profile doesn't need to include network or disk configuration details. During the upgrade, VMM records the node's network and disk configuration and uses that information instead of the computer profile.
- You can upgrade nodes that weren't originally provisioned using bare metal as long as those nodes meet bare metal requirements such as BMC. You'll need to provide this information in the upgrade wizard.
- The VMM library needs a virtual hard disk configured with Windows Server 2016.
::: moniker-end

::: moniker range="sc-vmm-2022"
- The cluster must be managed by VMM.
- The cluster must be running Windows Server 2016 or 2019.
- The cluster must meet the [requirements](hyper-v-bare-metal.md#before-you-start) for bare metal deployment. The only exception is that the physical computer profile doesn't need to include network or disk configuration details. During the upgrade, VMM records the node's network and disk configuration and uses that information instead of the computer profile.
- You can upgrade nodes that weren't originally provisioned using bare metal as long as those nodes meet bare metal requirements such as BMC. You'll need to provide this information in the upgrade wizard.
- The VMM library needs a virtual hard disk configured with Windows Server 2016 or 2019.
::: moniker-end

::: moniker range="sc-vmm-2025"
- The cluster must be managed by VMM.
- The cluster must be running Windows Server 2019 or later.
- The cluster must meet the [requirements](hyper-v-bare-metal.md#before-you-start) for bare metal deployment. The only exception is that the physical computer profile doesn't need to include network or disk configuration details. During the upgrade, VMM records the node's network and disk configuration and uses that information instead of the computer profile.
- You can upgrade nodes that weren't originally provisioned using bare metal as long as those nodes meet bare metal requirements such as BMC. You'll need to provide this information in the upgrade wizard.
- The VMM library needs a virtual hard disk configured with Windows Server 2019 or later.
::: moniker-end

## Run the upgrade

::: moniker range="<=sc-vmm-2019"

1. Select **Fabric** > **Servers** > **All Hosts**. Right-click the host cluster > **Upgrade Cluster**.
1. In the Upgrade Wizard > **Nodes**, select the nodes you want to upgrade or **Select All**. Then select **Physical computer profile** and select the profile for the nodes.
1. In **BMC Configuration**, select the Run As account with permissions to access the BMC or create a new one. In **Out-of-band management protocol**, select the protocol that the BMCs use. To use DCMI, select IPMI. DCMI is supported even though it's not listed. Ensure the correct port is listed.
1. In **Deployment Customization**, review the nodes to upgrade. If the wizard couldn't figure out all the settings, it displays a **Missing Settings** alert for the node. For example, if the node wasn't provisioned by bare metal, BMC settings might not be complete. Fill in the missing information.
    - Enter the BMC IP address if required. You can also change the node name. Don't clear **Skip Active Directory check for this computer name** unless you're changing the node name and you want to ensure the new name isn't in use.
    - In the network adapter configuration, you can specify the MAC address. Do this if you're configuring the management adapter for the cluster, and you want to configure it as a virtual network adapter. It's not the MAC address of the BMC. If you choose to specify static IP settings for the adapter, select a logical network and an IP subnet, if applicable. If the subnet contains an address pool, you can select **Obtain an IP address corresponding to the selected subnet**. Otherwise, enter an IP address within the logical network.
5. In **Summary**, select **Finish** to begin the upgrade. If the wizard finishes the nodes upgrade successfully, the wizard upgrades the cluster functional level to Windows Server 2016/2019.

::: moniker-end

::: moniker range="sc-vmm-2022"

1. Select **Fabric** > **Servers** > **All Hosts**. Right-click the host cluster > **Upgrade Cluster**.
1. In the Upgrade Wizard > **Nodes**, select the nodes you want to upgrade or **Select All**. Then select **Physical computer profile** and select the profile for the nodes.
1. In **BMC Configuration**, select the Run As account with permissions to access the BMC or create a new one. In **Out-of-band management protocol**, select the protocol that the BMCs use. To use DCMI, select IPMI. DCMI is supported even though it's not listed. Ensure the correct port is listed.
1. In **Deployment Customization**, review the nodes to upgrade. If the wizard couldn't figure out all the settings, it displays a **Missing Settings** alert for the node. For example, if the node wasn't provisioned by bare metal, BMC settings might not be complete. Fill in the missing information.
    - Enter the BMC IP address if required. You can also change the node name. Don't clear **Skip Active Directory check for this computer name** unless you're changing the node name and you want to ensure the new name isn't in use.
    - In the network adapter configuration, you can specify the MAC address. Do this if you're configuring the management adapter for the cluster, and you want to configure it as a virtual network adapter. It's not the MAC address of the BMC. If you choose to specify static IP settings for the adapter, select a logical network and an IP subnet, if applicable. If the subnet contains an address pool, you can select **Obtain an IP address corresponding to the selected subnet**. Otherwise, enter an IP address within the logical network.
5. In **Summary**, select **Finish** to begin the upgrade. If the wizard finishes the nodes upgrade successfully, the wizard upgrades the cluster functional level to Windows Server 2019/2022.

::: moniker-end

::: moniker range="sc-vmm-2025"

1. Select **Fabric** > **Servers** > **All Hosts**. Right-click the host cluster > **Upgrade Cluster**.
1. In the Upgrade Wizard > **Nodes**, select the nodes you want to upgrade or **Select All**. Then select **Physical computer profile**, and select the profile for the nodes.
1. In **BMC Configuration**, select the Run As account with permissions to access the BMC or create a new one. In **Out-of-band management protocol**, select the protocol that the BMCs use. To use DCMI, select IPMI. DCMI is supported even though it's not listed. Ensure the correct port is listed.
1. In **Deployment Customization**, review the nodes to upgrade. If the wizard couldn't figure out all of the settings, it displays a **Missing Settings** alert for the node. For example, if the node wasn't provisioned by bare metal, BMC settings might not be complete. Fill in the missing information.
    - Enter the BMC IP address if required. You can also change the node name. Don't clear **Skip Active Directory check for this computer name** unless you're changing the node name and you want to ensure the new name isn't in use.
    - In the network adapter configuration, you can specify the MAC address. Do this if you're configuring the management adapter for the cluster, and you want to configure it as a virtual network adapter. It's not the MAC address of the BMC. If you choose to specify static IP settings for the adapter, select a logical network and an IP subnet, if applicable. If the subnet contains an address pool, you can select **Obtain an IP address corresponding to the selected subnet**. Otherwise, type an IP address within the logical network.
5. In **Summary**, select **Finish** to begin the upgrade. If the wizard finishes the nodes upgrade successfully, the wizard upgrades the cluster functional level to Windows Server 2022/2025.

::: moniker-end

::: moniker range="<=sc-vmm-2019"

If for some reason you need to update the cluster functional level of a cluster that was upgraded outside VMM, right-click the **Cluster** > **Update Version**. This could happen if you upgrade the cluster nodes before adding the cluster to the VMM fabric, but the cluster is still functioning as a Windows Server 2012 R2/2016 cluster.

::: moniker-end

::: moniker range="sc-vmm-2022"

If for some reason you need to update the cluster functional level of a cluster that was upgraded outside VMM, right-click the **Cluster** > **Update Version**. This could happen if you upgrade the cluster nodes before adding the cluster to the VMM fabric, but the cluster is still functioning as a Windows Server 2016/2019 cluster.

::: moniker-end

::: moniker range="sc-vmm-2025"

If for some reason you need to update the cluster functional level of a cluster that was upgraded outside VMM, right-click the **Cluster** > **Update Version**. This could happen if you upgrade the cluster nodes before adding the cluster to the VMM fabric, but the cluster is still functioning as a Windows Server 2019/2022 cluster.

::: moniker-end