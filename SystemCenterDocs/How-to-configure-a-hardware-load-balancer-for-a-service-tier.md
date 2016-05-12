---
title: How to configure a hardware load balancer for a service tier
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b7b42324-7f1f-4d5b-8050-b0ddc3aca44c
---
# How to configure a hardware load balancer for a service tier
In [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)], a service is a set of virtual machines that are configured and deployed together and are managed as a single entity—for example, a deployment of a multi\-tier line\-of\-business application.

Use the following procedures to configure a hardware load balancer for one or more tiers of a service template in [!INCLUDE[vmm12short](Token/vmm12short_md.md)]. For example, you might configure a load balancer for a Web tier and for a middle business logic tier.

> [!NOTE]
> A load balancer must be configured before you deploy a service. After a service is deployed, you cannot add a load balancer by updating the service.

**Account requirements** To configure the fabric prerequisites, you must be an administrator or a delegated administrator. Delegated administrators can only configure the prerequisites that are within the scope of their user role. To add a load balancer to a service template, you must be an administrator, a delegated administrator, or a member of a self\-service user role that has the **Author** action in their scope.

## Fabric prerequisites
Before you begin this procedure, make sure that the following prerequisites are met:

-   Create the desired logical networks and VM networks, with one or more associated network sites. Ensure that the network sites where users will deploy the service have one or more associated IP subnets that you can create static IP address pools from. Also, ensure that you associate each network site with the host group or one of its parent host groups where the service may be deployed. For more information, see:

    -   [How to create a logical network and IP address pools in VMM](How-to-create-a-logical-network-and-IP-address-pools-in-VMM.md)

    -   [How to create a VM network for a VLAN in VMM](How-to-create-a-VM-network-for-a-VLAN-in-VMM.md)

    -   [How to create a VM network for network virtualization and add an IP address pool in VMM](How-to-create-a-VM-network-for-network-virtualization-and-add-an-IP-address-pool-in-VMM.md)

-   Create static IP address pools that are associated with the network sites where users will deploy the service. The IP address pool must contain a reserved range of virtual IP addresses that can be assigned to the load balancer. You must set up the static IP address pools for the load balancer and for the virtual machines that will be placed behind the load balancer. These can be from the same pool or from different pools, but the environment must have both virtual IP addresses and IP addresses for the virtual machines. For more information, see [How to create a logical network and IP address pools in VMM](How-to-create-a-logical-network-and-IP-address-pools-in-VMM.md) or [How to create a VM network for network virtualization and add an IP address pool in VMM](How-to-create-a-VM-network-for-network-virtualization-and-add-an-IP-address-pool-in-VMM.md).

-   Configure a hardware load balancer in [!INCLUDE[vmm12short](Token/vmm12short_md.md)]. You must have a supported hardware load balancer, and you must have installed the load balancer provider on the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] management server. When you configure the load balancer, you must select the host group or one of its parent host groups where the service may be deployed. Also, when you configure logical network affinity, make sure that you select the logical networks from which the load balancer can obtain its virtual IP address as the front\-end, and the logical networks to which you want to make the load balancer available for connections from the virtual machines that make up a service tier as the back\-end. For more information, see [How to add hardware load balancers in VMM](How-to-add-hardware-load-balancers-in-VMM.md).

-   Create a virtual IP \(VIP\) template for the hardware load balancer. For more information, see [How to create VIP templates for hardware load balancers in VMM](How-to-create-VIP-templates-for-hardware-load-balancers-in-VMM.md).

-   Ensure that the hosts where the service may be deployed can access the load balancer. Therefore, the host group where the load balancer is available must be the host group of the virtual machine host or one of its parent host groups.

-   On each host where the service may be deployed, ensure that a physical network adapter on the host is configured to use the same logical network that the service tier will use. For example, if the tier will use a logical network called **Management**, that logical network must be associated with a physical adapter on the host. For more information, see [How to configure network settings on a Hyper-V host in VMM](How-to-configure-network-settings-on-a-Hyper-V-host-in-VMM.md), see [How to configure network settings on a host by using a logical switch in VMM](How-to-configure-network-settings-on-a-host-by-using-a-logical-switch-in-VMM.md), or see [How to configure network settings on a VMware ESX host in VMM](How-to-configure-network-settings-on-a-VMware-ESX-host-in-VMM.md).

> [!NOTE]
> For an overview of the load balancer workflow, see the [Hardware load balancer workflow](Configuring-load-balancing-in-VMM.md#BKMK_hw) section of "Configuring Load Balancing in VMM Overview."

#### To add a load balancer to a service tier

1.  Open the service template in the **Virtual Machine Manager Service Template Designer**. To do this, follow these steps:

    1.  Open the **Library** workspace.

    2.  In the **Library** pane, expand **Templates**, and then click **Service Templates**.

    3.  In the **Templates** pane, click the service template that you want to open.

    4.  On the **Service Template** tab, in the **Actions** group, click **Open Designer**.

        The **Virtual Machine Manager Service Template Designer** opens with the service template displayed.

2.  On the **Home** tab, in the **Service Template Components** group, click **Add Load Balancer**.

    > [!NOTE]
    > This action is only available if VIP templates are defined in the Fabric workspace. Only a full administrator or delegated administrator can configure VIP templates.

3.  Click the load balancer object \(identifiable by the VIP template name\) that is added to the service map. In the load balancer details, select a different VIP template if needed.

4.  Configure the load balancer connection to a virtual network adapter for the service tier.

    1.  On the **Home** tab, in the **Tools** group, click the **Connector** tool to select it.

    2.  On the service map, click the **Server connection** object that is associated with the load balancer, and then click a **NIC** object \(for example, you could click the network adapter for a logical network called **Management**\). This connects the load balancer to the network adapter.

    3.  Click the **NIC** object to display its properties in the detail area. Verify that the IPv4 address type, the IPv6 address type, or both types \(depending on the logical network configuration\) are static, and that the MAC address type is static.

5.  Configure the client connection for the load balancer to use the correct logical network. With the Connector tool still selected, on the service map, click the **Client connection** object that is associated with the load balancer, and then click a logical network object. For example, you could click a logical network called **Management**. This connects the load balancer to the logical network.

6.  Save the updated service template settings. On the **Home** tab, in the **Service Template** group, click **Save and Validate**.

> [!IMPORTANT]
> When the service is deployed, [!INCLUDE[vmm12short](Token/vmm12short_md.md)] automatically selects a virtual IP address from the reserved range that is defined in the static IP address pool, and assigns it to the load\-balanced service tier. To enable users to connect to the service, the following must occur:
> 
> -   A full administrator or delegated administrator must determine the virtual IP address that [!INCLUDE[vmm12short](Token/vmm12short_md.md)] assigned to the load balancer.
> -   After the virtual IP address is determined, a Domain Name System \(DNS\) administrator must manually create a DNS entry for the virtual IP address. The DNS entry for the virtual IP address should be the name that users will specify to connect to the service, for example *ServiceName.contoso.com*.
> 
> For more information, see [How to determine the virtual IP address for a service](How-to-determine-the-virtual-IP-address-for-a-service.md).

## See Also
[How to add networking components to a service template](How-to-add-networking-components-to-a-service-template.md)
[How to configure NLB for a service tier](How-to-configure-NLB-for-a-service-tier.md)
[Configuring load balancing in VMM](Configuring-load-balancing-in-VMM.md)
[How to deploy a service in VMM](How-to-deploy-a-service-in-VMM.md)
[Creating service templates in VMM](Creating-service-templates-in-VMM.md)
[Managing services with VMM](Managing-services-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


