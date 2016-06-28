---
title: Prerequisites: configuring block storage in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18c46061-a045-4849-8d4e-86e8946053c7
---
# Prerequisites: configuring block storage in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

Before you configure storage in Virtual Machine Manager (VMM), review the following prerequisites:

-   The storage that you configure in VMM must be used by Hyper-V hosts or host clusters.

-   Storage arrays must be on the list in [Supported storage arrays for System Center 2012 VMM](http://social.technet.microsoft.com/wiki/contents/articles/16100.supported-storage-arrays-for-system-center-2012-vmm.aspx). Note that VMM recognizes storage on storage arrays that do not appear in this list. However, there is no guarantee that you can perform active management operations, such a logical unit provisioning, masking and unmasking, cloning, and taking snapshots on those storage arrays through VMM. If a storage array is not on this list, we recommend that you contact your storage vendor to determine VMM support.

-   WMI SMP providers from Dell EqualLogic and Nexsan must be installed on the VMM management server.

-   The SMI-S provider cannot be installed on the VMM management server.

-   If the SMI-S provider type for the storage array is a "proxy" provider that must be installed on a separate server, obtain and install the latest version of the SMI-S provider from your storage vendor on a server that the VMM management server can access over the network by IP address or by the fully qualified domain name (FQDN).

-   Review the choice between configuring one storage group per cluster or one storage group per node.

    > [!NOTE]
    > In VMM, a "storage group" binds together host initiators, target ports, and logical units. A storage group contains the host’s initiator IDs (one or more), in the form of either iSCSI Qualified Name (IQN) or World Wide Name (WWN). A storage group also contains one or more target ports and one or more logical units. Logical units are exposed to the host initiators through the target ports.

    When VMM manages the assignment of logical units, by default, it creates one storage group or masking set per host. The host can be either a stand-alone host or a host cluster node. However, for some storage arrays, it is preferable to use one storage group for the entire cluster, where host initiators for all cluster nodes are contained in a single storage group. To support this configuration, you must set the `CreateStorageGroupsPerCluster` property to `$true` by using the   [Set-SCStorageArray](http://technet.microsoft.com/library/jj613218.aspx) cmdlet.

## See Also
[Configuring block storage in VMM](Configuring-block-storage-in-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



