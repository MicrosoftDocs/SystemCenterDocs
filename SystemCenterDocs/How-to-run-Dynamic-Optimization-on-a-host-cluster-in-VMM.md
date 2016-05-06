---
title: How to run Dynamic Optimization on a host cluster in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9ea78b8e-1bd3-455c-bdb7-3e913077ea13
---
# How to run Dynamic Optimization on a host cluster in VMM
Use the following procedure to run Dynamic Optimization on demand on a host cluster in [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)]. Through Dynamic Optimization, [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] can balance load among hosts by migrating virtual machines within a host cluster. [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] only performs Dynamic Optimization on host clusters that support live migration. On demand Dynamic Optimization does not require that Dynamic Optimization be configured on the parent host group.

For more information about Dynamic Optimization, see [Configuring dynamic optimization and power optimization in VMM](./Configuring-dynamic-optimization-and-power-optimization-in-VMM.md).

**Account requirements** Administrators can run Dynamic Optimization on a host cluster. Delegated administrators can run Dynamic Optimization on host clusters that are within the scope of their Delegated Administrator user role.

### How to run Dynamic Optimization on a host cluster

1.  Open the **Fabric** workspace.

2.  On the **Fabric** pane, expand **Servers**, expand **Host Groups**, and navigate to the host cluster on which you want to run Dynamic Optimization. Then click the host cluster to select it.

3.  On the **Folder** tab, in the **Optimization** group, click **Optimize Hosts**.

    [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] performs a Dynamic Optimization review to determine whether virtual machines can be migrated to improve load balancing in the host cluster. If migrating virtual machines can improve load balancing, VMM displays a list of virtual machines that are recommended for migration, with the current and target hosts indicated. The list excludes any hosts that are in maintenance mode in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] and any virtual machines that are not highly available.

4.  To perform Dynamic Optimization on the host cluster, click **Migrate**.

## See Also
[Configuring dynamic optimization and power optimization in VMM](./Configuring-dynamic-optimization-and-power-optimization-in-VMM.md)
[How to configure Dynamic Optimization and Power Optimization in VMM](./How-to-configure-Dynamic-Optimization-and-Power-Optimization-in-VMM.md)
[Managing hosts and host clusters with VMM](./Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](./Managing-fabric-resources-with-VMM.md)


