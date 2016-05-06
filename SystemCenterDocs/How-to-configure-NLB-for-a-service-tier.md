---
title: How to configure NLB for a service tier
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24471a44-c974-4bd1-a5a8-141f94309e2d
---
# How to configure NLB for a service tier
In [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)], a service is a set of virtual machines that are configured and deployed together and are managed as a single entity—for example, a deployment of a multi\-tier line\-of\-business application.

Use the following procedure to configure Microsoft Network Load Balancing \(NLB\) for one or more tiers of a service template in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]. For example, you might configure a load balancer for a Web tier and for a middle business logic tier.

> [!NOTE]
> -   In service tiers running Linux, NLB cannot be used.
> -   With VM networks configured with network virtualization, NLB cannot be used.
> 
> For both of the previous configurations, hardware load balancing can be used instead, as described in [Configuring load balancing in VMM](./Configuring-load-balancing-in-VMM.md).

To support NLB, there are several prerequisites that must be met. These include fabric\-related prerequisites, and specific operating system requirements and configuration settings that are required for the virtual machines that you want to load balance.

> [!IMPORTANT]
> You must configure a load balancer for a tier before you deploy a service. After you deploy a service, you cannot add a load balancer by updating the service.

**Account requirements** To configure the fabric prerequisites, you must be an administrator or a delegated administrator. Delegated administrators can only configure the prerequisites that are within the scope of their user role. To add a load balancer to a service template, or to complete the virtual machine template prerequisites, you must be an administrator, a delegated administrator, or a member of a self\-service user role that has the **Author** action in their scope.

**Fabric prerequisites**

Before you begin this procedure, make sure that the following prerequisites are met:

-   Create a virtual IP \(VIP\) template for NLB. For more information, see [How to create VIP templates for Network Load Balancing &#40;NLB&#41; in VMM](./How-to-create-VIP-templates-for-Network-Load-Balancing--NLB--in-VMM.md).

-   Create the desired logical networks and VM networks, with one or more associated network sites. Ensure that the network sites where users will deploy the service have one or more associated IP subnets that you can create static IP address pools from. Also, ensure that you associate each network site with the host group or one of its parent host groups where the service may be deployed. For more information, see [How to create a logical network and IP address pools in VMM](./How-to-create-a-logical-network-and-IP-address-pools-in-VMM.md) and [How to create a VM network for a VLAN in VMM](./How-to-create-a-VM-network-for-a-VLAN-in-VMM.md).

-   Create static IP address pools that are associated with the network sites where users will deploy the service. The IP address pools must contain a reserved range of virtual IP \(VIP\) addresses that can be assigned to the load balancer, and a range for the virtual machines that will be placed behind the load balancer.

    > [!IMPORTANT]
    > The addresses for the VIPs and the dedicated IP addresses for the virtual machines can be from the same pool or from different pools. However, the VIP address and the dedicated virtual machine IP addresses must all be in the same subnet.

    For more information, see [How to create a logical network and IP address pools in VMM](./How-to-create-a-logical-network-and-IP-address-pools-in-VMM.md) or [How to create a VM network for network virtualization and add an IP address pool in VMM](./How-to-create-a-VM-network-for-network-virtualization-and-add-an-IP-address-pool-in-VMM.md).

-   On each host where the service may be deployed, ensure that a physical network adapter on the host is configured to use the same logical network that the service tier will use. For example, if the tier will use a logical network called **Management**, that logical network must be associated with a physical adapter on the host. For more information, see [How to configure network settings on a Hyper-V host in VMM](./How-to-configure-network-settings-on-a-Hyper-V-host-in-VMM.md) or [How to configure network settings on a host by using a logical switch in VMM](./How-to-configure-network-settings-on-a-host-by-using-a-logical-switch-in-VMM.md).

**Virtual machine template prerequisites**

When you use the Create VM Template wizard to create a virtual machine template for a service tier that you want to load balance by using NLB, or if you have an existing virtual machine template that you want to use, verify that the following prerequisites are met:

> [!NOTE]
> The following table lists only the required settings for NLB. Configure other settings according to your virtual machine requirements. For information about how to create a virtual machine template for a service tier, see [How to create a virtual machine template](./How-to-create-a-virtual-machine-template.md).

|NLB requirements|More information|
|--------------------|--------------------|
|Ensure that the operating system for the virtual hard disk is an appropriate version, as listed under “More information.”|One of the requirements is that you install the NLB feature in the guest operating system. To install operating\-system features through [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], you cannot use a guest operating system earlier than [!INCLUDE[nextref_server_7](./Token/nextref_server_7_md.md)]. **Note:** The NLB feature is included in most editions of the Windows Server operating system. An exception is the HPC Edition of [!INCLUDE[nextref_server_7](./Token/nextref_server_7_md.md)].|
|Configure the network adapter to use a network with static IP address assignment, static MAC addresses, and, depending on the hypervisor that you want to deploy the service to, enable MAC address spoofing.|On the **Configure Hardware** page of the Create VM Template wizard \(or the **Hardware Configuration** tab in the properties of an existing virtual machine template\), click a network adapter, and then do the following: **Note:** If you are using a hardware profile, configure these settings in the hardware profile.<br /><br />1.  Under **Connectivity**, click **Connected to a VM network**, and then select the desired network that meets the requirements that are outlined in the “Fabric Requirements” section of this topic.<br />2.  Click **Static IP \(from a static IP pool\)** to configure the network adapter to use a static IP address. In the **IP protocol version** list, select the correct IP protocol version, for example, **IPv4 only**.<br />3.  Under **MAC Address**, click **Static**.<br />4.  If appropriate, select **Enable spoofing of MAC addresses**. **Note:** Do not enable MAC address spoofing for a virtual machine template or an associated hardware profile that will be used to deploy a service to a Hyper\-V host running [!INCLUDE[nextref_server_7](./Token/nextref_server_7_md.md)], or to a VMware ESX host.|
|Set the administrator password|On the **Configure Operating System** page of the Create VM Template wizard \(or the **OS Configuration** tab in the properties of an existing virtual machine template\), under **General Settings**, click **Admin Password**. Either specify the password of the local administrator account or select a Run As account for the local administrator account. **Note:** If you are using a guest operating system profile, configure the administrator account settings in the profile.|
|Configure the virtual machine to join a domain|On the **Configure Operating System** page of the Create VM Template wizard \(or the **OS Configuration** tab in the properties of an existing virtual machine template\), under **Networking**, configure the virtual machine to join a domain. This includes the credentials to join the domain. **Note:** If you are using a guest operating system profile, configure the domain settings in the profile.|
|Enable the Network Load Balancing feature|On the **Configure Operating System** page of the Create VM Template wizard \(or the **OS Configuration** tab in the properties of an existing virtual machine template\), do the following: **Note:** If you are using a guest operating system profile, configure these settings in the profile.<br /><br />1.  Under **Roles and Features**, click **Features**.<br />2.  Select the **Network Load Balancing** check box.<br />3.  Optionally, under **Remote Server Administration Tools**, select the **Network Load Balancing Tools** check box. Network Load Balancing Tools include the Network Load Balancing Manager snap\-in, Windows PowerShell tools for managing Network Load Balancing, and the Nlb.exe and Wlbs.exe command\-line tools. **Important:**     The NLB tools are not available in a Server Core installation of the Windows Server 2008 R2 operating system or the Windows Server 2012 operating system. Therefore, do not select this option if you are using a Server Core installation, or service deployment will fail. \(If you are using a Server Core installation, and you receive a validation error message saying that you must select NLB and the NLB tools feature, make sure that you have the NLB feature selected. You can ignore the part of the warning message about NLB tools as it is not required.\)|

After you have a virtual machine template that meets the virtual machine template prerequisites, create a service template that uses the virtual machine template. The following procedure assumes you have an existing service template. For information about how to create a service template, see [How to create a service template in VMM](./How-to-create-a-service-template-in-VMM.md).

### To add an NLB load balancer to a service tier

1.  Open an existing service template that meets the prerequisites that are outlined in the “Virtual Machine Template Prerequisites” section of this topic. To do this, follow these steps:

    1.  Open the **Library** workspace.

    2.  In the **Library** pane, expand **Templates**, and then click **Service Templates**.

    3.  In the **Templates** pane, click the service template that you want to open.

    4.  On the **Service Template** tab, in the **Actions** group, click **Open Designer**.

        The **Virtual Machine Manager Service Template Designer** opens with the service template displayed.

2.  Click the virtual machine template that represents the tier that you want to load balance. In the virtual machine template details pane, select the **This computer tier can be scaled out** check box, and configure the number of instances.

3.  On the **Home** tab, in the **Service Template Components** group, click **Add Load Balancer**.

    > [!NOTE]
    > This action is only available if VIP templates are defined in the Fabric workspace. Only a full administrator or delegated administrator can configure VIP templates.

4.  Make sure that the correct VIP template for NLB is selected. To do this, follow these steps:

    1.  Click the load balancer object \(identifiable by the VIP template name\) that is added to the service map.

    2.  In the load balancer details, in the **Load Balancer VIP Profile** list, select a different VIP template if needed.

    3.  Verify that the **Load Balancer Model** field indicates **Network Load Balancing \(NLB\)**.

5.  Configure the load balancer connection to a virtual network adapter for the service tier.

    1.  On the **Home** tab, in the **Tools** group, click the **Connector** tool to select it.

    2.  On the service map, click the **Server connection** object that is associated with the load balancer, and then click a **NIC** object \(for example, you could click the network adapter for a logical network called **Management**\). This connects the load balancer to the network adapter.

    3.  Click the **NIC** object to display its properties in the detail area. Verify that the IPv4 address type, the IPv6 address type, or both types \(depending on the logical network configuration\) are static, and that the MAC address type is static.

6.  Configure the client connection for the load balancer to use the correct logical network. With the Connector tool still selected, on the service map, click the **Client connection** object that is associated with the load balancer, and then click a logical network object. For example, you could click a logical network called **Management**. This connects the load balancer to the logical network.

    > [!IMPORTANT]
    > For NLB deployments, the logical network that is associated with the client connection and the logical network of the NIC that is associated with the server connection in step 5 must be the same.

7.  Save the updated service template settings. On the **Home** tab, in the **Service Template** group, click **Save and Validate**.

> [!IMPORTANT]
> When the service is deployed, [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] automatically selects a virtual IP address from the reserved range that is defined in the static IP address pool, and assigns it to the load\-balanced service tier. To enable users to connect to the service, the following must occur:
> 
> -   A full administrator or delegated administrator must determine the virtual IP address that [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] assigned to the load balancer.
> -   After the virtual IP address is determined, a Domain Name System \(DNS\) administrator must manually create a DNS entry for the virtual IP address. The DNS entry for the virtual IP address should be the name that users will specify to connect to the service, for example *ServiceName.contoso.com*.
> 
> For more information, see [How to determine the virtual IP address for a service](./How-to-determine-the-virtual-IP-address-for-a-service.md).

## See Also
[How to add networking components to a service template](./How-to-add-networking-components-to-a-service-template.md)
[Configuring load balancing in VMM](./Configuring-load-balancing-in-VMM.md)
[How to configure a hardware load balancer for a service tier](./How-to-configure-a-hardware-load-balancer-for-a-service-tier.md)
[How to deploy a service in VMM](./How-to-deploy-a-service-in-VMM.md)
[Creating service templates in VMM](./Creating-service-templates-in-VMM.md)
[Managing services with VMM](./Managing-services-with-VMM.md)
[Managing tenant resources with VMM](./Managing-tenant-resources-with-VMM.md)


