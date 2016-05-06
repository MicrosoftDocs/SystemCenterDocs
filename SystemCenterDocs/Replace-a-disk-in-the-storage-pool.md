---
title: Replace a disk in the storage pool
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 101055ea-34ce-4467-bbca-e2a481f3f0a7
---
# Replace a disk in the storage pool
You can use the following procedure to replace a disk in the storage pool if a disk fails.

1.  In the **Disk Management** console, identify the replica volumes and recovery point volumes that are stored on the failed disk.

2.  Remove protection from the data sources that have replica volumes and recovery point volumes on the failed disk, and select **Delete protected data**.

3.  Physically remove the disk that needs to be replaced, and add the replacement disk

4.  In [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] Administrator Console, click **Management** > **Disks** tab > select the disk you removed > **Actions** > **Remove**.

5.  In the **Actions** pane >  **Add** > **Available disks**. Select the replacement disk > **Add**. Add the data sources from step 2 to an existing protection group, or create a new protection group for these data sources. Note that:

    -   If you create a new protection group and have tape backup of the data sources, create the replicas manually by using the tape backup.

    -   If you create a new protection group and don’t have tape backup of the data sources, allow [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] to create the replicas across the network.

    -   If you add the data sources to an existing protection group, [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] will start an immediate consistency check, which will re\-create the replicas.


