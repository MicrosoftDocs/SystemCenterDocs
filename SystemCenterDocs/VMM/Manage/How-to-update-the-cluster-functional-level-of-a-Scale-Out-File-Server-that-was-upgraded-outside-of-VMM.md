---
title: How to update the cluster functional level of a Scale-Out File Server that was upgraded outside of VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da460702-9f28-4850-af7f-494370b047d8
---
# How to update the cluster functional level of a Scale-Out File Server that was upgraded outside of VMM
If you use the upgrade wizard to upgrade a [!INCLUDE[winblue_server_2](../../Token/winblue_server_2_md.md)] Scale\-Out File Server to [!INCLUDE[winthreshold_server_2](../../Token/winthreshold_server_2_md.md)], the wizard performs this step automatically.  However, you may encounter circumstances where you need to perform this operation manually. For example, if a Scale\-Out File Server's nodes were upgraded before you brought the Scale\-Out File Server into [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] but the it is still functioning as a [!INCLUDE[winblue_server_2](../../Token/winblue_server_2_md.md)] Scale\-Out File Server, you can use this procedure to update it to a [!INCLUDE[winthreshold_server_2](../../Token/winthreshold_server_2_md.md)] Scale\-Out File Server.

### To update the cluster functional level of a Scale\-Out File Server whose nodes were upgraded outside of [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Storage** > **File Servers**, and in the **File Servers** pane, locate the Scale\-Out File Server.

3.  Right\-click the Scale\-Out File Server you want to update, and click **Update Version**.

## See Also
[Upgrading Windows Server 2012 R2 Scale-Out File Servers to Windows Server 2016 Technical Preview in VMM](Upgrading-Windows-Server-2012-R2-Scale-Out-File-Servers-to-Windows-Server-2016-Technical-Preview-in-VMM.md)
[Managing Scale-Out File Servers with VMM](Managing-Scale-Out-File-Servers-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


