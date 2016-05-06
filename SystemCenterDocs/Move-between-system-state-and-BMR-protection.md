---
title: Move between system state and BMR protection
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 213b9564-4acd-4056-8fef-017f29a44553
---
# Move between system state and BMR protection
You can migrate from system state protection to BMR protecting by modifying the protection group settings. Note the following:

-   If you move from system state protection to BMR protection, BMR protection will require less space on the recovery point volume. However, the extra space on the volume is not reclaimed. You can shrink the volume size manually from the **Modify Disk Allocation** page of the Modify Protection Group Wizard or by using the **Get\-DatasourceDiskAllocation** and **Set\-DatasourceDiskAllocation** cmdlets.

-   If you move from system state protection to BMR protection, BMR protection will require more space on the replica volume. The volume will be extended automatically. If you want to change the default space allocations you can use **Modify\-DiskAllocation**.

-   If you move from BMR protection to system state protection you’ll need more space on the recovery point volume.

    [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] might try to automatically grow the volume. If there is insufficient space in the storage pool, an error will be issued.

-   If you move from BMR protection to system state protection you’ll need space on the protected computer because system state protection first writes the replica to the local computer and then transfers it to the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server.

-   If you are trying to remove BMR protection to free up disk space, you must stop protection of BMR and system state.

