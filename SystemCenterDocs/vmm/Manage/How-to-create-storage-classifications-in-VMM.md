---
title: How to create storage classifications in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45266dad-a5cc-4872-8176-37a6f8dbfb2f
---
# How to create storage classifications in VMM
You can use the following procedure to create storage classifications in Virtual Machine Manager (VMM). Storage classifications enable you to assign user-defined storage classifications to discovered storage pools, typically by quality of service (QoS). For example, you could assign a classification of GOLD to storage pools that have the highest performance and availability.

**Account requirements** To complete this procedure, you must be a member of the Administrator user role or a member of the Delegated Administrator user role.

### To create storage classifications

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Storage**, right-click **Classification and Pools**, and then click **Create Classification**.

3.  In the **New Classification** dialog box, enter a name and description for each classification that you want to create. Click **Add** to add each newly created classification.

    As an example, you can create the following classifications.

    > [!NOTE]
    > This information is provided only as an example. Use classifications and descriptions that make sense for your environment.

    |Name|Description|
    |--------|---------------|
    |**GOLD**|**Storage pool based on solid-state drives (SSDs) that delivers high performance for I/O intensive applications**|
    |**SILVER**|**Fibre Channel Serial Attached SCSI (SAS) storage (RAID 5)**|
    |**BRONZE**|**iSCSI Serial ATA (SATA) storage (RAID 5)**|

## See Also
[Overview: storage classifications in VMM](Overview--storage-classifications-in-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


