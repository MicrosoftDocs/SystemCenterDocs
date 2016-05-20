---
title: How to manage vSANs and vHBAs with VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a64b46b0-5ce6-435a-8de6-70a86c2b0ff5
---
# How to manage vSANs and vHBAs with VMM
A virtual storage area network \(vSAN\) is a named group of physical Fibre Channel Host Bus Adapter \(HBA\) ports on a host computer that a VM connects to in order to access Fibre Channel storage devices. One or more vSANs can be created for each host computer. Each vSAN can only contain HBAs that are from the same fabric.

Virtual Host Bus Adapters \(vHBAs\) represent the virtualization of Fibre Channel HBAs, and are used by VMs to connect with vSANs. Each vHBA has a World Wide Node Name \(WWNN\), which is different than the host HBA WWNN.

Using N\_Port ID Virtualization \(NPIV\), a host computer HBA can map to multiple vHBAs. HBA ports assigned to a vSAN can be added or removed as needed.

Use the following procedures to manage vSANs with [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)]:

-   [To create a vSAN and assign HBAs to it](#BKMK_CreateVSAN)

-   [To edit vSAN port assignments](#BKMK_EditPort)

-   [To remove a vSAN from a host computer](#BKMK_RemoveVSAN)

-   [To add a new vHBA and assign it to a vSAN](#BKMK_AddVHBA)

-   [To change the default port settings for vHBAs](#BKMK_PortSettings)

## <a name="BKMK_CreateVSAN"></a>To create a vSAN and assign HBAs to it

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, right\-click the applicable host, and then click **Properties**.

3.  On the **Properties** page, click the **Hardware** tab, then click **New Virtual SAN**, and do the following:

    1.  In the **Name** box, enter a name for the vSAN.

    2.  In the **Description** box, enter a description for the vSAN.

    3.  Under **Fibre Channel adapters**, select the check boxes next to the Fibre Channel adapters \(HBAs\) that you want to assign to the vSAN.

    4.  When completed, click **OK**.

## <a name="BKMK_EditPort"></a>To edit vSAN port assignments

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, right\-click the applicable host, and then click **Properties**.

3.  On the **Properties** page, click the **Hardware** tab, and then scroll down to **FC Virtual SAN**.

4.  Under **Fibre Channel adapter details**, select or unselect the applicable check boxes next to the HBA ports listed.

## <a name="BKMK_RemoveVSAN"></a>To remove a vSAN from a host computer

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, right\-click the applicable host, and then click **Properties**.

3.  On the **Properties** page, click the **Hardware** tab, and then scroll down to **FC Virtual SAN**.

    > [!NOTE]
    > Before you remove a vSAN, remove any vHBAs attached to the vSAN.

4.  Right\-click the applicable vSAN, click **Delete**, and then click **OK**.

## <a name="BKMK_AddVHBA"></a>To add a new vHBA and assign it to a vSAN

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, right\-click the applicable host, and then click **Properties**.

3.  On the **Properties** page, click the **Hardware Configuration** tab, click **New**, click **Fibre Channel Adapter**, and then do the following:

    1.  In the **Virtual SAN name** box, select a vSAN from the drop\-down list to assign to the vHBA.

    2.  If you want to dynamically assign the range of port settings for the vHBA, click **Dynamically assign World Wide Names**.

    3.  If you want to statically assign port settings for the vHBA, click **Statically assign World Wide Names**, and then enter primary and secondary WWNN and WWPN port settings for the vHBA.

    4.  When completed, click **OK**.

## <a name="BKMK_PortSettings"></a>To change the default port settings for vHBAs

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, right\-click the applicable host, and then click **Properties**.

3.  On the **Properties** page, click the **Hardware** tab, and then scroll down to **Global FC settings**.

4.  Under **Fibre Channel adapter details**, do the following:

    1.  In the **Minimum** box, enter the lowest WWPN port setting.

    2.  In the **Maximum** box, enter the highest WWPN port setting.

    3.  In the **World Wide Node Name** box, enter a name.

    4.  When completed, click **OK**.

    > [!IMPORTANT]
    > Changing these settings does not affect vHBA ports that have already been created. To apply a new setting to an existing vHBA port, recreate the port by removing it and then adding it again.

## See Also
[Managing Virtual Fibre Channel fabrics with VMM](Managing-Virtual-Fibre-Channel-fabrics-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


