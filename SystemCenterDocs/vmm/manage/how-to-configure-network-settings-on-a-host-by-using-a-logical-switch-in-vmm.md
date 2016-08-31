---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to configure network settings on a host by using a logical switch in VMM
ms.technology:  virtual-machine-manager
ms.assetid:  06b231a6-4587-4e91-887e-583c0f1e380a
---

# How to configure network settings on a host by using a logical switch in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

With Virtual Machine Manager (VMM), you can configure network adapters on Hyper-V hosts by applying the settings in a logical switch to the adapters. The network adapters that you configure can be physical network adapters or virtual network adapters on the hosts.

For other ways of configuring network adapters on a host, see the links at the end of this topic.

Do the tasks in this topic in this order:

1.  [Specify whether a network adapter is used for virtual machines, host management, neither, or both](How-to-configure-network-settings-on-a-host-by-using-a-logical-switch-in-VMM.md#BKMK_use)

2.  [Configure network settings on a host by using a logical switch](How-to-configure-network-settings-on-a-host-by-using-a-logical-switch-in-VMM.md#BKMK_apply)

After you perform the procedures in this topic, as a best practice, review the procedures in [How to bring host network adapters into compliance with logical switch settings in VMM](How-to-bring-host-network-adapters-into-compliance-with-logical-switch-settings-in-VMM.md).

**Account requirements** To complete these procedures, you must be a member of the Administrator user role or a member of the Delegated Administrator user role where the management scope includes the host group where the Hyper-V host is located.

## <a name="BKMK_use"></a>Specify whether a network adapter is used for virtual machines, host management, neither, or both
Regardless of any logical switches you are using in your network configuration, you must specify whether a network adapter in a host is used for virtual machines, host management, neither, or both. (The host must already be under management in VMM.)

#### To specify whether a network adapter is used for virtual machines, host management, neither, or both

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers** > **All Hosts**.

3.  Navigate to the host, right-click it, and click **Properties**.

4.  In the **Properties** dialog box, click the **Hardware** tab.

5.  Under **Network adapters**, click the physical network adapter that you want to configure. If you want to use this network adapter for virtual machines, ensure that **Available for placement** is checked. If you want to use this network adapter for communication between the host and the VMM management server, ensure that **Used by management** is checked.

> [!IMPORTANT]
> -   You must make sure that you have at least one network adapter available for communication between the host and the VMM management server. Make sure that **Used by management** is checked for this network adapter.
> -   If you have already applied a logical switch and an uplink port profile to a network adapter, if you click **Logical network connectivity**, you can see the resulting connectivity. However, if you plan to apply a logical switch and an uplink port profile, do not make individual selections in **Logical network connectivity**. Instead, use the following procedure.

## <a name="BKMK_apply"></a>Configure network settings on a host by using a logical switch
Before you begin the following procedure, make sure you have configured the building blocks that are needed in the procedure, including logical networks, VM networks, and logical switches. For more information, see [Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md).

#### To configure network settings on a host by using a logical switch

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers** > **All Hosts**.

3.  Navigate to the host, right-click it, and click **Properties**.

4.  In the **Properties** dialog box, click the **Virtual Switches** tab.

5.  On the **Virtual Switches** tab, do the following:

    1.  Select an existing logical switch from the list, or click **New Virtual Switch** and then click **New Logical Switch**.

    2.  In the **Logical switch** list, select the logical switch that you want to use.

    3.  Under **Adapter**, select the physical adapter that you want to apply the logical switch to.

    4.  In the **Uplink Port Profile** list, select the uplink port profile. The list contains the uplink port profiles that have been added to the logical switch that you selected. If a profile seems to be missing, review the configuration of the logical switch and then return to this property tab.

    5.  Review the information about the virtual network adapters that will be created. These virtual network adapters have been configured within the logical switch.

    6.  As needed, repeat the steps for an additional logical switch.

        > [!IMPORTANT]
        > If you use the same logical switch and uplink port profile for two or more adapters, the two adapters might be teamed, depending on a setting in the logical switch. To find out if they will be teamed, open the logical switch properties, click the **General** tab, and view the **Uplink mode** setting. If the setting is **Team**, the adapters will be teamed. To see additional teaming settings, click the **Uplinks** tab. The teaming settings are described in [Load-balancing algorithm](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_algorithm) and [Teaming mode](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_teaming) in "Overview: plan logical switches and port profiles in VMM."

    7.  When you have finished configuring settings, click **OK**.

        > [!CAUTION]
        > While VMM creates the virtual switch, the host may temporarily lose network connectivity. This may have an adverse effect on other network operations in progress.

The following tips may also be useful:

> [!TIP]
> **Network optimizations**: VMM can detect whether the operating system on your host provides the network optimizations called Virtual Machine Queue (VMQ) or TCP Chimney Offload. If VMM detects either of them, it displays a message saying **Network optimization is available**. Look for the message in the **Host Properties** dialog box, on the **Virtual Switches** tab.

> [!TIP]
> **Compliance of network settings**: If you're using logical switches, you can later check to see if the network adapter settings on a host are still in compliance with the logical switch settings. If they"re not, you can use VMM to bring them back into compliance. For more information, see [How to bring host network adapters into compliance with logical switch settings in VMM](How-to-bring-host-network-adapters-into-compliance-with-logical-switch-settings-in-VMM.md).

## See Also
[How to configure network settings on a Hyper-V host in VMM](How-to-configure-network-settings-on-a-Hyper-V-host-in-VMM.md)
[Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)
[Bare Metal Deploy through VMM PowerShell (Part 1)](http://blogs.technet.com/b/privatecloud/archive/2013/02/22/bare-metal-deploy-through-vmm-powershell-part-1.aspx)
[Bare Metal Deploy through VMM PowerShell (Part 2)](http://blogs.technet.com/b/privatecloud/archive/2013/03/04/bare-metal-deploy-through-vmm-powershell-part-2.aspx)
[Hyper-V Host Network Settings through VMM PowerShell (Part 3)](http://blogs.technet.com/b/privatecloud/archive/2013/05/20/hyper-v-host-network-settings-through-vmm-powershell-part-3.aspx)



