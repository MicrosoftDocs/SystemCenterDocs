---
title: How to Create IP Address Pools for VM Networks in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae6e919f-0308-4e2f-a8ad-8d97ccba77dc
---
# How to Create IP Address Pools for VM Networks in VMM
You can use the following procedure to create a static IP address pool for a VM network in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] in [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)]. When you create a static IP address pool for a VM network, [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] can assign static IP addresses to Windows\-based virtual machines \(running on any supported hypervisor platform\) that use the VM network. By using static IP address pools, IP address management for the virtual environment is brought within the scope of the VMM administrator.

> [!IMPORTANT]
> For guidelines about when IP pools are necessary on a VM network, when they are optional, and when to create an IP pool in a logical network rather than a VM network, see [Guidelines for IP address pools](./Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md#BKMK_address_pools) in "Overview: plan logical networks, network sites, and IP address pools in VMM."

**Account requirements** To complete this procedure, you must be a member of the Administrator or Delegated Administrator user role.

## Prerequisites
Perform this procedure only after all the other networking elements have been configured for your virtual machines, including the logical network \(which is used as a foundation for VM networks\), the network sites for the logical network, and the VM network for which you want to create IP address pools. For more information, see [Prerequisites for gateways in VMM](./Prerequisites-for-gateways-in-VMM.md).

#### To create static IP address pools for VM networks in VMM

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

    1.  Under **IP address range**, enter the starting and ending IP addresses from the subnet that will make up the managed IP address pool. The starting and ending IP addresses must be contained within the subnet.

        > [!NOTE]
        > Be aware that you can create multiple IP address pools within a subnet. If you create multiple IP address pools within a subnet, the ranges cannot overlap.

        > [!TIP]
        > The **Total addresses** field displays the total number of IP addresses in the specified IP address range.

    2.  Under **Reserved IP addresses**, specify the IP address ranges that you want to reserve for other purposes. The IP addresses that you want to reserve must fall within the IP address range that you specified in step 8a.

9. Optionally, on the **Gateway** page, click **Insert**, and then specify one or more default gateway addresses and the metric. The default gateway address must fall within the same subnet range as the IP address pool. It does not have to be part of the IP address pool range.

    > [!NOTE]
    > The metric is a value that is assigned to an IP route for a particular network interface that identifies the cost that is associated with using that route. If you use the automatic metric, the metric is automatically configured for local routes based on the link speed.

10. Optionally, on the **DNS** page, specify Domain Name System \(DNS\)\-related information, such as the list of DNS servers and their order, the default DNS suffix for the connection, and the list of DNS search suffixes.

    > [!IMPORTANT]
    > For virtual machines that will join an Active Directory domain, we recommend that you use Group Policy to set the primary DNS suffix. This will ensure that when a Windows\-based virtual machine is set to register its IP addresses with the primary DNS suffix, a Windows\-based DNS server will register the IP address dynamically. Additionally, the use of Group Policy enables you to have an IP address pool that spans multiple domains. In this case, you would not want to specify a single primary DNS suffix.

11. Optionally, on the **WINS** page, click **Insert**, and then enter the IP address of a Windows Internet Name Service \(WINS\) server. You can also select the check box that indicates whether to enable NetBIOS over TCP\/IP. Be aware that enabling NetBIOS over TCP\/IP is not recommended if the address range consists of public IP addresses.

12. On the **Summary** page, confirm the settings, and then click **Finish**.

    The **Jobs** dialog box appears. Make sure that the job has a status of **Completed**, and then close the dialog box.

13. To verify that the IP address pool was created, in the **VM Networks and IP Pools** pane, expand the VM network where you created the pool.

    The IP address pool appears under the VM network.

14. Optionally, repeat this procedure to create additional IP address pools for VM networks.

> [!NOTE]
> You can use the Windows PowerShell cmdlets, [Get\-SCIPAddress](http://technet.microsoft.com/library/jj654453.aspx) and [Get\-SCStaticIPAddressPool](http://technet.microsoft.com/library/jj654257.aspx), to view the states of the IP addresses in an IP address pool. Use the cmdlets with the following syntax, where `<StaticIPAddressPool>` is the name of your static IP address pool:
> 
> `$ippool=Get-SCStaticIPAddressPool -Name <StaticIPAddressPool>`
> 
> `Get-SCIPAddress –StaticIPAddressPool $ippool | Format-Table –property Address,AssignedToType,State`

From time to time, you might need to release IP addresses that are in the pool but that are marked by [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] as “inactive.” Releasing them makes them available for reassignment. For more information, see [How to release inactive IP addresses for VM networks in VMM](./How-to-release-inactive-IP-addresses-for-VM-networks-in-VMM.md).

After a virtual machine has been deployed in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], you can view the IP address or addresses assigned to that virtual machine. To do this, right\-click the listing for the virtual machine, click **Properties**, click the **Hardware Configuration** tab, click the network adapter, and in the results pane, click the **Connection details** button.

## See Also
[How to release inactive IP addresses for VM networks in VMM](./How-to-release-inactive-IP-addresses-for-VM-networks-in-VMM.md)
[Prerequisites for gateways in VMM](./Prerequisites-for-gateways-in-VMM.md)
[How to create a VM network for a VLAN in VMM](./How-to-create-a-VM-network-for-a-VLAN-in-VMM.md)
[Overview: plan logical networks, network sites, and IP address pools in VMM](./Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md)


