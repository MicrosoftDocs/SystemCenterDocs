---
title: How to set a disk witness for a Scale-Out File Server quorum in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82197e9e-5df3-4134-9f0b-34318477d355
---
# How to set a disk witness for a Scale-Out File Server quorum in VMM
In Virtual Machine Manager \(VMM\), you can specify that the disk witness for a Scale\-out File Server cluster quorum should come from a particular storage pool. VMM will create a three\-way mirror space and configure it as the disk witness for the cluster. The storage pool must have at least five physical disks. For more information about three\-way mirror spaces and resiliency, see [What are the best uses of simple, mirror, and parity spaces?](http://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx#What_are_the_best_uses_of_simple_mirror_and_parity_spaces) in "Storage Spaces Frequently Asked Questions \(FAQ\).".

## Select a disk witness for a Scale\-out File Server cluster quorum
Use the following procedure to specify that a disk witness should come from a storage pool.

#### To select a disk witness for a Scale\-out File Server cluster quorum

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, click **Storage**, right\-click the applicable file server, and then click **Properties**.

3.  On the **General** page, select the checkbox next to **Use disk witness for this file server from the specified pool.**

4.  In the **Pools** box, select a storage pool from the drop\-down list.

5.  When complete, click **OK**.

## See Also
[How to create or modify a storage pool on a Scale-Out File Server in VMM](How-to-create-or-modify-a-storage-pool-on-a-Scale-Out-File-Server-in-VMM.md)
[Overview: configuring storage using Scale-Out File Servers in VMM](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md)
[Configuring storage using Scale-Out File Servers in VMM](Configuring-storage-using-Scale-Out-File-Servers-in-VMM.md)


