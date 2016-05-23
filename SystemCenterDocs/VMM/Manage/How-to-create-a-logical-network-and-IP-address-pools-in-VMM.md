---
title: How to create a logical network and IP address pools in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f7b6403-876a-4eae-9f00-5372626d51bc
---
# How to create a logical network and IP address pools in VMM
Logical networks form the foundation of your network configuration in [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)] in [!INCLUDE[sc_threshold_1](../../Token/sc_threshold_1_md.md)]. You create and name logical networks based on the function they serve in your environment, for example, the “Management,” “Cluster,” “Storage,” or “Tenant” networks. Within each logical network, you create one or more network sites that specify IP subnets, virtual local area networks \(VLANs\), or subnet\/VLAN pairs that represent your environment.

For information about planning your logical networks, see [Overview: plan logical networks, network sites, and IP address pools in VMM](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md). To see how this procedure fits into an overall workflow, see [Implementing the configuration](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md#BKMK_implementing) in "Configuring logical networks, VM networks, and logical switches in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]."

If you want to use a virtual switch extension, network manager, or vendor network\-management console to manage your networks instead of working with them directly in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], see [VMM networking reference: using a virtual switch extension manager or network manager in VMM](VMM-networking-reference--using-a-virtual-switch-extension-manager-or-network-manager-in-VMM.md)

> [!IMPORTANT]
> [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] does not automatically create port groups on VMware ESX hosts. Therefore, in order for logical networks to work correctly for managed ESX hosts, you must use VMware vCenter Server to configure port groups with the necessary VLANs that correspond to the network sites.

This topic contains the following procedures:

-   [Create a logical network](How-to-create-a-logical-network-and-IP-address-pools-in-VMM.md#BKMK_LN)

-   [Create a static IP address pool for a logical network](How-to-create-a-logical-network-and-IP-address-pools-in-VMM.md#BKMK_pool)

## <a name="BKMK_LN"></a>Create a logical network
**Account requirements** To complete this procedure, you must be a member of the Administrator or the Delegated Administrator user role. Delegated administrators can only associate a logical network to host groups that are included in their administrative scope.

#### To create a logical network

1.  Open the **Fabric** workspace.

2.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

3.  In the **Fabric** pane, expand **Networking** > **Logical Networks**.

4.  On the **Home** tab, in the **Create** group, click **Create Logical Network**.

    The **Create Logical Network Wizard** opens.

5.  On the **Name** page, do the following:

    1.  Enter a name and optional description for the logical network.

        For example, enter the name **Management**, with the description **Network for managing hosts**.

    2.  Select one or more check boxes based on how you intend to use any VM networks that will be configured on top of this logical network. The following table provides guidelines.

        |Use of VM networks that will be created on top of this logical network|Action|
        |--------------------------------------------------------------------------|----------|
        |**Hyper\-V network virtualization**: multiple VM networks with isolation|Select **One connected network** and then select **Allow new VM networks created on this logical network to use network virtualization**.|
        |**VLAN\-based configuration**: manage VLANs that have been created for network isolation within the physical network|In most cases, select **VLAN\-based independent networks**. However, if you are using private VLAN technology, select **Private VLAN \(PVLAN\) networks**.|
        |**One VM network that gives direct access to the logical network**: no isolation|Select **One connected network** and select **Create a VM network with the same name to allow virtual machines to access this logical network directly**. If this logical network will also support network virtualization, select the check box to allow network virtualization.<br /><br />If you select **One connected network** but you do not create the VM network now, you will still be able to create the VM network later.|

6.  Click **Next**.

7.  On the **Network Site** page, take the following steps.

    > [!NOTE]
    > For guidelines for configuring network sites, see [Guidelines for network sites: VLAN and IP subnet settings](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md#BKMK_vlans_ip) in "Overview: plan logical networks, network sites, and IP address pools in VMM."
    > 
    > If you do not need to configure network sites, on the **Network Site** page, click **Next**, and then click **Finish** to complete the wizard.

    1.  To create a network site, click **Add**.

        [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] automatically generates a site name that consists of the logical network name, followed by an underscore and a number.

    2.  Review the network site name and ensure that it is no longer than 64 characters. To change the default name, in the **Network site name** box, enter a new name for the network site.

        For example, enter the name **Management \- Seattle**.

    3.  Under **Host groups that can use this network site**, select the check box next to each host group to which you want to make the logical network available.

        For example, to make the **Management** logical network available to a host group called **Seattle** \(and all its child host groups\), select the check box next to **Seattle**.

    4.  Under **Associated VLANs and IP subnets**, enter the VLANs and IP subnets that you want to assign to the network site. To enter VLAN and IP subnet information, click **Insert row**, click the field under **VLAN** or **IP subnet**, depending on what you want to configure, and then enter a VLAN, an IP subnet, or a subnet\/VLAN pair. You can insert multiple rows.

        If you previously selected the option for private VLANs, also enter the **SecondaryVLAN** for each VLAN that you enter.

        > [!NOTE]
        > -   Make sure that you use VLANs and IP subnets that are available in your network.
        > -   By default, if you leave the VLAN field empty, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] assigns a VLAN of 0. This indicates to [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] not to use VLANs. In trunk mode, VLAN 0 indicates native VLAN.

        **Example of typical network site configuration**

        ![](Image/VMM_TH_LogicalNetwork.JPG)

    5.  Optionally, create additional network sites by clicking **Add** and repeating the process.

        For example, you could create a network site named **Management\-New York**, assign it to the **New York** host group, and add an appropriate IP subnet\/VLAN pair for the network in New York.

    6.  When you complete this step, click **Next**.

8.  On the **Summary** page, review the settings, and then click **Finish**.

    The **Jobs** dialog box appears. Make sure the job has a status of **Completed**, and then close the dialog box.

9. Verify that the logical network appears in the **Logical Networks and IP Pools** pane. Also, if you added network sites, right\-click the logical network, click **Properties**, click the **Network Site** tab, and verify that the intended network sites appear on the tab.

## <a name="BKMK_pool"></a>Create a static IP address pool for a logical network
In a logical network, you can provide static IP addressing by creating static IP address pools. Static IP address pools also have other uses. To decide whether you need an IP address pool, see [Guidelines for IP address pools](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md#BKMK_address_pools) in "Overview: plan logical networks, network sites, and IP address pools in VMM."

**Account requirements** To complete this procedure, you must be a member of the Administrator or Delegated Administrator user role.

#### To create a static IP address pool for a logical network

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Networking** > **Logical Networks**.

3.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

4.  In the **Logical Networks and IP Pools** pane, click the logical network where you want to create the IP pool.

    For example, you could click a logical network called **Management**.

5.  On the **Home** tab, in the **Create** group, click **Create IP Pool**.

    The Create Static IP Address Pool Wizard opens.

6.  On the **Name** page, do the following, and then click **Next**.

    1.  Enter a name and optional description for the IP address pool.

    2.  In the **Logical network** list, make sure that the correct logical network is selected.

    For example, enter the following name and description for the **Management** logical network, and then click **Next**.

    |||
    |-|-|
    |Name:|**Management – Seattle IP pool**|
    |Description:|**IP addresses for management \- Seattle**|

7.  On the **Network Site** page, select an existing network site or create a new one. Alternatively, if you want to use multicasting or broadcasting, skip to the next numbered step.

    If you select **Use an existing network site**, select the network site and the IP subnet that you want to create the IP address pool from, and then click **Next**.

    > [!NOTE]
    > You cannot change the virtual local area network \(VLAN\) or the assigned host groups for an existing network site from this page. If you try to change the host groups that can use the network site from this page, the value will revert to the original value when you continue to the next page of the wizard. To modify these values, you must modify the properties of the logical network. For more information, see [How to modify or delete a logical network in VMM](How-to-modify-or-delete-a-logical-network-in-VMM.md).

    If you select **Create a network site**, do the following, and then click **Next**:

    1.  In the **Network site** name box, enter a name for the network site.

    2.  In the **IP subnet** box, enter the IP subnet that you want to assign to the network site. Later in this procedure you can assign a range of IP addresses from the subnet to the pool. Specify the IP subnet with Classless Inter\-Domain Router \(CIDR\) notation, for example 10.0.0.0\/24.

    3.  If you are using VLANs, in the **VLAN** box, enter the VLAN ID. A VLAN of 0 indicates to [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] not to use VLANs. In trunk mode, VLAN 0 indicates native VLAN.

    4.  Under **Host groups that can use this network site**, select the check box next to each host group to which you want to make the network site and the associated logical network available.

8.  If you want to use multicasting or broadcasting, follow this step. Otherwise, skip to the next numbered step.

    If the logical network on which you are creating the IP address pool is configured to use network virtualization, you can use this pool to support broadcasting or multicasting. To do this, on the **Network Site** page, click **Create a multicast IP address pool**, select the IP subnet that you want to use for multicasting or broadcasting, and then click **Next**. For more information, see [VMM networking reference: IP address pool requirements for multicasting or broadcasting](VMM-networking-reference--IP-address-pool-requirements-for-multicasting-or-broadcasting.md).

9. On the **IP address range** page, do the following, and then click **Next**:

    1.  Under **IP address range**, enter the starting and ending IP addresses for the managed IP address pool. The beginning and ending IP address must be contained within the subnet.

        > [!NOTE]
        > You can create multiple IP address pools within a subnet. If you create multiple IP address pools within a subnet, the ranges cannot overlap.

        > [!TIP]
        > The **Total addresses** field displays the total number of IP addresses in the specified IP address range.

    2.  Under **VIPs and reserved IP addresses**, specify IP address ranges that you want to reserve, such as a range for load balancer virtual IP addresses \(VIPs\). The IP addresses that you want to reserve must fall within the IP address range that you specified for the IP address pool.

        > [!NOTE]
        > During deployment of a service with a load\-balanced service tier, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] automatically assigns a virtual IP address to the load balancer from the reserved range of VIP addresses. After the DNS administrator registers the assigned VIP address in DNS, clients can access the service by connecting through its registered name in DNS.

10. Optionally, on the **Gateway** page, click **Insert**, and then specify one or more default gateway addresses and the metric. The default gateway address must fall within the same subnet range as the IP address pool. It does not have to be part of the IP address pool range.

    > [!NOTE]
    > The metric is a value that is assigned to an IP route for a particular network interface that identifies the cost that is associated with using that route. If you use the automatic metric, the metric is automatically configured for local routes based on the link speed.

11. Optionally, on the **DNS** page, specify Domain Name System \(DNS\)\-related information, such as the list of DNS servers and their order, the default DNS suffix for the connection, and the list of DNS search suffixes.

    > [!IMPORTANT]
    > For virtual machines that will join an Active Directory domain, we recommend that you use Group Policy to set the primary DNS suffix. This will ensure that when a Windows\-based virtual machine is set to register its IP addresses with the primary DNS suffix, a Windows\-based DNS server will register the IP address dynamically. Additionally, the use of Group Policy enables you to have an IP address pool that spans multiple domains. In this case, you would not want to specify a single primary DNS suffix.

12. Optionally, on the **WINS** page, click **Insert**, and then enter the IP address of a Windows Internet Name Service \(WINS\) server. You can also select the check box that indicates whether to enable NetBIOS over TCP\/IP. Be aware that enabling NetBIOS over TCP\/IP is not recommended if the address range consists of public IP addresses.

13. On the **Summary** page, confirm the settings, and then click **Finish**.

    The **Jobs** dialog box appears. Make sure that the job has a status of **Completed**, and then close the dialog box.

14. To verify that the IP address pool was created, in the **Logical Networks and IP Pools** pane, expand the logical network where you created the pool.

    The IP address pool appears under the logical network.

15. Optionally, repeat this procedure to add IP address pools for other logical networks.

> [!NOTE]
> You can use the Windows PowerShell cmdlets, [Get-SCIPAddress](http://technet.microsoft.com/library/jj654453.aspx) and [Get-SCStaticIPAddressPool](https://technet.microsoft.com/library/jj654257.aspx), to view the states of the IP addresses in an IP address pool. Use the cmdlets with the following syntax, where `<StaticIPAddressPool>` is the name of your static IP address pool:
> 
> `$ippool=Get-SCStaticIPAddressPool -Name <StaticIPAddressPool>`
> 
> `Get-SCIPAddress –StaticIPAddressPool $ippool | Format-Table –property Address,AssignedToType,State`

From time to time, you might need to release IP addresses that are in the pool but that are marked by [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] as “inactive.” Releasing them makes them available for reassignment. For more information, see [How to release inactive IP or MAC addresses in VMM](How-to-release-inactive-IP-or-MAC-addresses-in-VMM.md).

After a virtual machine has been deployed in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], you can view the IP address or addresses assigned to that virtual machine. To do this, right\-click the listing for the virtual machine, click **Properties**, click the **Hardware Configuration** tab, click the network adapter, and in the results pane, click the **Connection details** button.

## See Also
[Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)


