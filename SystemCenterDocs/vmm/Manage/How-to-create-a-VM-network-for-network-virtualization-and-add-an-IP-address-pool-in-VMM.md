---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to create a VM network for network virtualization and add an IP address pool in VMM
ms.technology:  virtual-machine-manager
ms.assetid:  168132bf-9c34-4bb7-ab00-d7b07b28598c
---

# How to create a VM network for network virtualization and add an IP address pool in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

In Virtual Machine Manager (VMM), to support multiple tenants (also called clients or customers) with their own networks, isolated from the networks of others, use VM networks configured for Hyper-V network virtualization. For more information, see [Plan VM networks for Hyper-V network virtualization](Overview--plan-VM-networks-in-VMM.md#BKMK_hnv) in "Overview: plan VM networks in VMM." To see how this procedure fits into an overall workflow, see [Implementing the configuration](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md#BKMK_implementing) in "Configuring logical networks, VM networks, and logical switches in VMM."

After creating the VM network, create one or more IP address pools on it, regardless of whether you will use static IP addresses or DHCP on the VM network. If you choose DHCP, VMM will respond to a DHCP request with an address from an IP address pool.

This topic contains the following procedures:

-   [Create a VM network on a logical network where network virtualization is enabled](How-to-create-a-VM-network-for-network-virtualization-and-add-an-IP-address-pool-in-VMM.md#BKMK_nv_enabled)

-   [Create a static IP address pool for a VM network](How-to-create-a-VM-network-for-network-virtualization-and-add-an-IP-address-pool-in-VMM.md#BKMK_pool)

## <a name="BKMK_nv_enabled"></a>Create a VM network on a logical network where network virtualization is enabled
To perform this procedure, you must already have a logical network that uses the **One connected network** option, with the option **Allow new VM networks created on this logical network to use network virtualization**.

> [!NOTE]
> If you want to create a VM network and configure it with a gateway at the same time, you must first add the gateway to your VMM configuration. You can also add a gateway later, then open the property sheet of an existing VM network and configure the VM network to use the gateway. For more information, see [Configuring gateways in VMM](Configuring-gateways-in-VMM.md).

#### To create a VM network on a logical network where network virtualization is enabled

1.  Open the **VMs and Services** workspace.

2.  On the **Home** tab, in the **Show** group, click **VM Networks**.

3.  In the **VMs and Services** pane, click **VM Networks**.

4.  On the **Home** tab, in the **Create** group, click **Create VM Network**.

    The Create VM Network Wizard opens.

5.  On the **Name** page, type a name and an optional description, and then in the **Logical network** list, select the logical network on which you want to create the VM network. (This must be a logical network on which network virtualization is enabled.) Then click **Next**.

    > [!NOTE]
    > The wizard pages and VM network properties that you can configure will vary depending on the properties of the logical network that you selected.

6.  On the **Isolation** page, select **Isolate using Hyper-V network virtualization**. If you do not see this option, confirm that you selected a logical network that uses the option **Allow new VM networks created on this logical network to use network virtualization**, or see the links listed at the end of this topic.

    If needed, change the settings for the IP address protocol for the logical network and the IP address protocol for the VM network. Then click **Next**.

7.  On the **VM Subnets** page, click **Add**, type a name for the IP subnet, and specify the subnet by using CIDR notation. Add more VM subnets as needed, and then click **Next**.

8.  On the **Connectivity** page, if you see the message **No network service that specifies a gateway has been added to VMM**, proceed to the next step. Otherwise, configure connectivity (gateway) properties according to the following guidelines:

    -   **No connectivity** Leave all check boxes cleared if the virtual machines on this VM network will communicate only with other virtual machines on this VM network.

        > [!NOTE]
        > You can also leave the check boxes cleared if you plan to configure the gateway properties of this VM network later.

    -   **Connect to another network through a VPN tunnel** Select this option if the virtual machines on this VM network will communicate with other networks through a VPN tunnel. If the device will use the Border Gateway Protocol, also select the check box to enable this protocol. In the **Gateway device** list, select the VPN gateway device that you want to use. Confirm that the capabilities that are listed for the device are as expected.

        If you select **Connect to another network through a VPN tunnel** and select a **Gateway device**, the **VPN Connections** page of the wizard appears. If you selected the check box for Border Gateway Protocol, the **Border Gateway Protocol** page also appears. Fill in these pages based on information that you obtain from the administrator of that VPN gateway, for example, information about the VPN endpoint and the bandwidth. For more information, see [Prerequisites for gateways in VMM](Prerequisites-for-gateways-in-VMM.md).

    -   **Connect directly to an additional logical network** Select this option if the virtual machines on this VM network will communicate with other networks in this data center. Also select either **Direct routing** or **Network address translation (NAT)**. In the **Gateway device** list, select the gateway device that you want to use. Confirm that the capabilities that are listed for the device are as expected.

9. After you complete the options on each page that is related to connectivity, click **Next**.

10. On the **Summary** page, review and confirm the settings, and then click **Finish**.

11. Verify that the VM network appears in the **VM Networks and IP Pools** pane.

## <a name="BKMK_pool"></a>Create a static IP address pool for a VM network
In a VM network for network virtualization, create at least one IP address pool. For more information about IP address pools, see [Guidelines for IP address pools](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md#BKMK_address_pools) in "Overview: plan logical networks, network sites, and IP address pools in VMM."

#### To create a static IP address pool for a VM network

1.  Open the **VMs and Services** workspace.

    > [!NOTE]
    > Because this IP address pool is for virtual machines, it is created in the **VMs and services** workspace, not in the **Fabric** workspace.

2.  In the **VMs and Services** pane, click **VM Networks**.

3.  On the **Home** tab, in the **Show** group, click **VM Networks**.

    The **VM Network** tab appears.

4.  Click the **VM Network** tab.

5.  In the **VM Networks and IP Pools** pane, click the VM network where you want to create the IP pool.

6.  On the **VM Network** tab, in the **Create** group, click **Create IP Pool**.

    The Create Static IP Address Pool Wizard opens.

7.  On the **Name** page, do the following, and then click **Next**.

    1.  Enter a name and optional description for the IP address pool.

    2.  In the **VM network** list, make sure that the correct VM network is selected.

    3.  In the **VM subnet** list, make sure that the correct VM subnet is selected.

8.  On the **IP address range** page, do the following, and then click **Next**:

    1.  Under **IP address range**, enter the starting and ending IP addresses for the managed IP address pool. The starting and ending IP addresses must be contained within the subnet.

        > [!NOTE]
        > You can create multiple IP address pools within a subnet. If you create multiple IP address pools within a subnet, the ranges cannot overlap.

        > [!TIP]
        > The **Total addresses** field displays the total number of IP addresses in the specified IP address range.

    2.  Under **Reserved IP addresses**, specify the IP address ranges that you want to reserve for other purposes. The IP addresses that you want to reserve must fall within the IP address range that you specified for the IP address pool.

9. Optionally, on the **Gateway** page, click **Insert**, and then specify one or more default gateway addresses and the metric. The default gateway address must fall within the same subnet as the IP address pool. It does not have to be part of the IP address pool range.

    > [!NOTE]
    > The metric is a value that is assigned to an IP route for a particular network interface that identifies the cost that is associated with using that route. If you use the automatic metric, the metric is automatically configured for local routes based on the link speed.

10. Optionally, on the **DNS** page, specify Domain Name System (DNS)-related information, such as the list of DNS servers and their order, the default DNS suffix for the connection, and the list of DNS search suffixes.

    > [!IMPORTANT]
    > For virtual machines that will join an Active Directory domain, we recommend that you use Group Policy to set the primary DNS suffix. This will ensure that when a Windows-based virtual machine is set to register its IP addresses with the primary DNS suffix, a Windows-based DNS server will register the IP address dynamically. Additionally, the use of Group Policy enables you to have an IP address pool that spans multiple domains. In this case, you would not want to specify a single primary DNS suffix.

11. Optionally, on the **WINS** page, click **Insert**, and then enter the IP address of a Windows Internet Name Service (WINS) server. You can also select the check box that indicates whether to enable NetBIOS over TCP/IP. Be aware that enabling NetBIOS over TCP/IP is not recommended if the address range consists of public IP addresses.

12. On the **Summary** page, confirm the settings, and then click **Finish**.

    The **Jobs** dialog box appears. Make sure that the job has a status of **Completed**, and then close the dialog box.

13. To verify that the IP address pool was created, in the **VM Networks and IP Pools** pane, expand the VM network where you created the pool.

    The IP address pool appears under the VM network.

14. Optionally, repeat this procedure to create additional IP address pools for VM networks.

> [!NOTE]
> You can use the Windows PowerShell cmdlets, [Get-SCIPAddress](http://technet.microsoft.com/library/jj654453.aspx) and [Get-SCStaticIPAddressPool](http://technet.microsoft.com/library/jj654257.aspx), to view the states of the IP addresses in an IP address pool. Use the cmdlets with the following syntax, where `<StaticIPAddressPool>` is the name of your static IP address pool:
> 
> `$ippool=Get-SCStaticIPAddressPool -Name <StaticIPAddressPool>`
> 
> `Get-SCIPAddress �StaticIPAddressPool $ippool | Format-Table �property Address,AssignedToType,State`

From time to time, you might need to release IP addresses that are in the pool but that are marked by VMM as �inactive.� Releasing them makes them available for reassignment. For more information, see [How to release inactive IP addresses for VM networks in VMM](How-to-release-inactive-IP-addresses-for-VM-networks-in-VMM.md).

After a virtual machine has been deployed in VMM, you can view the IP address or addresses assigned to that virtual machine. To do this, right-click the listing for the virtual machine, click **Properties**, click the **Hardware Configuration** tab, click the network adapter, and in the results pane, click the **Connection details** button.

> [!IMPORTANT]
> If you configure a virtual machine to obtain a static IP address from an IP address pool, you must also configure the virtual machine to use a static MAC address. You can either specify the MAC address manually (during the **Configure Settings** step) or have VMM automatically assign a MAC address from a MAC address pool.
> 
> This requirement for static MAC addresses is necessary because VMM uses the MAC address to identify which network adapter to set the static IP address to, and this identification must happen before the virtual machine starts. Identifying the network adapter is especially important if a virtual machine has multiple adapters. If the MAC addresses were assigned dynamically through Hyper-V, VMM could not consistently identify the correct adapter to set a static IP address on.
> 
> VMM provides static MAC address pools by default, but you can customize the pools. For more information, see [VMM networking reference: creating custom MAC address pools in VMM](VMM-networking-reference--creating-custom-MAC-address-pools-in-VMM.md).

## See Also
[How to create a VM network for a VLAN in VMM](How-to-create-a-VM-network-for-a-VLAN-in-VMM.md)
[Overview: plan VM networks in VMM](Overview--plan-VM-networks-in-VMM.md)
[Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)



