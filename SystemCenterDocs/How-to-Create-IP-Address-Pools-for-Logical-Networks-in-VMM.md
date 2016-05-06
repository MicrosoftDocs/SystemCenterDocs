---
title: How to Create IP Address Pools for Logical Networks in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c549f961-01d0-4d28-8b93-f4108a34f00a
---
# How to Create IP Address Pools for Logical Networks in VMM
You can use the following procedure to create a static IP address pool for a logical network in [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)]. With static IP address pools, IP address management for the virtual environment is brought within the scope of the VMM administrator.

> [!IMPORTANT]
> For guidelines about when IP pools are necessary on a logical network, when they are optional, and when to create an IP pool in a VM network in addition to an IP pool in the logical network, see [Guidelines for IP address pools](./Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md#BKMK_address_pools) in "Overview: plan logical networks, network sites, and IP address pools in VMM."

**Account requirements** To complete this procedure, you must be a member of the Administrator or Delegated Administrator user role.

## Prerequisites
Before you begin this procedure, make sure that a logical network exists, ideally with one or more associated network sites \(which are part of the logical network\). The network sites must have at least one IP subnet or IP subnet\/VLAN pair assigned. For more information about creating a network site, see [How to create a logical network and IP address pools in VMM](./How-to-create-a-logical-network-and-IP-address-pools-in-VMM.md). If you do not already have network sites defined, you can create a network site when you create the static IP address pool.

#### To create static IP address pools for logical networks

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Networking**, and then click **Logical Networks**.

3.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

4.  In the **Logical Networks and IP Pools** pane, click the logical network where you want to create the IP pool.

    For example, you might have a logical network named **Management** where you want to create an IP pool .

5.  On the **Home** tab, in the **Create** group, click **Create IP Pool**.

    The Create Static IP Address Pool Wizard opens.

6.  On the **Name** page, do the following, and then click **Next**.

    1.  Enter a name and optional description for the IP address pool.

    2.  In the **Logical network** list, make sure that the correct logical network is selected.

    For example, enter the following name and description for the **Management** logical network, and then click **Next**.

    |||
    |-|-|
    |Name:|**Management – Seattle IP pool**|
    |Description:|**IP addresses for managing hosts \- Seattle**|

7.  On the **Network Site** page, select an existing network site or create a new one. Alternatively, if you want to use multicasting or broadcasting, skip to the next numbered step.

    If you select **Use an existing network site**, select the network site and the IP subnet that you want to create the IP address pool from, and then click **Next**.

    > [!NOTE]
    > You cannot change the virtual local area network \(VLAN\) or the assigned host groups for an existing network site from this page. If you try to change the host groups that can use the network site from this page, the value will revert to the original value when you continue to the next page of the wizard. To modify these values, you must modify the properties of the logical network. For more information, see [How to modify or delete a logical network in VMM](./How-to-modify-or-delete-a-logical-network-in-VMM.md).

    If you select **Create a network site**, do the following, and then click **Next**:

    1.  In the **Network site** name box, enter a name for the network site.

    2.  In the **IP subnet** box, enter the IP subnet that you want to assign to the network site. Later in this procedure you can assign a range of IP addresses from the subnet to the pool. You must specify the IP subnet by using Classless Inter\-Domain Router \(CIDR\) notation, for example 10.0.0.0\/24.

    3.  If you are using VLANs, in the **VLAN** box, enter the VLAN ID. A VLAN of 0 indicates to [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] not to use VLANs. In trunk mode, VLAN 0 indicates native VLAN.

    4.  Under **Host groups that can use this network site**, select the check box next to each host group to which you want to make the network site and the associated logical network available.

8.  If you want to use multicasting or broadcasting, follow this step. Otherwise, skip to the next numbered step.

    If the logical network on which you are creating the IP address pool is configured to use network virtualization, you can use this pool to support broadcasting or multicasting. To do this, on the **Network Site** page, click **Create a multicast IP address pool**, select the IP subnet that you want to use for multicasting or broadcasting, and then click **Next**. If you select this option, also see [VMM networking reference: IP address pool requirements for multicasting or broadcasting](./VMM-networking-reference--IP-address-pool-requirements-for-multicasting-or-broadcasting.md).

9. On the **IP address range** page, do the following, and then click **Next**:

    1.  Under **IP address range**, enter the starting and ending IP addresses from the subnet that will make up the managed IP address pool. The beginning and ending IP address must be contained within the subnet.

        > [!NOTE]
        > Be aware that you can create multiple IP address pools within a subnet. If you create multiple IP address pools within a subnet, the ranges cannot overlap.

        For example, add the following information for the **Management – Seattle** network site, and then click **Next**.

        |||
        |-|-|
        |Starting IP address:|**10.0.0.10**|
        |Ending IP address:|**10.0.0.99**|

        > [!TIP]
        > The **Total addresses** field displays the total number of IP addresses in the specified IP address range.

    2.  Under **VIPs and reserved IP addresses**, specify IP address ranges that you want to reserve, such as a range for load balancer virtual IP addresses \(VIPs\). The IP addresses that you want to reserve must fall within the IP address range that you specified in step 8a.

        For example, in the **IP addresses reserved for creating load balancer VIPs** box, enter the address range **10.0.0.25–10.0.0.35**, and then click **Next**.

        > [!NOTE]
        > During deployment of a service with a load\-balanced service tier, VMM automatically assigns a virtual IP address to the load balancer from the reserved range of VIP addresses. After the DNS administrator registers the assigned VIP address in DNS, clients can access the service by connecting through its registered name in DNS.

10. Optionally, on the **Gateway** page, click **Insert**, and then specify one or more default gateway addresses and the metric. The default gateway address must fall within the same subnet range as the IP address pool. It does not have to be part of the IP address pool range.

    For example, enter the default gateway address **10.0.0.1**, accept the default of **Automatic** as the metric, and then click **Next**.

    > [!NOTE]
    > The metric is a value that is assigned to an IP route for a particular network interface that identifies the cost that is associated with using that route. If you use the automatic metric, the metric is automatically configured for local routes based on the link speed.

11. Optionally, on the **DNS** page, specify Domain Name System \(DNS\)\-related information, such as the list of DNS servers and their order, the default DNS suffix for the connection, and the list of DNS search suffixes.

    > [!IMPORTANT]
    > For virtual machines that will join an Active Directory domain, we recommend that you use Group Policy to set the primary DNS suffix. This will ensure that when a Windows\-based virtual machine is set to register its IP addresses with the primary DNS suffix, a Windows\-based DNS server will register the IP address dynamically. Additionally, the use of Group Policy enables you to have an IP address pool that spans multiple domains. In this case, you would not want to specify a single primary DNS suffix.

    For example, enter the DNS server address **10.0.0.2**, the connection\-specific DNS suffix **contoso.com**, and then click **Next**.

12. Optionally, on the **WINS** page, click **Insert**, and then enter the IP address of a Windows Internet Name Service \(WINS\) server. You can also select the check box that indicates whether to enable NetBIOS over TCP\/IP. Be aware that enabling NetBIOS over TCP\/IP is not recommended if the address range consists of public IP addresses.

    For example, enter the WINS server address **10.0.0.3**, and then click **Next**.

13. On the **Summary** page, confirm the settings, and then click **Finish**.

    The **Jobs** dialog box appears. Make sure that the job has a status of **Completed**, and then close the dialog box.

14. To verify that the IP address pool was created, in the **Logical Networks and IP Pools** pane, expand the logical network where you created the pool.

    The IP address pool appears under the logical network.

15. Optionally, repeat this procedure to add IP address pools for other logical networks.

    > [!NOTE]
    > Throughout the example scenarios, the **Management** logical network is used as an example. Therefore, the example IP addresses are provided only for the **Management** logical network.

> [!NOTE]
> You can use the Windows PowerShell cmdlets, [Get\-SCIPAddress](http://technet.microsoft.com/library/jj654453.aspx) and [Get\-SCStaticIPAddressPool](https://technet.microsoft.com/library/jj654257.aspx), to view the states of the IP addresses in an IP address pool. Use the cmdlets with the following syntax, where `<StaticIPAddressPool>` is the name of your static IP address pool:
> 
> `$ippool=Get-SCStaticIPAddressPool -Name <StaticIPAddressPool>`
> 
> `Get-SCIPAddress –StaticIPAddressPool $ippool | Format-Table –property Address,AssignedToType,State`

From time to time, you might need to release IP addresses that are in the pool but that are marked by [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] as “inactive.” Releasing them makes them available for reassignment. For more information, see [How to release inactive IP or MAC addresses in VMM](./How-to-release-inactive-IP-or-MAC-addresses-in-VMM.md).

After a virtual machine has been deployed in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], you can view the IP address or addresses assigned to that virtual machine. To do this, right\-click the listing for the virtual machine, click **Properties**, click the **Hardware Configuration** tab, click the network adapter, and in the results pane, click the **Connection details** button.

## See Also
[How to release inactive IP or MAC addresses in VMM](./How-to-release-inactive-IP-or-MAC-addresses-in-VMM.md)
[Overview: plan logical networks, network sites, and IP address pools in VMM](./Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md)
[How to create a logical network and IP address pools in VMM](./How-to-create-a-logical-network-and-IP-address-pools-in-VMM.md)
[How to Create IP Address Pools for VM Networks in VMM](./How-to-Create-IP-Address-Pools-for-VM-Networks-in-VMM.md)
[VMM networking reference: creating custom MAC address pools in VMM](./VMM-networking-reference--creating-custom-MAC-address-pools-in-VMM.md)


