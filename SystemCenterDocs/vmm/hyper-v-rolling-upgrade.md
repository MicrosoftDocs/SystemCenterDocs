---
ms.assetid: e7d1bf48-453f-49a4-bb4f-e85bbf3fc302
title: Perform a rolling upgrade of a Hyper-V host cluster to Windows Server 2016 in VMM
description: This article provides guidance on upgrading Hyper-V host clusters
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Perform a rolling upgrade of a Hyper-V host cluster to Windows Server 2016 in VMM

>Applies To: System Center 2016 - Virtual Machine Manager

Cluster rolling upgrade in a new feature in Windows Server 2016. It enables you to upgrade the operating system of cluster nodes from Windows Server 2012 R2 to Windows Server 2016 without stopping Hyper-V workloads running on the nodes. [Read more](https://technet.microsoft.com/library/dn850430.aspx) about rolling upgrade requirements and architecture.

## Cluster rolling upgrade in VMM

System Center 2016 - Virtual Machine Manager (VMM) supports using the rolling upgrade feature to upgrade Hyper-V clusters in the VMM fabric. You can upgrade an entire cluster, or specific cluster nodes. Here's what the upgrade does:

- **Creates a template**: Creates a template of the node configuration by combining the appropriate physical computer profile with the node configuration settings detailed in the upgrade wizard.
- **Migrates workloads**: Migrates workloads off the node so workload operations aren't interrupted.
- **Removes node**: Puts the node into maintenance mode and then removes it from the cluster. This removes all VMM agents, virtual switch extensions, and so forth from the node.
- **Provisions the node**: Provisions the node running Windows Server 2016, and configures it according to the saved template.
- **Returns the node to VMM**: Brings the node back under VMM management and installs the VMM agent.
- **Returnw the node to the cluster**: Adds the node back into the cluster, brings it out of maintenance mode, and returns virtual machine workloads to it.

## Before you start

- The cluster must be managed by VMM.
- The cluster must be running Windows Server 2012 R2.
- The cluster must meet the [requirements](hyper-v-bare-metal.md#before-you-start) for bare metal deployment. The only exception is that the physical computer profile doesn't need to include network or disk configuration details. During the upgrade VMM records the node's network and disk configuration and uses that information instead of the computer profile.
- You can upgrade nodes that weren't originally provisioned using bare metal as long as those nodes meet bare metal requirements such as BMC. You'll need to provide this information in the upgrade wizard.
- The VMM library needs a virtual hard disk configured with Windows Server 2016.


## Run the upgrade

1. Click **Fabric** > **Servers** > **All Hosts**. Right-click the host cluster > **Upgrade Cluster**.
2. In the Upgrade Wizard > **Nodes**, click the nodes you want to upgrade or **Select All**. Then click **Physical computer profile**, and select the profile for the nodes.
3. In **BMC Configuration**, select the Run As account with permissions to access the BMC or create a new one. In **Out-of-band management protocol** click the protocol that the BMCs use. To use DCMI click IPMI. DCMI is supported even though it's not listed. Make sure the correct port is listed.
4. In **Deployment Customization**, review the nodes to upgrade. If the wizard couldn't figure out all of the settings it displays a **Missing Settings** alert for the node. For example if the node wasn't provisioned by bare metal BMC settings might not be complete. Fill in the missing information.

	- Enter the BMC IP address if required. You can also change the node name. Don't clear **Skip Active Directory check for this computer name** unless you're changing the node name and you want to make sure thenew name is not in use.
	- In the network adapter configuration you can specify the MAC address. Do this if you're configuring the management adapter for the cluster, and you want to configure it as a virtual network adapter. It's not the MAC address of the BMC. If you choose to specify static IP settings for the adapter, select a logical network and an IP subnet if applicable. If the subnet contains and address pool you can select **Obtain an IP address corresponding to the selected subnet**. Otherwise type an IP address within the logical network.

5. In **Summary** click **Finish** to begin the upgrade. If the wizard finishes the node upgrades successfully all all of the cluster nodes are running Windows Server 2016 the wizard upgrade the cluster functional level to Windows Server 2016.


If for some reason you need to update the cluster functional level of a cluster that was upgraded outside VMM you can upgrade the functional level by right-clicking the **Cluster** > **Update Version**. This could happen if you upgrade the cluster nodes before adding the cluster to the VMM fabric, but the cluster is still functioning as a Windows Server 2012 R2 cluster.
