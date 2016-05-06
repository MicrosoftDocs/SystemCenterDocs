---
title: How to manage Virtual Fibre Channel zones and zonesets with VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3633a09-a9ec-42ce-9774-185679502839
---
# How to manage Virtual Fibre Channel zones and zonesets with VMM
Zones are used to connect a Fibre Channel array to a host computer or virtual machine \(VM\). Specifically, the storage array target ports are mapped to the HBA ports on the host or to the virtual HBA \(vHBA\) ports for the VM. The HBA and vHBA ports are referred to as initiator ports. The zoning process is also known as onboarding.

You can create zones for a host, a VM, or both. For Hyper\-V failover clusters, a zone is needed for each host computer in the cluster.

Zones are grouped into zonesets, which use common Fibre Channel fabric devices. When all zones in a zone set have been added, modified, or removed as needed, the zoneset must be activated. Zoneset activation pushes information for each zone down to the Fibre Channel switches in the selected fabric.

Only members of the same zone can communicate with each other.

Use the following procedures to create new zones and then activate the zoneset. If you want to add a storage array to a Hyper\-V cluster, you need to zone the array to each host computer first. Similarly, if you want to add an array to a guest cluster, you need to zone the array to each VM first.

1.  [To create a new zone](#BKMK_CreateZone)

2.  [To activate a zoneset](#BKMK_ActivateZoneset)

    > [!NOTE]
    > Activating a zoneset may cause some downtime in the fabric as information is propagated to all the switches.

Use the following procedures to view the zonesets associated with a fabric, edit zone information, or remove a zone from a zoneset.

-   [To view the zonesets for a fabric](#BKMK_ViewZonesets)

-   [To edit the zone name and description or to remove a zone](#BKMK_EditZone)

-   [To edit storage array zoning](#BKMK_Editzoning)

## <a name="BKMK_CreateZone"></a>To create a new zone

1.  Open the **VMs and Services** workspace.

2.  In the **Services** pane, right\-click the applicable VM, and then click **Properties**.

3.  On the **Properties** page, click the **Storage** tab, click **Add**, and then click **Add Fibre Channel Array**.

4.  On the **Create New Zone** dialog box, do the following:

    1.  In the **Zone Name** box, enter a name for the zone.

    2.  In the **Storage Array** box, select an array from the drop\-down list.

    3.  In the **Fabric** box, select a switch from the drop\-down list.

    4.  Under **Storage array target ports**, select the applicable WWPM port or ports.

    5.  Under **Virtual machine initiator**, select the applicable WWPM port or ports.

    6.  When complete, click **Create**.

    7.  To view zone aliases in the user interface that are available for selection, click **Show aliases**.

## <a name="BKMK_ActivateZoneset"></a>To activate a zoneset

1.  Open the **Fabric** workspace.

2.  Under **Name**, click the applicable inactive zoneset and then on the **Home** tab, click **Activate Zoneset**.

## <a name="BKMK_ViewZonesets"></a>To view the zonesets for a fabric

1.  Open the **Fabric** workspace, and then click **Fibre Channel Fabric**.

2.  Under **Name**, right\-click the applicable fabric, and then click **Properties**.

3.  On the **Properties** page, click the **Zonesets** tab.

## <a name="BKMK_EditZone"></a>To edit the zone name and description or to remove a zone

1.  Open the **Fabric** workspace.

2.  Under **Name**, right\-click the applicable zoneset, and then click **Properties**.

3.  On the **Properties** page, click the **Zones** tab.

4.  To edit a zone in a zoneset, click **Edit**, and change the zone name and description as needed.

5.  To remove a zone from a zoneset, click **Remove**, click **Yes**, and then click **OK**.

## <a name="BKMK_Editzoning"></a>To edit storage array zoning

1.  Open the **VMs and Services** workspace.

2.  In the **VMs and Services** pane, right\-click the applicable host, and then click **Properties**.

3.  On the **Properties** page, click the **Storage** tab.

4.  Under **Storage**, scroll down to **Fibre Channel Arrays**, click **Edit**, click the applicable array, and then do the following:

    1.  Click **Modify zoning** to edit zoning information.

    2.  Click **View existing zoning** to view zoning information.

    3.  Click **New** to assign the storage array to a new zone.

5.  When complete, click **OK**.

## See Also
[Managing Virtual Fibre Channel fabrics with VMM](./Managing-Virtual-Fibre-Channel-fabrics-with-VMM.md)
[Managing storage resources and capacity with VMM](./Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](./Managing-fabric-resources-with-VMM.md)


