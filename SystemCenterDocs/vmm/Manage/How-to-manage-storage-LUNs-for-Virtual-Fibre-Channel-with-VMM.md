---
title: How to manage storage LUNs for Virtual Fibre Channel with VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 32532316-0282-491c-b884-6bf5fa787c7c
---
# How to manage storage LUNs for Virtual Fibre Channel with VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

For a host computer, VM, or computer service tier to access storage array resources, Logical Units (LUs) and associated Numbers (LUNs) must be created and then registered (unmasked) to the host, VM, or tier.

Use the following procedures to create a new logical unit number (LUN) for a storage array and  register (unmask) a LUN to one or more host HBA initiator ports:

-   [To create a LUN](#BKMK_CreateLUN)

-   [To register a storage LUN](#BKMK_RegLun)

## <a name="BKMK_CreateLUN"></a>To create a storage LUN

1.  Open the **Fabric** workspace.

2.  In the **Fabrics** pane, click **Storage** and then click **Classifications and Pools**.

3.  Under **Name**, click the applicable storage device, and then on the **Home** tab, click **Create Logical Unit**.

4.  In the **Create Logical Unit** dialog box, do the following:

    1.  In the **Storage pool** box, select a pool from the drop-down list.

    2.  In the **Name** box, enter a name.

    3.  In the **Description** box, enter a description.

    4.  In the **Size** box, enter a storage value in GB.

    5.  Click a radio button to create either a thin or fixed size logical unit.

    6.  When complete, click **OK**.

## <a name="BKMK_RegLun"></a>To register a storage LUN

1.  Open the **VMs and Services** workspace.

2.  In the **VMs and Services** pane, right-click the applicable VM and then click **Properties**.

3.  On the **Properties** page, click the **Storage** tab.

4.  Click **Add** and then click **Add Disk**.

5.  On the **Create Logical Unit** page, do the following:

    -   Next to **Storage pool**, select a pool from the drop-down list.

    -   In **Name**, enter a name for the LUN.

    -   In **Size**, enter a storage size in GB.

6.  When complete, click **OK**. The LUN is now registered (unmasked).

## See Also
[Managing Virtual Fibre Channel fabrics with VMM](Managing-Virtual-Fibre-Channel-fabrics-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



