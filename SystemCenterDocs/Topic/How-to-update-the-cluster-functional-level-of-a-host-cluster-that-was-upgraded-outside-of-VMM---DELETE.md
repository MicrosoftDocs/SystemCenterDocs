---
title: How to update the cluster functional level of a host cluster that was upgraded outside of VMM - DELETE
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: adac7641-068e-47af-805b-52e80540ee8a
---
# How to update the cluster functional level of a host cluster that was upgraded outside of VMM - DELETE
If you use the upgrade wizard to upgrade a [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)] cluster to [!INCLUDE[winthreshold_server_2](../Token/winthreshold_server_2_md.md)], the wizard performs this step automatically.  However, you may encounter circumstances where you need to perform this operation manually. For example, if a cluster's nodes were upgraded before you brought the cluster into [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] but the cluster is still functioning as a [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)] cluster, you can use this procedure to update it to a [!INCLUDE[winthreshold_server_2](../Token/winthreshold_server_2_md.md)] cluster.

### To update the cluster functional level of a cluster whose nodes were upgraded outside of [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, click **Servers**, and then click **All Hosts**.

3.  Right\-click the cluster you want to upgrade, and click **Update Version**.

## See Also
[Upgrading Windows Server 2012 R2 host clusters to Windows Server 2016 Technical Preview in VMM](../Topic/Upgrading-Windows-Server-2012-R2-host-clusters-to-Windows-Server-2016-Technical-Preview-in-VMM.md)
[Managing Hyper-V hosts and host clusters with VMM](../Topic/Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)

