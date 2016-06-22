---
title: How to create a logical switch in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0141a944-d781-41d6-b904-807893e6fd67
---
# How to create a logical switch in VMM
In Virtual Machine Manager \(VMM\), you can use logical switches \(and the port profiles inside them\) to help you configure switch settings consistently across multiple hosts. A logical switch is like a template for a virtual switch—it acts as a container for the switch settings and capabilities that you want to use. Instead of configuring switch settings individually for each network adapter, you can specify settings and capabilities in a logical switch, and then use the logical switch to apply those settings consistently across network adapters on multiple hosts.

To prepare for creating a logical switch, see [Overview: plan logical switches and port profiles in VMM](Overview--plan-logical-switches-and-port-profiles-in-VMM.md). Be sure to review the overview if you plan to enable single\-root I\/O virtualization \(SR\-IOV\) in your logical switch.

To see how this procedure fits into an overall workflow, see [Implementing the configuration](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md#BKMK_implementing) in "Configuring logical networks, VM networks, and logical switches in VMM."

For information about using Windows PowerShell for logical switches, see the links at the end of this topic.

**Account requirements** To complete this procedure, you must be a member of the Administrator or the Delegated Administrator user role. When configuring the switch, delegated administrators can select only uplink port profiles that contain network sites that are in the administrative scope of the delegated administrator.

### To create a logical switch

1.  Open the **Fabric** workspace.

2.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

3.  In the **Fabric** pane, expand **Networking** > **Logical Switches**.

4.  On the **Home** tab, in the **Create** group, click **Create Logical Switch**.

    The Create Logical Switch Wizard opens.

5.  On the **Getting Started** page, review the information about logical switches, and then click **Next**.

6.  Fill in the **General** page as follows:

    |Item|Description|
    |--------|---------------|
    |**Name** and **Description**|Type a name and \(optionally\) a description.|
    |**Uplink mode**|Select **No Uplink Team** or **Team**. Teaming is also known as load balancing and failover \(LBFO\).<br /><br />If you select **Team**, you also enable any teaming settings that you include in port profiles in the logical switch \(step 10 in this procedure\). These settings are described in [Load-balancing algorithm](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_algorithm) and [Teaming mode](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_teaming) in "Overview: plan logical switches and port profiles in VMM."|
    |**Enable single root I\/O virtualization \(SR\-IOV\)**|SR\-IOV enables virtual machines to bypass the switch and directly address the physical network adapter. SR\-IOV has multiple requirements:<br /><br />-   You must have SR\-IOV support in the host hardware and firmware, the physical network adapter, and drivers in the management operating system and in the guest operating system.<br />-   For the **Virtual Port** page of this wizard, see the Note in step 8, later in this procedure.|
    |**Minimum bandwidth mode**|Select **Default**, **Weight**, **Absolute**, or **None**. For information about the modes, see [Optional: review options for configuring bandwidth](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_bandwidth) in "Overview: plan logical switches and port profiles in VMM."|

7.  If you are using \(optional\) virtual switch extensions, on the **Extensions** page, select one or more extensions, and then arrange the order in which the extensions should be processed by clicking **Move Up** and **Move Down**. Then click **Next**.

    If an extension that you expected does not appear in the list, the provider software has probably not been installed on the VMM management server. For information about installing a provider, see the documentation from the vendor.

    > [!IMPORTANT]
    > To avoid conflicts between extensions, only one forwarding extension can be selected at a time.
    > 
    > Extensions process network traffic through the switch in the order that they are listed.

8.  On the **Virtual Port** page, add one or more port classifications and network adapter port profiles. A port profile adds capabilities, and the port classification makes it easy to identify the virtual port \(and its capabilities\), when it is offered as a selection in other parts of the VMM interface. Optionally, you can skip this step and then add these items later.

    > [!NOTE]
    > For information about creating port classifications and port profiles outside of the Create Logical Switch Wizard, see the following topics:
    > 
    > -   [VMM networking reference: creating a port classification in VMM](VMM-networking-reference--creating-a-port-classification-in-VMM.md)
    > -   [VMM networking reference: creating a custom port profile for virtual network adapters](VMM-networking-reference--creating-a-custom-port-profile-for-virtual-network-adapters.md)

    For example, to include capabilities for a management network in the logical switch, select the built\-in **Host management** port classification and the built\-in **Host management** port profile.

    To add a port classification and port profile, click **Add**, and then, in the **Add Virtual Port** dialog box, do the following:

    1.  Click **Browse**.

    2.  Either select a port classification or click **Create Port Classification** and specify a name and optional description for the port classification. Click **OK** until you have returned to the **Add Virtual Port** dialog box.

    3.  While still in the **Add Virtual Port** dialog box, to include a virtual network adapter port profile, select the check box, and then select the port profile, or click **Create** to create a custom profile. For information about the available settings, see [VMM networking reference: creating a custom port profile for virtual network adapters](VMM-networking-reference--creating-a-custom-port-profile-for-virtual-network-adapters.md).

    4.  To return to the **Virtual Port** page, click **OK**.

    As needed, repeat the process to add classifications and port profiles \(capabilities\) to the switch.

    > [!NOTE]
    > To use SR\-IOV, you must select a port classification, and select or create a virtual network adapter port profile in which SR\-IOV is enabled. For example, you could select the built\-in **SR\-IOV** classification and the built\-in **SR\-IOV** profile.

9. Still on the **Virtual Port** page, to set one port classification as the default, select that classification and then click **Set Default**. To clear a default setting from the list of port classifications, click **Clear Default**.

    After you have completed all settings on the page, click **Next**.

10. On the **Uplinks** page, fill in settings as follows:

    |Selection|What you can configure|
    |-------------|--------------------------|
    |**Add** > **New Uplink Port Profile**|When you add an uplink port profile, it becomes available in a list in that logical switch. Later, when you select that logical switch for a network adapter in a host, the list is displayed, and you can choose the uplink port profile for that network adapter.<br /><br />For a new port profile:<br /><br />-   Type a name and \(optionally\) a description.<br />-   Select teaming settings, as described in [Load-balancing algorithm](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_algorithm) and [Teaming mode](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_teaming) in "Overview: plan logical switches and port profiles in VMM."<br />-   Under **Network sites**, select the network sites to include in the logical switch.<br />-   If you have hosts running Windows Server 2012, select or clear **Enable Hyper\-V network virtualization** as appropriate. \(This setting does not affect hosts running a later operating system.\)|
    |**Add** > **Existing Uplink Port Profile**|Select an uplink port profile that you have already created. The port profile will be added to a list in that logical switch. Later, when you select that logical switch for a network adapter in a host, the list is displayed, and you can choose the uplink port profile or profiles for that network adapter.<br /><br />For more information about creating uplink port profiles outside of the Create Logical Switch Wizard, see [VMM networking reference: creating an uplink port profile in VMM](VMM-networking-reference--creating-an-uplink-port-profile-in-VMM.md).|
    |**New virtual network adapter** \(for the selected uplink\)—button is dimmed if the VM networks are configured for network virtualization|-   **Name**: Type a name for the virtual network adapter. For example, you could type **MgmtVNic**.<br />-   **VM Network**: Click **Browse** and then either select a VM network, or click **Create VM Network**. For information about VM networks, see [Overview: plan VM networks in VMM](Overview--plan-VM-networks-in-VMM.md).<br />-   **VM subnet**: As needed, select a subnet.<br />-   **Enable VLAN** and **VLAN ID**: If the selected VM network is VLAN\-based, **Enable VLAN** is automatically checked, and you can select the **VLAN ID**. For background information, see [Plan VM networks for a VLAN-based configuration](Overview--plan-VM-networks-in-VMM.md#BKMK_VLAN) in "Overview: plan VM networks in VMM."<br />-   **Host management and "Inherit connection" settings**: As appropriate, select one or both settings. If you select **Inherit connection settings from host network adapter**, the IP address configuration settings are dimmed.<br />-   **IP address configuration**: Select **DHCP**, or select **Static** and then select an IP address pool.<br />-   **Port profile**: Select the classification associated with the capabilities that you want for this virtual network adapter. For example, if you were configuring a management network adapter, you could select the **Host management** classification.|
    |**Delete**|Deletes the selected item.|

    After you have completed all settings, click **Next**.

11. On the **Summary** page, review and confirm the settings, and then click **Finish**.

    The **Jobs** dialog box appears. Make sure that the job has a status of **Completed**, and then close the dialog box.

12. Verify that the logical switch appears in the **Logical Switches** pane.

## See Also
[Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)
[Bare Metal Deploy through VMM PowerShell (Part 1)](http://blogs.technet.com/b/privatecloud/archive/2013/02/22/bare-metal-deploy-through-vmm-powershell-part-1.aspx)
[Bare Metal Deploy through VMM PowerShell (Part 2)](http://blogs.technet.com/b/privatecloud/archive/2013/03/04/bare-metal-deploy-through-vmm-powershell-part-2.aspx)
[Hyper-V Host Network Settings through VMM PowerShell (Part 3)](http://blogs.technet.com/b/privatecloud/archive/2013/05/20/hyper-v-host-network-settings-through-vmm-powershell-part-3.aspx)


