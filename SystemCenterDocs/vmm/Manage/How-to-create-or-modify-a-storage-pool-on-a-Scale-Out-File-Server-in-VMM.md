---
title: How to create or modify a storage pool on a Scale-Out File Server in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce7dfc06-7d96-404d-82ad-de4ccdf44c26
---
# How to create or modify a storage pool on a Scale-Out File Server in VMM
You can use Virtual Machine Manager \(VMM\) to create or modify storage pools on Scale\-Out File Servers. Storage pools are described in [Storage Spaces Overview](http://technet.microsoft.com/library/hh831739.aspx). To see how this procedure fits into an overall workflow, see [Overview: configuring storage using Scale-Out File Servers in VMM](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md).

### To create or modify a storage pool on a Scale\-Out File Server

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, click **Storage** > **File Servers**.

3.  In the **File Servers, File Shares** pane, right\-click the Scale\-Out File Server \(not the nodes\), and then click **Manage Pools**. The **Manage Pools of File Server <file server>** dialog box appears.

4.  Click **New**, or select a storage pool you want to modify and then click **Edit**.

5.  A wizard or properties dialog box appears. Fill in the pages or tabs:

    |Page or tab|Notes|
    |---------------|---------|
    |**General**|For a new storage pool, type a **Name** and select a **Classification**. To create a new classification for this pool, click **New**, and then specify and name and description for the classification. For information about classifications, see [Stage 2: Plan your storage classifications](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md#BKMK_classifications) in "Overview: configuring storage using Scale\-Out File Server clusters in VMM."|
    |**Physical Disks**|A list of the disks in the Scale\-Out File Server is displayed. For example, with a file server using shared storage, the disks might be Serial Attached SCSI \(SAS\) storage disks. As another example, with a file server using Storage Spaces Direct, the disks would be the local disks attached to each cluster node.<br /><br />To modify an existing storage pool, select disks you want to add, and clear the boxes for disks you want to remove.<br /><br />For a new pool, the list includes only disks that are not in a storage pool.|
    |**Default Settings**|For specific configurations where you need to change the fault domain or interleave, configure these settings here. Otherwise, you can use default settings.<br /><br />-   **Fault domain**: When you select a fault domain, you specify how you want the copies of your data to be distributed across the cluster. For example, to store copies of your data on multiple disks in the cluster, select **Disk**. **Note:**     **Fault domain** is not displayed for clusters configured with Storage Spaces Direct. These clusters always have a fault domain of **Node**, which means that copies of the data are stored on multiple nodes in the cluster. Even if a node becomes unavailable, access to data continues uninterrupted.<br />-   **Interleave**: Optionally, you can change the interleave value from the default. Interleave works with another parameter, the number of columns, to control the precise way in which data is written to physical disks. For more information, see [Storage Spaces Frequently Asked Questions (FAQ)](http://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx).|

6.  Close the wizard or dialog box.

7.  Click **OK** to create or modify the storage pool.

    Depending on your settings, the **Jobs** dialog box might appear. Ensure that the job has a status of **Completed**, and then close the dialog box.

8.  After the job completes, to confirm that the storage pool exists and is in the right classification, in the **Fabric** pane, under **Storage**, click **Classifications and Pools**, and expand the classifications as needed to view the pools.

To create a file share, see [How to create a file share on a Scale-Out File Server in VMM](How-to-create-a-file-share-on-a-Scale-Out-File-Server-in-VMM.md).

To see how this procedure fits into an overall workflow, see [Overview: configuring storage using Scale-Out File Servers in VMM](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md).

## See Also
[Configuring storage using Scale-Out File Servers in VMM](Configuring-storage-using-Scale-Out-File-Servers-in-VMM.md)


