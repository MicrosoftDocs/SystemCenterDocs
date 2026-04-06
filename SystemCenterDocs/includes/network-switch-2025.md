---
ms.assetid: cc13696a-7a15-4899-9b6f-d38e9e03b32a
title: include file
description: This article describes how to create logical switches in the VMM fabric
author: Jeronika-MS
ms.author: v-gajeronika
ms.date:  08/21/2024
ms.topic:  include
ms.service:  system-center
ms.subservice:  virtual-machine-manager
ms.custom: engagement-fy24
ms.update-cycle: 1095-days
---

## How to create logical switches

This article describes how to create logical switches in the System Center Virtual Machine Manager (VMM) fabric, convert a host virtual switch to a logical switch, and set up virtual switch extensions if you need them.

A logical switch brings virtual switch extensions, port profiles, and port classifications together so that you can configure each network adapter with the settings you need and have consistent settings on network adapters across multiple hosts. You can team multiple network adapters by applying the same logical switch and uplink port profile to them.


## Set up virtual switch extensions

You install switch extensions on the VMM server and then include them in a logical switch. There are a few types of switch extensions:

- **Monitoring extensions** can be used to monitor and report on network traffic, but they can't modify packets.
- **Capturing extensions** can be used to inspect and sample traffic, but they can't modify packets.
- **Filtering extensions** can be used to block, modify, or defragment packets. They can also block ports.
- **Forwarding extensions** can be used to direct traffic by defining destinations, and they can also capture and filter traffic. To avoid conflicts, only one forwarding extension can be active on a logical switch.

You can set up a virtual switch extension manager (network manager) if you want to manage extensions using a vendor management console and the VMM console together.

### Set up a virtual switch extension manager

1. Obtain the provider software from your vendor and install the provider on the VMM management server. If you have a cluster, install it on all the nodes.
2. Select **Fabric** > **Home** > **Show** > **Fabric Resources** > **Networking** > **Switch Extension Managers**.
3. In **Add Virtual Switch Extension Manager Wizard** > **General**, specify the manufacturer and enter the connection string. For example, myextmanager1.contoso.com:443. The exact syntax is defined by the vendor. Specify the account you want to use to connect to the resource.
4. In **Host Groups**, specify the host groups for which you want to use the extension manager.
5. In **Summary**, review settings and select **Finish**. Check that the extension appears in the **Virtual Switch Extension Managers** pane.


## Set up a logical switch

>[!NOTE]
> Ensure you've at least one uplink port profile before you begin.

1. Select **Fabric** > **Networking**
2. Right-click **Logical Switches**, and then select **Create Logical Switch**.
3. In **Create Logical Switch Wizard** > **Getting Started**, review the information.
4. In **General**,
    - Specify a name
    - Provide a description (optional).
5. In **Uplink Mode**, select:
    - **Embedded Team** - if you're using Windows Server 2019 or later.
    - **No Uplink Team** - if you're not using any teaming.

    **Embedded Team** is the default Uplink mode.
6. In **Settings**, select the minimum bandwidth mode. If you've deployed Microsoft network controller, you can specify that it must manage the switch. If you enable this setting, you won't be able to add extensions to the switch.
    - **Weight** - Weight is the default minimum bandwidth mode. Weight specifies a percentage of bandwidth rather than a specific number of bits per second. Minimum bandwidth is a value ranging from 1 to 100.
    - **Default** - The system sets the mode to **Weight** if the switch isn't IOV enabled, or **None** if the switch is IOV enabled.
    - **Absolute** - Minimum bandwidth will be in bits per second.  
    - **None** - Minimum bandwidth is disabled on the switch. Users can't configure it on any network adapter that is connected to the switch.
7. Enable SR-IOV if you need to. SR-IOV enables virtual machines to bypass the switch and directly address the physical network adapter.
If you want to enable:
    - Ensure that you've SR-IOV support in the host hardware and firmware, the physical network adapter, and drivers in the management operating system and in the guest operating system.
    - Create a native port profile for virtual network adapters that is SR-IOV enabled.
    - When you configure networking settings on the host (in the host property called Virtual switches), attach the native port profile for virtual network adapters to the virtual switch by using a port classification. You can use the SR-IOV port classification that is provided in VMM or create your own port classification.
8. In **Extensions**, if you're using virtual switch extensions, select them and arrange the order. Extensions process network traffic through the switch in the order you specify. 

> [!NOTE]
> Only one forwarding extension can be enabled. None of the extensions are enabled by default.

9. In **Virtual Port**, add one or more port classifications and virtual network adapter port profiles. Every Port Classification must be mapped to a Port Profile. You can view Port Classification to Port Profile mapping on the **Virtual Port** screen.

10. In **Uplink**, add an uplink port profile, or [create a new one](../vmm/network-port-profile.md). When you add an uplink port profile, it's placed in a list of profiles that are available through that logical switch. However, when you apply the logical switch to a network adapter in a host, the uplink port profile is applied to that network adapter only if you select it from the list of available profiles.

    If *Uplink* is chosen as Embedded Team (Switch Embedded Team or SET), then only Hyper-V Port and Dynamic load balancing algorithms are supported. Hyper-V Port is the default load balancing algorithm. If *Uplink* mode is chosen as Embedded Team, then Hyper-V Port is the recommended load balancing algorithm; Dynamic isn't recommended.

11. In **Summary**, review the settings and select **Finish**. Verify if the switch created appears in **Logical Switches**.

## Convert virtual switch to logical switch

If a host in the VMM fabric has a standard virtual switch with or without SET, you can convert it to use as a logical switch.

> [!NOTE]
> - Before you can convert, you need a logical switch in place with specific settings.
> - You must be a member of the Administrator user role, or a member of the Delegated Administrator user role, where the management scope includes the host group in which the Hyper-V host is located.


### Compare switch settings

1.	Record if NIC Teaming (LBFO) or SET is being used on the host.
2.	If you're using NIC teaming on the host, record teaming and load balancing settings by running the PowerShell commandlet *Get-NetLbfoTeam*.
3. In **Hyper-V Manager**, right-click the host > **Virtual Switch Manager**. Select the virtual switch and verify whether **Enable single-root I/O virtualization (SR-IOV)** is selected. Close Hyper-V Manager.
4. In the VMM console > **Fabric** > **Servers** > **All Hosts**, right-click the host > **Properties**.
5. In **Virtual Switches**, note the properties, including logical network and minimum bandwidth mode.
6. In **Fabric** > **Networking** > **Logical Switches**, right-click the logical switch that you want to convert the host configuration to and select **Properties**.
7. In **Logical Switches**, record the information:
    - In **General**, record the uplink mode, whether SR-IOV is enabled, and minimum bandwidth mode.
    - In **Extensions**, note whether any forwarding extensions have been added to the logical switch.
    - In **Virtual port**, record the names of the port profiles that are listed. Ensure that you  note if one of them has SR-IOV in the name.
    - In **Uplinks**, record the network sites, whether uplink mode is teamed, the load balancing algorithm, and teaming mode.

8. In **Fabric** > **Networking**, select **Port Profiles**. For any relevant port profiles, select **Properties**. In **Offload Settings**, see if **Enable Single-root I/O virtualization** is checked.
9. Now compare the recorded information that you recorded for the logical switch and port profiles, with the virtual switch information.
10. Review the following table to see whether you can convert the host to use the logical switch.

    Item | Conversion
    --- |---
    **SR-IOV** |The SR-IOV setting (enabled or disabled) must be the same in the logical switch as it's in the virtual switch.<br/><br/> If SR-IOV is enabled, it must be enabled in the logical switch itself, and in at least one virtual network adapter port profile within the logical switch.
    **Uplink mode**<br/><br/> **Load balancing algorithm**<br /><br /> **Teaming mode** | The **Uplink mode** setting must match.<br /><br /> If the uplink mode is **Team**, then the **Load balancing algorithm** and **Teaming mode** must also match.
    **Minimum bandwidth mode** | Must match.
    **Network sites** | The logical switch must be configured for the correct network sites (in the correct logical network) for this host.

11. If the settings in the logical switch don't match as described in the table, you need to find or create a logical switch that does match.

### Convert a host to use a logical switch

> [!NOTE]
> - The conversion will not interrupt network traffic.
> - If any operation in the conversion fails, no settings will be changed, and the switch will not be converted.


1. In VMM, select **Fabric** > **Servers** > **All Hosts**. Right-click the host > **Properties**.
2. On the **Virtual Switches** tab, select **Convert to Logical Switch**.
3. Select the logical switch to which you want to convert the host. Select the uplink port profile to use and select **Convert**.
4. The **Jobs** dialog box might appear, depending on your settings. Ensure the job has a status of **Completed** and then close the dialog.
5. To verify that the switch was converted, right-click the host, select **Properties**, and then select the **Virtual Switches** tab.
