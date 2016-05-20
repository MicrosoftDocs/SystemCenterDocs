---
title: How to configure network settings on a Hyper-V host in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 80c630b1-ab1e-47be-83aa-478655b3dbcb
---
# How to configure network settings on a Hyper-V host in VMM

Configure network settings for Hyper-V hosts and clusters as follows:


1. Ensure you've [set up logical networks](https://technet.microsoft.com/library/mt238072.aspx) before you begin. In addition make sure that the network sites within your logical networks are configured to use the host group of the host you want to assign them to.
2. Assign logical networks to a physical network adapter on a host.
3. Configure settings for external, internal, and private virtual networks
4. If you want to consistently assign logical networks and other network settings to multiple physical network adapters across multiple hosts, you can configure network settings using a logical switch. 


## Assign logical networks to a physical network adapter on a host

1.  Open **Fabric** > **Servers** > **All Hosts** and click the host group.
2.  click **Hosts** > the host name > **Properties** > **Hardware**.
3.  Under **Network Adapters**, click the physical network adapter that you want to configure. If you want to use this network adapter for virtual machines, ensure that **Available for placement** is checked. If you want to use this network adapter for communication between the host and the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] management server, ensure that **Used by management** is checked. Make sure that you have at least one network adapter available for communication between the host and the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] management server. Make sure that **Used by management** is checked for this network adapter.
4.  Under the physical network adapter, click **Logical network connectivity**. Notice the various kinds of information displayed, such as the list of IP subnets and VLANs that are available. If you’ve added a top\-of\-rack \(TOR\) switch as a network service, port information that is provided by the switch might also be displayed.
5.  Review the list of logical networks, and take note of the following:

	- You might have to look fairly carefully at the entries in the list, because some of them might not actually be available for this host. The list is not limited to the logical networks with network sites that include the host group of this host. Instead, the list includes all the logical networks.
	
	- You might see some logical networks that appear to have been created automatically—this means that you added a host to [!INCLUDE[vmm12short](Token/vmm12short_md.md)] and the host didn’t already have logical networks assigned to its network adapters. However, automatic creation of logical networks depends on your global settings.

6.  Check the box next to each logical network that you want to assign to the physical adapter. For example, if you configured a logical network called **Management**, and that logical network is available to the host group of your host, check the box next to **Management**.

## Configure settings for external, internal, and private virtual networks

Control the types of connectivity available to virtual machines by using **External**, **Internal**, or **Private** settings \(more details about these settings are in the procedure\). Also use this procedure to configure host access through VLANs. You configure these settings through a host property called a virtual switch.


1.  Click **Fabric** > **Servers** > **All Hosts** > host group > **Hosts** > **Host** > **Properties**.
2.  In **Properties** click the **Virtual Switches** tab. Then click an existing virtual switch, or click **New Virtual Switch** and then click **New Standard Switch**. If you do not want to apply each setting individually \(that is, you do not want to use a standard switch\), you can configure network settings using a logical switch instead.
3.  In **Name** , enter a name, or accept the default.
4.  In the **Network binding** list, click the network type. You can configure the following types:

	|||
    |-|-|
    |**External**|Allows virtual machines to communicate with each other and with externally located servers, and optionally with the host operating system. You might use this setting to allow virtual machines to access a perimeter network and not expose the host operating system. An **External** network is bound to a physical network adapter.|
    |**Internal**|Allows communication between virtual machines on the same host and between the virtual machines and the host. This setting is often used to build a test environment where virtual machines are connected to the host operating system, but not connected to external networks. An **Internal** network is not bound to a physical network adapter.|
    |**Private**|Allows communication between virtual machines on the same host but not with the host or with external networks. This setting is often used to isolate virtual machines from network traffic in the host operating system and in the external networks. A **Private** network does not have a virtual network adapter in the host operating system, and is not bound to a physical network adapter.|

5.  If you click **External**, do the following:

	- In the **Network adapter** list, click the physical network adapter that you want to associate with the external virtual switch.
	- Review the **Logical network** field, which tells you which logical networks are assigned to the network adapter. 
	- To access the host through a VLAN, check **Access host through a VLAN** \(if available\), and then select a VLAN number. The list that you see shows the VLANs that are included in the logical network and are assigned to the network adapter. If you specify a VLAN for a single network connection to the host, network connectivity may be lost and you may lose the ability to manage the host. We recommend that you always use at least two physical network adapters on a host: one network adapter dedicated to remote management and communication between the host and the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] server, and one or more network adapters dedicated to the external virtual networks that are used by virtual machines.

## Configure network settings with a logical switch

You can configure network adapters by applying a logical switch and port profiles to the adapters.  

To do this you'll need to:

1. Configure the logical switch and port profiles that you will apply.
2. Specify whether a network adapter is used for virtual machines, host management, neither, or both.
2. Configure network settings on a host by applying a logical switch. The network adapters that you configure can be physical network adapters or virtual network adapters on the hosts.


### Set up a logical switch


1. Open the **Fabric** > **Home **> **Show** > **Fabric Resources** > **Networking** > **Logical Switches**.
2. In the Create Logical Switch Wizard > **Getting Started** page, review the information.
3. In **General**, enter a name and optional description for the logical switch. If you want to enable single root I/O virtualization (SR-IOV), select the Enable single root I/O virtualization (SR-IOV) check box. SR-IOV enables virtual machines to bypass the switch and directly address the physical network adapter. To fully enable SR-IOV make sure that:

	- You have SR-IOV support in the host hardware and firmware, the physical network adapter, and drivers in the management operating system and in the guest operating system.
	- Create a native port profile for virtual network adapters that is also SR-IOV enabled.
	- When you configure networking settings on the host (in the host property called Virtual switches), attach the native port profile for virtual network adapters to the virtual switch by using a port classification. You can use the SR-IOV port classification that is provided in VMM, or create your own port classification.
4. If you are using (optional) virtual switch extensions, on the Extensions page, select the boxes for one or more extensions, and then arrange the order in which the extensions should be processed by clicking Move Up and Move Down. f an extension that you expected does not appear in the list, it is likely that the provider software has not been installed on the VMM management server. For more information about how to install a provider, refer to the documentation from the vendor. To avoid conflicts between extensions, only one forwarding extension can be selected at a time. Extensions process network traffic through the switch in the order that they are listed.
5. In **Uplink** do the following:

	- To configure teaming for multiple network adapters by applying this logical switch to multiple adapters, for Uplink mode, select Team. Otherwise, leave the selection as No Uplink Team.
	- If you select Team, when you apply this logical switch with an uplink port profile, you will also apply two settings that are specified in the uplink port profile: the load-balancing algorithm and teaming mode settings.
	- To add an uplink port profile, click Add and in the Add Uplink Port Profile dialog box, select a port profile. Then click OK. Repeat this process until you have added all of the uplink port profiles that you want to add.
	- When you add an uplink port profile, it is placed in a list of profiles that are available through that logical switch. However, when you apply the logical switch to a network adapter in a host, the uplink port profile is applied to that network adapter only if you select it from the list of available profiles.
	- To remove an uplink port profile, select the profile and then click Remove.

6. In **Virtual Port**, add one or more port classifications (which make it easy to see the intended uses for a switch), with or without the associated virtual network adapter port profiles (which add capabilities to the logical switch). Optionally, you can skip this step and then add these items later. To add a port classification, click **Add** > **Virtual Port**. 
7. Either select a port classification or click **Create Port Classification** and specify a name and optional description for the port classification. Click OK until you have returned to the **Add Virtual Port** dialog box. While you are still in the Add Virtual Port dialog box, to include a virtual network adapter port profile, select the check box, and then in the Native virtual network adapter port profile list, select the port profile that you want to include. Repeat the process to add the required port classifications.
8. To set one port classification as the default, select that classification and then click Set Default. To clear a default setting from the list of port classifications, click Clear Default.
9. In **Summary**, review and confirm the settings, and then click **Finish**. The Jobs dialog box appears. Make sure that the job has a status of Completed, and then close the dialog box. Verify that the logical switch appears in the Logical Switches pane.

#### Configure a top-of-rack (TOR) switch

Before you add a top-of-rack switch:

- Ensure that you have the necessary provider software on the VMM management server. If your switch is based on the Common Information Model (CIM) network switch profile, you can use the provider that is included in VMM in System Center 2012 R2. Otherwise, you must obtain the provider software that is provided by the switch vendor and install it on the VMM management server. After you install the provider software, restart the System Center Virtual Machine Manager service.
- If you have installed a high availability VMM management server on a cluster, ensure that the provider is installed on all nodes of the cluster. Confirm that the provider is listed in **Settings** > **Configuration Providers**.
- For your TOR switch, make sure that you know the manufacturer and model, the name of an account that has configuration permissions, the connection string, and the host groups to include. If certificates are used for the provider software, make sure you know how to view the thumbprint information for those certificates.


1. Open **Fabric** > **Home** > **Show** > **Fabric Resources** > **Networking** > **Network Services**. Network services include gateways, virtual switch extensions, network managers, and TOR switches.
2. In the Add Network Service Wizard > Name page, specify a name and optional description.
3. On the Manufacturer and Model page, make selections as follows:

	- To use the provider software that is included in VMM, in the **Manufacturer **list, click **Microsoft**, and in the **Model** list, click **Microsoft Network Switch Profile Switch**.
	- To use provider software that is provided by the switch vendor, click the appropriate **Manufacturer** and ** Model** for your switch.
4. On the **Credentials** page, either click Browse and then on the Select a Run As Account dialog box, select an account, or click **Create Run As Accoun**t and create a new account.
5.  On the **Connection String** page, in the **Connection strin**g box, type the connection string that is used by the TOR switch. For example, you might enter the following connection string: https://TORswitch1.contoso.com:5986. If you are not using the provider software that is included in VMM, when you enter the connection string, use the syntax that is defined by the manufacturer of your TOR switch.
6. On the Certificates page, if certificates are listed, verify that the thumbprints of those certificates match the thumbprints of the certificates that are installed on the TOR switch. Then select the box to confirm that the certificates can be imported to the trusted certificate store. If no certificates are listed, the connection string that was provided probably does not require a certificate, and you can continue to the next page of the wizard. However, if no certificates are listed but your TOR switch requires them, confirm that the certificates were installed correctly on your device.
7. On the Provider page, in the Configuration provider list, select an available provider, and then click Test to run basic validation against the TOR switch by using the selected provider. If tests indicate that the provider software works as expected, click Next.
8. On the Host Group page, select one or more host groups to which the TOR switch will be available.
9. On the Summary page, review and confirm the settings, and then click Finish.

### Specify whether a network adapter is used for virtual machines, host management, neither, or both


Regardless of any port profiles and logical switches you are using in your network configuration, you must specify whether a network adapter in a host is used for virtual machines, host management, neither, or both. (The host must already be under management in VMM.)

1. Open  **Fabric** > **Servers** > **All Hosts** > host group > **Hosts** > **Host** > **Properties** > **Hardware**.
2. Under **Network adapters**, click the physical network adapter that you want to configure. If you want to use this network adapter for virtual machines, ensure that Available for placement is checked. If you want to use this network adapter for communication between the host and the VMM management server, ensure that Used by management is checked. You must make sure that you have at least one network adapter available for communication between the host and the VMM management server. Make sure that Used by management is checked for this network adapter.
3. If you have already applied a logical switch and an uplink port profile to a network adapter, if you click Logical network connectivity, you can see the resulting connectivity. However, if you plan to apply a logical switch and an uplink port profile, do not make individual selections in Logical network connectivity. Instead, use the following procedure.



### Configure network settings on a host by applying a logical switch

1. Open  **Fabric** > **Servers** > **All Hosts** > host group > **Hosts** > **Host** > **Properties** > **Virtual Switches**.
2. Select the logical switch you created. Under **Adapter**, select the physical adapter that you want to apply the logical switch to.
3. In the **Uplink Port Profile** list, select the uplink port profile that you want to apply. The list contains the uplink port profiles that have been added to the logical switch that you selected. If a profile seems to be missing, review the configuration of the logical switch and then return to this property tab. 
4. Repeat the steps as needed. If you apply the same logical switch and uplink port profile to two or more adapters, the two adapters might be teamed, depending on a setting in the logical switch. To find out if they will be teamed, open the logical switch properties, click the Uplink tab, and view the Uplink mode setting. If the setting is Team, the adapters will be teamed. The specific mode in which they will be teamed is determined by a setting in the uplink port profile.
5. If you didn't create the virtual switch earlier and you do it now, the host may temporarily lose network connectivity. This may have an adverse effect on other network operations in progress.



Compliance of network settings: After you apply logical switches, you can later check to see if the network adapter settings on a host are still in compliance with the logical switch settings. If they’re not, you can use VMM to bring them back into compliance. 


