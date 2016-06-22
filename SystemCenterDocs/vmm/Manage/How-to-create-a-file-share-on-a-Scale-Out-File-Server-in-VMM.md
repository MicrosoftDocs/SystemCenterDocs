---
title: How to create a file share on a Scale-Out File Server in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 418b1158-9d53-4be5-a885-87b9878ce277
---
# How to create a file share on a Scale-Out File Server in VMM
On a Scale\-Out File Server in Virtual Machine Manager \(VMM\), you can create a new file share from an existing storage pool or from a Cluster Shared Volume \(CSV\). VMM performs the necessary steps to create the file share, for example \(if necessary\) creating the storage space, initializing and formatting the disk, and creating the CSV. To see how this procedure fits into an overall workflow, see [Overview: configuring storage using Scale-Out File Servers in VMM](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md).

Before you begin this procedure, it might be helpful to review mirror spaces, specifically two\-way mirror spaces and three\-way mirror spaces, which are described in [What are the best uses of simple, mirror, and parity spaces?](http://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx#What_are_the_best_uses_of_simple_mirror_and_parity_spaces) in "Storage Spaces Frequently Asked Questions \(FAQ\)."

### To create a file share on a Scale\-Out File Server in VMM

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, click **Storage**, and then on the **Home** tab, click **Create File Share**.

3.  Fill in the **Create File Share Wizard**as follows:

    |Item|Information to specify|
    |--------|--------------------------|
    |**Storage Type**|<ul><li>**File Server**: Select the Scale\-Out File Server that you want to create the share on. For information about creating or adding a Scale\-Out File Server, see the links at the end of this topic.</li><li>**Name** and **Description**: Type the share name, and optionally, a description.</li><li>**Storage type** and **Storage pool**:<br /><br /><ul><li>If a storage pool exists, and you want VMM to do the necessary initializing and formatting steps, select the **Storage pool** option, and then select the storage pool you want to use.<br />        If you haven't created the pool yet, see [How to create or modify a storage pool on a Scale-Out File Server in VMM](How-to-create-or-modify-a-storage-pool-on-a-Scale-Out-File-Server-in-VMM.md).</li><li>If the CSV already exists, select the **Volume** option, and then specify the CSV you want to use.</li><li>If the folder \(path\) already exists, for example, if the file share was accidently deleted, select **Local path**, and specify the path.</li></ul></li><li>**Classification**: The file share inherits the classification of the storage pool. If you want a different classification, select that classification from the list, or click **New** and create a classification. For information about classifications, see [Stage 2: Plan your storage classifications](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md#BKMK_classifications) in "Overview: configuring storage using Scale\-Out File Server clusters in VMM."</li></ul>|
    |**Capacity**|-   **Size**: Type the size in MB.<br />-   **File system**: You can leave this at the default setting, unless the disk is used for backups or for deduplication, in which case **NTFS** is recommended. If the operating system on the file server is Windows Server Technical Preview or Windows Server 2012 R2, the default is **ReFS** \(Resilient File System\). If it is Windows Server 2012, the default is **NTFS**.<br />-   **Resiliency**: For ReFS, resiliency must be mirror \(either two\-way or three\-way\). For NTFS, it can be mirror \(either two\-way or three\-way\) or parity \(either single or dual\). The default is a three\-way mirror. For more information, see [What are the best uses of simple, mirror, and parity spaces?](http://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx#What_are_the_best_uses_of_simple_mirror_and_parity_spaces) in "Storage Spaces Frequently Asked Questions \(FAQ\)."<br />-   **Data deduplication**: Enabled or disabled. For more information, see[Data Deduplication Overview](http://technet.microsoft.com/library/hh831602.aspx).<br />-   **Allocation unit size** \(optional\): You can specify an allocation unit size \(also called "cluster size"\), or leave it at the default.<br />-   **Enable storage tiers**: If you select this, the **Storage Tiers** page appears.|
    |**Storage Tiers**|Specify settings for the storage tiers. For information about storage tiers, see[What's New in Storage Spaces in Windows Server](http://technet.microsoft.com/library/dn387076.aspx).<br /><br />This wizard page only appears if you enabled storage tiers on the previous page.|

4.  On the **Summary** page, confirm the settings, and then click **Finish**.

    Depending on your settings, the **Jobs** dialog box might appear. Ensure that the job has a status of **Completed**, and then close the dialog box.

5.  To verify that the file share was created, in the **Fabric** pane, expand **Storage** > **File Servers**. In the **File Servers, File Shares** pane, expand the file server where you created the file share.

For details about what VMM does when creating the file share, see [Stage 4: Create file shares](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md#BKMK_shares) in "Overview: configuring storage using Scale\-Out File Server clusters in VMM."

## See Also
[Configuring storage using Scale-Out File Servers in VMM](Configuring-storage-using-Scale-Out-File-Servers-in-VMM.md)
[How to add an existing Scale-Out File Server to storage in VMM](How-to-add-an-existing-Scale-Out-File-Server-to-storage-in-VMM.md)
[Creating a host cluster in VMM from existing Windows servers](Creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md)
[Deploying Hyper-V hosts or host clusters from bare metal with VMM](Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)


