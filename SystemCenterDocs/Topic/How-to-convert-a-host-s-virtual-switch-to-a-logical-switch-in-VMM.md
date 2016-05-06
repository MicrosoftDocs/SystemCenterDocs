---
title: How to convert a host&#39;s virtual switch to a logical switch in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cabe44ea-905d-42f0-ab25-5d21a7af5875
---
# How to convert a host&#39;s virtual switch to a logical switch in VMM
If a host that you're managing with [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] has a standard virtual switch configuration, you can convert the configuration to use a logical switch.

Logical switches \(and the port profiles inside them\) act as templates or containers for the switch settings and capabilities that you want to use. Instead of configuring switch settings individually for each network adapter, you can specify the settings and capabilities in a logical switch, and then use the logical switch to apply those settings consistently across network adapters on multiple hosts.

> [!IMPORTANT]
> Before you can convert the configuration of the host to use a logical switch, you must have an appropriate logical switch, and it must match certain settings in the existing standard virtual switch, as described in this topic.

Do the tasks in this topic in this order:

1.  [Compare important settings in an existing virtual switch with settings in a logical switch](../Topic/How-to-convert-a-host-s-virtual-switch-to-a-logical-switch-in-VMM.md#BKMK_compare)

2.  [Convert a host from using a standard virtual switch to using a logical switch](../Topic/How-to-convert-a-host-s-virtual-switch-to-a-logical-switch-in-VMM.md#BKMK_convert)

**Account requirements** To complete these procedures, you must be a member of the Administrator user role or a member of the Delegated Administrator user role where the management scope includes the host group where the Hyper\-V host is located.

## <a name="BKMK_compare"></a>Compare important settings in an existing virtual switch with settings in a logical switch
To prepare for converting to a logical switch, review the settings in the following procedure.

#### To compare important settings in an existing virtual switch with settings in a logical switch that you want to convert to

1.  On the host, in Server Manager, in the console tree, click **Hyper\-V**.

2.  Under **SERVERS**, right\-click the host and then click **Configure NIC Teaming**.

3.  Record the information under **TEAMS** \(if there are any teams\), including **Teaming Mode** and **Load Balancing** information.

4.  Close the **NIC Teaming** dialog box.

5.  Still on the host, in Hyper\-V Manager \(not [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]\), right\-click the host and then click **Virtual Switch Manager**.

6.  In the **Virtual Switch Manager** dialog box, select the virtual switch, and in the results pane, see whether **Enable single\-root I\/O virtualization \(SR\-IOV\)** is selected. Record this information.

7.  Close the **Virtual Switch Manager** dialog box, and then close Hyper\-V Manager.

8.  Start the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console, and then open the **Fabric** workspace.

9. In the **Fabric** pane, expand **Servers** > **All Hosts**.

10. Navigate to the host, right\-click it, and click **Properties**.

11. In the **Properties** dialog box, click the **Virtual Switches** tab.

12. Make note of these virtual switch properties:

    -   **Logical network**

    -   **Minimum bandwidth mode**

13. Still in the **Fabric** workspace, on the **Home** tab, in the **Show** group, click **Fabric Resources**.

14. In the **Fabric** pane, expand **Networking** > **Logical Switches**.

15. In the **Logical Switches** pane, right\-click the logical switch that you want to convert the host configuration to, and then click **Properties**.

16. Record the following information from the property tabs:

    |Tab|Item to record|
    |-------|------------------|
    |**General**|-   **Uplink mode**<br />-   **Enable single\-root I\/O virtualization \(SR\-IOV\)**: checked or unchecked<br />-   **Minimum bandwidth mode**|
    |**Extensions**|Note whether any forwarding extensions have been added to the logical switch.|
    |**Virtual port**|Record the names of the port profiles that are listed. Be sure to note if one of them has SR\-IOV in the name.|
    |**Uplinks**|<ul><li>**Network sites**</li><li>If the **Uplink mode** \(on the **General** tab\) is **Teamed**, note the teaming settings:<br /><br /><ul><li>**Load balancing algorithm**</li><li>**Teaming mode**</li></ul></li></ul>|

17. Close the properties dialog box for the logical switch.

18. In the **Fabric** pane, under **Networking**, click **Port Profiles**.

19. For one of the virtual network adapter port profiles that were listed in the logical switch, right\-click the port profile, and then click **Properties**. On the **Offload Settings**, see if **Enable Single\-root I\/O virtualization** is checked, then close the port profile. Repeat this step for the other port profiles in the logical switch.

20. Compare the information that you recorded for the logical switch and port profiles with the virtual switch information \(the information that you recorded in other parts of the interface\). Review the following table to see whether you can convert the configuration of this host to use the logical switch:

    |Item|Required result of comparison between virtual switch and logical switch|
    |--------|---------------------------------------------------------------------------|
    |**SR\-IOV** setting|The SR\-IOV setting \(enabled or disabled\) must be the same in the logical switch as it is in the virtual switch. If SR\-IOV is enabled, it must be enabled in the logical switch itself and in at least one virtual network adapter port profile within the logical switch.|
    |**Uplink mode**<br /><br />**Load balancing algorithm**<br /><br />**Teaming mode**|The **Uplink mode** setting must match.<br /><br />If the uplink mode is **Team**, the **Load balancing algorithm** and **Teaming mode** must also match.|
    |**Minimum bandwidth mode**|Must match.|
    |**Network sites**|The logical switch must be configured for the correct network sites \(in the correct logical network\) for this host.|

21. If the settings in the logical switch do not match the virtual switch in the ways listed in the preceding table, locate or create a logical switch that does match. For information about creating a logical switch, see:

    -   [Overview: plan logical switches and port profiles in VMM](../Topic/Overview--plan-logical-switches-and-port-profiles-in-VMM.md)

    -   [How to create a logical switch in VMM](../Topic/How-to-create-a-logical-switch-in-VMM.md)

## <a name="BKMK_convert"></a>Convert a host from using a standard virtual switch to using a logical switch
After you use the preceding procedure to confirm the settings in the logical switch that you want to convert to, you can do the conversion. The conversion will not interrupt network traffic. If any operation in the conversion fails, no settings will be changed, and the switch will not be converted. If the conversion fails, please see the tables in [Compare important settings in an existing virtual switch with settings in a logical switch](#BKMK_compare), earlier in this topic.

#### To convert a host from using a standard virtual switch to using a logical switch

1.  In [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers** > **All Hosts**.

3.  Navigate to the host, right\-click it, and click **Properties**.

4.  In the **Properties** dialog box, click the **Virtual Switches** tab.

5.  If needed, scroll to the bottom of the tab. If the **Convert to Logical Switch** button is dimmed, use the first procedure in this topic to ensure that you have a logical switch that matches important settings in the virtual switch. Otherwise, continue.

6.  Click **Convert to Logical Switch**.

7.  In the dialog box, select the logical switch that you want to convert the host to. Then select the uplink port profile to use.

8.  Click **Convert**.

    The **Jobs** dialog box might appear, depending on your settings. Make sure that the job has a status of **Completed**, and then close the dialog box.

9. To verify that the switch was converted, right\-click the host, click **Properties**, and then click the **Virtual Switches** tab.

## See Also
[Configuring logical networks, VM networks, and logical switches in VMM](../Topic/Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](../Topic/Managing-network-resources-with-VMM.md)

