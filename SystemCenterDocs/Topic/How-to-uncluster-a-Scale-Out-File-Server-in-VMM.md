---
title: How to uncluster a Scale-Out File Server in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 14dd198f-21d6-4357-9227-37105172462a
---
# How to uncluster a Scale-Out File Server in VMM
You can use the following procedures to uncluster or remove a Scale\-Out File Server that is being managed in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)].

When you remove a Scale\-Out File Server, it still exists, but it's not managed by [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]. To uncluster a Scale\-Out File Server, you can use the [Uninstall-SCStorageFileServer](http://technet.microsoft.com/library/dn472840.aspx) cmdlet.

### To remove a Scale\-Out File Server

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Storage** > **Providers**.

3.  In the **Providers** pane, locate the storage provider that is associated with the Scale\-Out File Server you want to remove.

4.  On the **Home** tab, click **Remove**.

## See Also
[Modifying Scale-Out File Servers in VMM](../Topic/Modifying-Scale-Out-File-Servers-in-VMM.md)
[Managing Scale-Out File Servers with VMM](../Topic/Managing-Scale-Out-File-Servers-with-VMM.md)
[Managing storage resources and capacity with VMM](../Topic/Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)

