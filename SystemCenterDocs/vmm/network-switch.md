---
ms.assetid: 15be7169-be12-4047-b1fd-fe6ad4b2fdc1
title: Create logical switches
description: This article describes how to create logical switches in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  07/20/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Create logical switches

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes how to create logical switches in the System Center 2016 - Virtual Machine Manager (VMM) fabric, convert a host virtual switch to a logical switch, and set up virtual switch extensions if you need them.

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
3. In **Add Virtual Switch Extension Manager Wizard** > **General** specify the manufacturer and type the connection string for example myextmanager1.contoso.com:443. The exact syntax is defined by the vendor. Specify the account you want to use to connect to the resource.
4. In **Host Groups** specify the host groups for which you want to use the extension manager.
5. In **Summary** review settings and click **Finish**. Check that the extension appears in the **Virtual Switch Extension Managers** pane.


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
6. In **Uplink** add an uplink port profile, or [create a new one](network-port-profile.md). When you add an uplink port profile, it is placed in a list of profiles that are available through that logical switch. However, when you apply the logical switch to a network adapter in a host, the uplink port profile is applied to that network adapter only if you select it from the list of available profiles.
7. In **Summary** review the settings and click **Finish**. Verify the switch appears in **Logical Switches**.

## Convert virtual switch to logical switch

If a host in the VMM fabric has a standard virtual switch, you can convert it to use a logical switch.

Note that:

- Before you can convert, you need a logical switch in place, with specific settings.
- You must be a member of the Administrator user role, or a member of the Delegated Administrator user role, where the management scope includes the host group in which the Hyper-V host is located.

### Compare switch settings

1. In **Server Manager** on the host,  click **Hyper-V**. Close Server Manager.
2. Right-click the host >  **Configure NIC Teaming**, and record any teaming and load balancing settings.
3. In **Hyper-V Manager**, right-click the host > **Virtual Switch Manager**. Select the virtual switch and verify whether **Enable single-root I/O virtualization (SR-IOV)** is selected. Close Hyper-V Manager.
4. In the VMM console > **Fabric** > **Servers** > **All Hosts**, right-click the host > **Properties**.
5. In **Virtual Switches**, note the properties, including logical network, and minimum bandwidth mode.
6. In **Fabric** > **Networking** > **Logical Switches**, right-click the logical switch that you want to convert the host configuration to, and click **Properties**.
7. In **Logical Switches**, record the information:
    - In **General**, record the uplink mode, whether SR-IOV is enable, and minimum bandwidth mode.
    - In **Extensions**, note whether any forwarding extensions have been added to the logical switch.
    - In **Virtual port**, record the names of the port profiles that are listed. Be sure to note if one of them has SR-IOV in the name.
    - In **Uplinks**, record the network sites, whether uplink mode is teamed, the load balancing algorithm, and teaming mode.

8. In **Fabric** > **Networking**, click **Port Profiles**. For any relevant port profiles, click **Properties**. In **Offload Settings**, see if **Enable Single-root I/O virtualization** is checked.
9. Now compare the recorded information that you recorded for the logical switch and port profiles, with the virtual switch information.
10. Review the following table to see whether you can convert the host to use the logical switch.

    Item | Conversion
    --- |---
    **SR-IOV** |The SR-IOV setting (enabled or disabled) must be the same in the logical switch as it is in the virtual switch.<br/><br/> If SR-IOV is enabled, it must be enabled in the logical switch itself, and in at least one virtual network adapter port profile within the logical switch.
    **Uplink mode**<br/><br/> **Load balancing algorithm**<br /><br /> **Teaming mode** | The **Uplink mode** setting must match.<br /><br /> If the uplink mode is **Team**, then the **Load balancing algorithm** and **Teaming mode** must also match.
    **Minimum bandwidth mode** | Must match.
    **Network sites** | The logical switch must be configured for the correct network sites (in the correct logical network) for this host.

11. If the settings in the logical switch don't match as described in the table, you need to find or create a logical switch that does match.

### Convert a host to use a logical switch

> [!NOTE]

> - The following procedure is not applicable for SET, use the [script](#script-for-set-switch-conversion) instead.
> - The conversion will not interrupt network traffic.
> - If any operation in the conversion fails, no settings will be changed, and the switch will not be converted.


1. In VMM, click  **Fabric** > **Servers** > **All Hosts**. Right-click the host > **Properties**.
2. On the **Virtual Switches** tab, click **Convert to Logical Switch**.
3. Select the logical switch that you want to convert the host to. Then select the uplink port profile to use, and click **Convert**.
4. The **Jobs** dialog box might appear, depending on your settings. Make sure that the job has a status of **Completed**, and then close the dialog box.
5. To verify that the switch was converted, right-click the host, click **Properties**, and then click the **Virtual Switches** tab.

#### Script for SET switch conversion

> [!NOTE]

> Create a logical switch in VMM with the same name as the SET switch that is deployed on the host.
> Standard switch will be converted to this logical switch after you run the following script on the host.


```powershell
#Replace Virtual Switch name with already deployed switch name on host
$VirtualSwitchName="SETswitch"

#Replace logical switch ID below with the one got from Get-SCLogicalSwitch cmdlet for the switch created in VMM
$LogicalSwitchId="45b98a8d-1887-4431-9f20-8b9beed853ce"

#Replace port profile name with the one created associated with above logical switch in VMM
$PortProfileName="Mgmt_UPP"

#Replace uplink port profile set ID with the one got from Get-SCUplinkPortProfileSet for the port profile set created in VMM
$PortProfileSetId="fd9e4c9a-4ffa-4845-808d-930e6616b62f"

$vswitch=Get-VMSwitch -Name $VirtualSwitchName
$VMMPortFeatureId="1f59a509-a6ba-4aba-8504-b29d542d44bb"
$defaultPortFeature = Get-VMSystemSwitchExtensionPortFeature -FeatureId $VMMPortFeatureId
$VMMFeatureId="8b54c928-eb03-4aff-8039-99171dd900ff"
$currentFeature = Get-VMSwitchExtensionSwitchFeature -SwitchName $VirtualSwitchName -FeatureId $VMMFeatureId
$defaultFeature = Get-VMSystemSwitchExtensionSwitchFeature -FeatureId $VMMFeatureId
$defaultFeature.SettingData.LogicalSwitchId=$LogicalSwitchId
$defaultFeature.SettingData.LogicalSwitchName=$VirtualSwitchName
Add-VMSwitchExtensionSwitchFeature -SwitchName $VirtualSwitchName -VMSwitchExtensionFeature $defaultFeature

$defaultPortFeature = Get-VMSystemSwitchExtensionPortFeature -FeatureId $VMMPortFeatureId
$defaultPortFeature.SettingData.PortProfileSetId=$PortProfileSetId
$defaultPortFeature.SettingData.PortProfileSetName=$PortProfileName
$defaultPortFeature.SettingData.NetCfgInstanceId="{" + $vswitch.Id +"}"
Add-VMSwitchExtensionPortFeature -SwitchName $VirtualSwitchName -VMSwitchExtensionFeature $defaultPortFeature –ExternalPort
```

After you run the script, refresh the host in VMM and verify if VMM recognizes the switch as logical switch.

## Next steps

[Apply network settings](hyper-v-network.md) on a host with a logical switch.
