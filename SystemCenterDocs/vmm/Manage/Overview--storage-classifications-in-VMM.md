---
title: Overview: storage classifications in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: edad40e9-bf3b-4766-bea2-1d844dc065ea
---
# Overview: storage classifications in VMM
Applies To:  [!INCLUDE[scvm_threshold_1](../../includes/scvm_threshold_1_md.md)]

In [!INCLUDE[vmm12sp1_long](../../includes/vmm12sp1_long_md.md)], to simplify the assignment of storage to users and virtual machines, you create storage classifications that fit your environment. You can do this when running a wizard such as the New Storage Pool Wizard, on the page that asks you to assign a classification to the object you're creating. Or you can create the storage classification as a separate action: in the **Fabric** workspace, click **Create Storage Classification**.

For example, you could create the following classifications:

-   **Bldg1Gold**: A set of solid\-state drives \(SSDs\) that you will make available to users in building 1.

-   **Bldg1Silver**: A set of SSDs and hard disk drives \(HDDs\) that you will make available to users in building 1.

-   **Bldg2Gold**: A set of SSDs that you will make available to users in building 2.

-   **Bldg2Silver**: A set of SSDs and HDDs that you will make available to users in building 2.

After you create your classifications, you can assign the classifications to storage pools. When you create file shares in a pool, they inherit the pool's classification, but you can adjust file share classifications individually, if needed.

Later, you can use these classifications to provide the classified storage to a particular set of virtual machines or cloud users, avoiding the need to assign each individual unit of storage \(such as a storage pool or a share\) manually.

## See Also
[How to create storage classifications in VMM](How-to-create-storage-classifications-in-VMM.md)
[Configuring storage using Scale-Out File Servers in VMM](Configuring-storage-using-Scale-Out-File-Servers-in-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


