---
ms.assetid: 9148e441-d7c0-4ee5-b784-df93de8394ab
title: Provision a cluster from Hyper-V standalone hosts in the VMM fabric
description: This article provides about provisioning a Hyper-V cluster in the VMM fabric
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 04/14/2025
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy24
---

# Provision a cluster from Hyper-V standalone hosts in the VMM fabric

Use the instructions in this article to create a cluster from standalone Hyper-V host servers that are managed in the System Center Virtual Machine Manager (VMM) fabric.

## Before you start

**Prerequisite** | **Details**
--- | ---
**VMM** | You'll need a VMM host group set up in the fabric. This is needed to allocate shared storage logical units if VMM needs to assign shared storage to the cluster nodes.
**Hyper-V** | You must have two or more standalone Hyper-V hosts in the VMM fabric that are in the same VMM host group.<br/><br/> The hosts must meet the requirements for failover clustering.<br/><br/> All the hosts that will be in the cluster must be running the same operating system.<br/><br/> All hosts must belong to the same VMM host group.<br/><br/> You must have a domain account \(to use as the basis for a Run As account\) for creating the cluster. The account must have administrative permissions on the servers that will become cluster nodes and must belong to the same domain as those servers. Also, the account requires **Create Computer objects** permission in the container that is used for Computer accounts in the domain.
**Storage** | Storage must be discovered and classified in the Fabric workspace of the VMM console. Then, either storage pools or logical units or both must be allocated to the host group or the parent host group chosen for your set of hosts.<br/><br/> If the shared storage isn't managed by VMM, disks must be available to all nodes in the cluster before you can add them. You'll need to provision one or more logical units to all hosts that you want to cluster, and mount and format the storage disks on one of the hosts.<br/><br/> To access shared storage, the Multipath I/O (MPIO) feature must be installed on each Hyper-V host. VMM doesn't add this automatically. You can add MPIO using the server manager. If MPIO is installed, VMM will automatically enable it for supported storage arrays using the Microsoft provided Device Specific Module \(DSM\). If you already installed vendor\-specific DSMs for supported storage arrays and then add the host VMM, the vendor\-specific MPIO settings will be used to communicate with those arrays. If you add a host to VMM management before you add the MPIO feature, you must add the MPIO feature, and then manually configure MPIO to add the discovered device hardware IDs. Or you can install vendor\-specific DSMs.<br/><br/> If you're using iSCSI SAN as your shared storage, the Microsoft iSCSI initiator service must be installed and running (set to automatic) on each Hyper-V host. VMM uses the iSCSI initiator service to configure shared storage on the Hyper-V nodes automatically when the cluster is created. There's no need to discover iSCSI portals on each Hyper-V node if VMM manages the shared storage.<br/><br/> If you're using a Fibre Channel storage array network \(SAN\), each host must have a host bus adapter \(HBA\) installed, and zoning must be correctly configured. For more information, see your storage array vendor’s documentation. <br/><br/> By default, when VMM manages the assignment of logical units, VMM creates one storage group per host, either a standalone host or a host cluster node. However, for some storage arrays, it's preferable to use one storage group for the entire cluster, where host initiators for all cluster nodes are contained in a single storage group. To support this, you must set the CreateStorageGroupsPerCluster property to $true using the [Set-SCStorageArray](/previous-versions/system-center/powershell/system-center-2012-r2/jj613218(v=sc.20)) cmdlet.
**Networking** | For all Hyper-V hosts that you want to cluster, if the hosts are configured to use static IP addresses on a particular network, ensure that the static IP addresses on all hosts are in the same subnet.<br/><br/> If you've already created a network configuration in VMM that is relevant to the cluster and have applied that configuration to network adapters in the hosts, ensure that the configuration is applied consistently across all the hosts you want to cluster. For example, if you've designated a specific set of network adapters (one per host) as management adapters for the cluster, ensure that the name of the logical network and VM network associated with those network adapters is consistent. When VMM is identifying networks that the cluster can use, it will only recognize networks with consistent settings on every node.

## Create a cluster

1. In the VMM console, select **Fabric** > **Create** > **Hyper-V Cluster** to open the Create Hyper-V Cluster wizard.
2. In **General**, specify a cluster name and choose the host group in which the existing Hyper-V hosts are located.
3. In **Resource Type**, select the Run As account that you'll use to create the cluster. The account that you use must have administrative permissions on the servers that will become cluster nodes and must belong to the same domain as the Hyper\-V hosts that you want to cluster. Also, the account requires **Create Computer objects** permission in the container that is used for Computer accounts in the domain. Ensure that **Existing Windows servers** is selected, and if you don't need support from Microsoft for this cluster, you can select **Skip cluster validation**.

::: moniker range="<=sc-vmm-2022"
4. In **Nodes**, select the Hyper-V host servers that you want to include in the cluster. You can select multiple hosts using the CTRL key or a range using SHIFT.
::: moniker-end

::: moniker range="sc-vmm-2025"
4. In **Nodes**, select the Hyper-V host servers that you want to include in the cluster. You can select multiple hosts using the CTRL key or a range using SHIFT. Cluster validation requires CLIUSR account to be added in the Windows Server 2025 nodes that are being added to a cluster.
::: moniker-end

5. In **IP address** (if it appears), enter the IP address you want to use for the cluster.
6. In **Storage**, select the data disks you want the cluster to use. The list of available disks includes the logical units associated with the host group that you selected at the beginning of the wizard.
    - If you assigned storage out-of-band, disks that aren't managed by VMM are displayed and selected as available disks, with the checkbox next to each disk dimmed and unavailable.
      - If you're using a non-Microsoft clustered file system \(CFS\) solution, ensure that you're aware which disks are CFS disks. Don't select those disks for the cluster. If you do, cluster creation will fail.
      - If the number of selected hosts for the cluster is even, the smallest disk that is larger than 500 megabytes \(MB\) is automatically chosen as the witness disk and is unavailable for selection.
7. In **Virtual Switches**, you can select the logical networks to use when VMM automatically creates virtual switches on the Hyper-V nodes. The external virtual switches on destination Hyper-V nodes. VMM will automatically create the virtual switches on all the Hyper-V nodes.
8. In **Summary**, confirm the settings and then select **Finish**. You can monitor the cluster status on the **Jobs** page. After the job finishes, you can verify cluster information by right-clicking **Properties** > **Status** tab on the cluster. You can also right-click the cluster and select **Validate Cluster**.

Here's what VMM does after you create the cluster:

1. Validates that all hosts meet the prerequisites, such as required operating system and domain membership
2. Enables the Failover Clustering feature on each host
3. Unmasks the selected storage logical units to each host
4. Runs the cluster validation process
5. Creates the cluster with quorum settings, configures any cluster static IP settings that you specified, and enables Cluster Shared Volumes \(CSVs\)
6. Assign the logical unit as a CSV on the cluster for each logical unit that is designated as a CSV.

## Next steps

[Provision VMs](provision-vms.md)
