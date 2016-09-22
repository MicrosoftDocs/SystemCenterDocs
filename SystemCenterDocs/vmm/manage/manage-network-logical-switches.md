---
title: Create logical switches
description: This article describes how to create logical switches in the VMM fabric
author:  rayne-wiselman
ms-author: raynew
manager:  cfreemanwa
ms.date:  2016-09-22
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Create logical switches

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes how to create logical switches in the System Center 2016 - Virtual Machine Manager (VMM) fabric, and to set up virtual switch extensions if you need them.

## Overview

A logical switch brings virtual switch extensions, port profiles, and port classifications together so that you can configure each network adapter with the settings you need, and have consistent settings on network adapters across multiple hosts. You can team multiple network adapters by applying the same logical switch and uplink port profile to them.  


## Set up virtual switch extensions

You install switch extensions on the VMM server and then include them in a logical switch. There are a few types of switch extensions:

- **Monitoring extensions** can be used to monitor and report on network traffic, but they cannot modify packets.
- **Capturing extensions** can be used to inspect and sample traffic, but they cannot modify packets.
- **Filtering extensions** can be used to block, modify, or defragment packets. They can also block ports.
- **Forwarding extensions** can be used to direct traffic by defining destinations, and they can capture and filter traffic. To avoid conflicts, only one forwarding extension can be active on a logical switch.

You can set up a virtual switch extension manager (network manager) if you want to managed extensions using a vendor management console and the VMM console together.

### Set up a virtual switch extension manager

1. Obtain the provider software from your vendor and install the provider on the VMM management server. If you have a cluster install it on all nodes.
2. Click **Fabric** > **Home** > **Show** > **Fabric Resources** > **Networking** > **Switch Extension Managers**.
3. In **Add Virtual Switch Extension Manager Wizard** > **General** specify the manufacturer and type the connection string for example myextmanager1.contosol.com:443. The exact syntax is defined by the vendor. Specify the account you want to use to connect to the resource.
4.  In **Host Groups** specify the host groups for which you want to use the extension manager.
5.  In **Summary** review settings and click **Finish**. Check that the extension appears in the **Virtual Switch Extension Managers** pane.


## Set up a logical switch

1. Make sure you have at least one uplink port profile before you begin.
2. Click **Fabric** tab > **Networking** > **Logical Switches** > **Create Logical Switch**.
3. In **Create Logical Switch Wizard** > **Getting Started**, review the information.
4. In **General**, specify a name and optional description.
5. In **Uplink Mode**, select:
	- **No Uplink Team** if you're not using teaming.
	- **Embedded Team** if you want to deploy the switch with SET-based teaming
	- **Team** if you want to use NIC teaming
6. In **Settings**, select the minimum bandwidth mode. If you've deployed Microsoft network controller, you can specify that it should manage the switch. If you enable this setting you won't be able to add extensions to the switch.
7. Enable SR-IOV if you need to. SR-IOV enables virtual machines to bypass the switch and directly address the physical network adapter. If you want to enable:

	- Make sure that you have SR-IOV support in the host hardware and firmware, the physical network adapter, and drivers in the management operating system and in the guest operating system.
	- Create a native port profile for virtual network adapters that is also SR-IOV enabled.
	- When you configure networking settings on the host (in the host property called Virtual switches), attach the native port profile for virtual network adapters to the virtual switch by using a port classification. You can use the SR-IOV port classification that is provided in VMM, or create your own port classification.
4. In **Extensions**, if you're using virtual switch extensions select them and arrange the order. extensions process network traffic through the switch in the order you specify. Note that only one forwarding extension can be enabled.
5. In **Virtual Port** add one or more port classifications and virtual network adapter port profiles. You can also create a port classification and set a default classification.
6. In **Uplink** add an uplink port profile, or [create a new one](manage-network-port-profiles.md). When you add an uplink port profile, it is placed in a list of profiles that are available through that logical switch. However, when you apply the logical switch to a network adapter in a host, the uplink port profile is applied to that network adapter only if you select it from the list of available profiles.
7. In **Summary** review the settings and click **Finish**. Verify the switch appears in **Logical Switches**.

## Next steps

[Apply network settings](manage-compute-add-networking-hyper-v.md) on a host with a logical switch.
