---
ms.assetid: 979fc81c-b946-47ab-8ddb-50e53478d3f4
title: Set up networking for Hyper-V hosts and clusters in the VMM fabric
description: This article describes how to set up networking for Hyper-V hosts and clusters in the VMM fabric
author: rayne-wiselman
ms.author: raynew
manager: carmonm
ms.date: 11/01/2017
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
---


# Set up networking for Hyper-V hosts and clusters in the VMM fabric

Read this article to set up network settings for Hyper-V hosts and clusters in the System Center - Virtual Machine Manager (VMM) compute fabric.

You can apply network settings to a Hyper-V host or cluster using a logical switch. Applying a logical switch ensure that logical networks, and other network settings, are consistently assigned to multiple physical network adapters.

## Before you start

- If you want to configure network settings manually ensure you've set up logical networks before you begin. In addition make sure that the network sites within your logical networks are configured to use the host group of the host you want to assign them to. Check this in **Fabric** > **Servers** > **All Hosts**, and click the host group. In **Hosts**, click the host > **Properties**.
- If you want to use a logical switch you need to create the logical switch and port profiles.

## Configure network settings with a logical switch

To do this you'll need to [configure the logical switch](network-switch.md) and [port profiles](network-port-profile.md) you'll apply. Then you need to indicate what the physical network adapter is used for, and configure network settings by applying a logical switch. The network adapters that you configure can be physical or virtual adapters on the hosts.

## Specify what the network adapter is used for

Regardless of any port profiles and logical switches you are using in your network configuration, you must specify whether a network adapter in a host is used for virtual machines, host management, neither, or both. (The host must already be under management in VMM.)

1. Open  **Fabric** > **Servers** > **All Hosts** > host-group-name > **Hosts** > **Host** > **Properties** > **Hardware**.
1. Under **Network adapters**, click the physical network adapter that you want to configure.
    - If you want to use this network adapter for virtual machines, ensure that **Available for placement** is checked.
    - If you want to use this network adapter for communication between the host and the VMM management server, ensure that **Used by management** is checked. You must make sure that you have at least one network adapter available for communication between the host and the VMM management server.
1. You don't need to configure individual settings in **Logical network connectivity** because you're using a switch.

## Apply a logical switch

1. Open  **Fabric** > **Servers** > **All Hosts** > *host group* > **Hosts** > **Host** > **Properties** > **Virtual Switches**.
1. Select the logical switch you created. Under **Adapter**, select the physical adapter that you want to apply the logical switch to.
1. In the **Uplink Port Profile** list, select the uplink port profile that you want to apply. The list contains the uplink port profiles that have been added to the logical switch that you selected. If a profile seems to be missing, review the configuration of the logical switch and then return to this property tab. Click **OK** to finish. Note that if you didn't create the virtual switch earlier and do in now, the host might temporarily lose network connectivity when VMM creates the switch.
1. Repeat the steps as needed. If you apply the same logical switch and uplink port profile to two or more adapters, the two adapters might be teamed, depending on a setting in the logical switch. To find out if they will be teamed, open the logical switch properties, click the **Uplink** tab, and view the **Uplink mode** setting. If the setting is **Team**, the adapters will be teamed. The specific mode in which they will be teamed is determined by a setting in the uplink port profile.
1. After applying the logical switch you can check that the network adapter settings and verify whether they're in compliance with the switch:
    - Click **Fabric**> **Networking** > **Logical Switches** > **Home** > **Show** > **Hosts**.
    - In **Logical Switch Information for Hosts** verify the settings. **Fully compliant** indicates that the host settings are compliant with the logical switch. **Partially compliant** indicates some issues. Check the reasons in **Compliance errors**. **Non compliant** indicates that none of the IP subnets and VLANs defined for the logical network are assigned to the physical adapter. Click the switch > **Remediate** to fix this.
    - If you have a cluster, check each node.

::: moniker range=">=sc-vmm-1807"

## Monitor physical network devices

VMM supports Link Layer Discovery Protocol (LLDP). You can now leverage the LLDP information to remotely monitor physical network device properties and information. You can view this information by using VMM console and PowerShell.

**Console view**

To get the details of network devices from the VMM console, go to **View** > **Host** > **Properties** > **Hardware Configuration** > **Network adapter**.   

> [!NOTE]
> The details displayed contain a time stamp (updated on). To get the current details, refresh the page.

  ![lldp support](media/lldp-support/lldp-view.png)

The following LLDP information is displayed:

|**Information displayed** | **Description**
| --- | --- |
| Chassis ID <br/><br/> | Switch chassis ID |
| Port ID <br/><br/> | Switch port to which NIC is connected |
| Port Description <br/><br/> | Details related to the  port such as *Type*|
| System Name	Manufacturer <br/><br/> | Manufacturer, Software version details |
| System Description <br/><br/> | Detailed system description |
| Available Capabilities <br/><br/> | Available system capabilities (such as switching, routing) |
| Enabled Capabilities <br/><br/> | Enabled system capabilities (such as switching, routing) |
| VLAN ID <br/><br/> | Virtual LAN identifier |
| Management Address <br/><br/> | IP management address |

**PowerShell**

Use the following PowerShell command to view/refresh the LLDP details:

```powershell
Set-SCVMHostNetworkAdapter -RefreshLLDP
```

> [!NOTE]
>
> By default, LLDP Packet wait time is set as 30 seconds. You can modify this value by modifying the registry key at **Software\Microsoft\Microsoft System Center Virtual Machine Manager Server\Settings\LLdpPacketWaitIntervalSeconds**. The minimum value you can set is 5 seconds, maximum value is 300 seconds.

  ::: moniker-end


## Next steps

[Set up storage](hyper-v-storage.md) for Hyper-V hosts.
