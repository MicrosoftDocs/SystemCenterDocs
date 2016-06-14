---
title: Prerequisites: creating a host cluster in VMM from existing Windows servers
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce4332bc-814c-42de-bb89-4947c4e42d68
---
# Prerequisites: creating a host cluster in VMM from existing Windows servers
Before you [!INCLUDE[vmm12sp1_long](../../includes/vmm12sp1_long_md.md)] to create a host cluster from existing servers, review the prerequisites in this topic.

-   [Host cluster prerequisites: hosts and account](Prerequisites--creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md#BKMK_hosts_hosts)

-   [Host cluster prerequisites: Fibre Channel or iSCSI storage arrays](Prerequisites--creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md#BKMK_arrays) \(for Fibre Channel or iSCSI storage only\)

-   [Host cluster prerequisites: storage allocation and configuration](Prerequisites--creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md#BKMK_storage_allocation) \(for all storage configurations\)

-   [Host cluster prerequisites: networking](Prerequisites--creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md#BKMK_networking)

For information about bare\-metal provisioning, or procedures you can follow after meeting these prerequisites, see the links at the end of this topic.

## <a name="BKMK_hosts_hosts"></a>Host server and account prerequisites
You must meet the following prerequisites for the servers and the account that you will use to create the cluster:

-   You must have two or more stand\-alone Hyper\-V hosts that are managed by [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)]. For more information, see [Adding Windows servers as Hyper-V hosts or host clusters in VMM](Adding-Windows-servers-as-Hyper-V-hosts-or-host-clusters-in-VMM.md) and the [Server Operating Systems](https://technet.microsoft.com/library/dn997307.aspx) requirements.

-   The Hyper\-V hosts must meet the requirements for failover clustering. All of the hosts intended for one  cluster must be running the same operating system.

-   The Hyper\-V hosts that you want to add as cluster nodes must be located in the same Active Directory domain. The domain must be trusted by the domain of the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management server.

-   The Hyper\-V hosts must belong to the same host group in [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)].

-   You must have a domain account \(to use as the basis for a Run As account\) for creating the cluster. The account must have administrative permissions on the servers that will become cluster nodes, and must belong to the same domain as those servers. Also, the account requires **Create Computer objects** permission in the container that is used for Computer accounts in the domain. For more information, see the account prerequisites listed in[Create a Failover Cluster](http://technet.microsoft.com/library/dn505754.aspx#BKMK_ClusPrereq).

## <a name="BKMK_arrays"></a>Host server prerequisites when using Fibre Channel or iSCSI arrays for storage
If you are using Fibre Channel or iSCSI storage, your hosts must have access to the storage array. The following list provides details:

-   **Multipath I\/O**: The Multipath I\/O \(MPIO\) feature must be added on each host that will access the Fibre Channel or iSCSI storage array. You can add the MPIO feature through Server Manager.

    For more information, including information about how to add the MPIO feature, see[Microsoft Multipath I/O (MPIO) Users Guide for Windows Server 2012](http://www.microsoft.com/download/details.aspx?id=30450).

    If the MPIO feature is already enabled before you add a host to [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management, [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] will automatically enable MPIO for supported storage arrays by using the Microsoft provided Device Specific Module \(DSM\). If you already installed vendor\-specific DSMs for supported storage arrays, and then add the host to [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management, the vendor\-specific MPIO settings will be used to communicate with those arrays.

    If you add a host to [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management before you add the MPIO feature, you must add the MPIO feature, and then manually configure MPIO to add the discovered device hardware IDs. Or, you can install vendor\-specific DSMs.

-   **Fibre Channel**: If you are using a Fibre Channel storage array network \(SAN\), each host must have a host bus adapter \(HBA\) installed, and zoning must be correctly configured. For more information, see your storage array vendor’s documentation.

-   **iSCSI**: If you are using an iSCSI SAN, make sure that iSCSI portals have been added and that the iSCSI initiator is logged into the array. Additionally, make sure that the Microsoft iSCSI Initiator Service on each host is started and set to Automatic.

    > [!IMPORTANT]
    > In [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)], a "storage group" binds together host initiators, target ports, and logical units. A storage group contains the host’s initiator IDs \(one or more\), in the form of either iSCSI Qualified Name \(IQN\) or World Wide Name \(WWN\). A storage group also contains one or more target ports and one or more logical units. Logical units are exposed to the host initiators through the target ports.
    > 
    > By default, when [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] manages the assignment of logical units, [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] creates one storage group per host, either a stand\-alone host or a host cluster node. However, for some storage arrays, it is preferable to use one storage group for the entire cluster, where host initiators for all cluster nodes are contained in a single storage group. To support this configuration, you must set the `CreateStorageGroupsPerCluster` property to `$true` by using the [Set-SCStorageArray](http://technet.microsoft.com/library/jj613218.aspx) cmdlet.

## <a name="BKMK_storage_allocation"></a>Storage configuration and allocation prerequisites
Prerequisites vary for storage allocation and configuration, depending on whether your storage is under [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management:

-   **For storage under [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management**: To use shared storage that is under [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management, storage must already be discovered and classified in the Fabric workspace of the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] console. Then, either storage pools, logical units \(or file shares\), or both must be allocated to the host group or the parent host group chosen for your set of hosts. For more information, see[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md).

    If you allocate storage pools to host groups, you can wait until after the host cluster is created to create logical units \(within the storage pools\) on the cluster. For more information, see [How to configure storage on a Hyper-V host cluster in VMM](How-to-configure-storage-on-a-Hyper-V-host-cluster-in-VMM.md).

-   **For storage not under [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management**: To use shared storage that is not under [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management, disks must be available to all nodes in the cluster before you can add them. Therefore, you must provision one or more logical units to all hosts that you want to cluster, and mount and format the storage disks on one of the hosts.

    > [!IMPORTANT]
    > [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] is agnostic regarding the use of asymmetric storage, where a workload can use disks that are shared between a subset of the cluster nodes. [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] does not support or block this storage configuration. Note that to work correctly with [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)], each cluster node must be a possible owner of the cluster disk. \(Support for asymmetric storage was introduced in Windows Server 2008 R2 Service Pack 1.\)

## <a name="BKMK_networking"></a>Networking prerequisites

-   For all Hyper\-V hosts that you want to cluster, if the hosts are configured to use static IP addresses on a particular network, make sure that the static IP addresses on all hosts are in the same subnet.

-   If you have already created a network configuration in [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] that is relevant to the cluster, and have applied that configuration to network adapters in the hosts, ensure that the configuration is applied consistently across all the hosts you want to cluster. For example, if you have designated a specific set of network adapters \(one per host\) as management adapters for the cluster, make sure that the name of the logical network and VM network associated with those network adapters is consistent. When [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] is identifying networks that the cluster can use, it will only recognize networks with consistent settings on every node.

    For more information about creating a network configuration in [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)], see [Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md).

## See Also
[Creating a host cluster in VMM from existing Windows servers](Creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md)
[Deploying Hyper-V hosts or host clusters from bare metal with VMM](Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)
[Managing Hyper-V hosts and host clusters with VMM](Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


