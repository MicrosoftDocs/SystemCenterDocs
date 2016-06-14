---
title: Configuring load balancing in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0add8a3b-884e-4fe3-8bac-8834ed4f8d5d
---
# Configuring load balancing in VMM
Networking in [!INCLUDE[vmm12sp1_long](../../includes/vmm12sp1_long_md.md)] includes load balancing integration, so that you can automatically provision load balancers in your virtualized environment. Load balancing integration works together with other network enhancements in [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)]. For information about these enhancements, see the list of topics at the end of this topic.

## <a name="BKMK_LoadBalancerIntegration"></a>Load balancer integration
By adding a load balancer to [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)], you can load balance requests to the virtual machines that make up a service tier. You can add supported hardware load balancers through the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] console or, for some configurations, you can use Microsoft Network Load Balancing \(NLB\). NLB is included as a possible load balancer when you install [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)]. NLB uses round robin as the load\-balancing method.

> [!NOTE]
> -   Service tiers running Linux cannot use NLB.
> -   VM networks configured with network virtualization cannot use NLB.
> 
> Both of the previous configurations can use hardware load balancing instead.

To add supported hardware load balancers, you must install a configuration provider that is available from the load balancer manufacturer. The configuration provider is a plug\-in to [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] that translates [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] PowerShell commands to API calls that are specific to a load balancer manufacturer and model.

Before you can use a hardware load balancer or NLB, you must create associated virtual IP \(VIP\) templates.

### VIP templates
A virtual IP \(VIP\) template contains load balancer\-related configuration settings for a specific type of network traffic. For example, you could create a template that specifies the load balancing behavior for HTTPS traffic on a specific load balancer manufacturer and model. These templates represent the best practices from a load balancer configuration standpoint.

After you create a VIP template, users \(including self\-service users\) can specify the VIP template when they create a service. When a user models a service, they can pick an available template that best matches their needs for the type of load balancer and the type of application.

> [!NOTE]
> For information about how to create VIP templates, see [How to create VIP templates for hardware load balancers in VMM](How-to-create-VIP-templates-for-hardware-load-balancers-in-VMM.md) and [How to create VIP templates for Network Load Balancing &#40;NLB&#41; in VMM](How-to-create-VIP-templates-for-Network-Load-Balancing--NLB--in-VMM.md).

### <a name="BKMK_hw"></a>Hardware load balancer workflow
The following list describes the hardware load balancer workflow to load balance a service tier:

1.  In the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] console, while creating a static IP address pool, the administrator configures a reserved range of virtual IP addresses.

    > [!NOTE]
    > This step can be performed at any time before deploying a service that uses a load balancer. You must have one virtual IP address for each service tier that uses load balancing.

2.  The administrator installs the load balancer configuration provider on the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management server.

    > [!NOTE]
    > For information about supported load balancers and how to obtain configuration providers, see the “Prerequisites” section of [How to add hardware load balancers in VMM](How-to-add-hardware-load-balancers-in-VMM.md).

3.  In the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] console, the administrator adds the load balancer to [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management. Through the Add Load Balancer wizard, the administrator does the following:

    -   Selects the host groups where the load balancer will be available

    -   Specifies the load balancer manufacturer and model

    -   Specifies the load balancer DNS names \(or IP addresses\) and the port number that is used for load balancer management

    -   Specifies the affinity to logical networks

    -   Selects the configuration provider

    -   Optionally tests the connection to the load balancer

4.  In the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] console, the administrator creates one or more VIP templates. Through the Load Balancer VIP Template wizard, the administrator defines the following:

    -   The port to use for the type of network traffic that will be load balanced

    -   Whether the template applies to any supported load balancer or to a specific type of load balancer

    -   The type of protocol to load balance \(for example HTTPS\)

    -   Whether to enable session persistence

    -   Optional health monitors that can be configured to periodically check that the load balancer is responsive

    -   The type of load balancing method to use

    For more information, see [How to create VIP templates for hardware load balancers in VMM](How-to-create-VIP-templates-for-hardware-load-balancers-in-VMM.md).

5.  A user \(typically a self\-service user\) creates a service template. In the Service Template Designer window, they add a load balancer to a service tier, and then select which VIP template to use. When the service is deployed, [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] automatically selects a virtual IP address from the reserved range in the static IP address pool and assigns it to the load balancer. This IP address is considered the “front\-end” IP address for a load\-balanced service tier. [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] also assigns static IP addresses to the virtual machines that make up the service tier. These are considered “back\-end” dedicated IP addresses, as they are behind the load balancer.

6.  After the service is deployed, the administrator verifies in the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] console which virtual IP address is being used as the front\-end IP address for the service tier. The administrator then contacts the DNS administrator to create a DNS entry for the assigned virtual IP address. For example, if the front\-end Web tier of a service is load balanced, the administrator can verify which virtual IP address is used for that tier. The DNS administrator can then create an entry in DNS for the name that users will specify to connect to the Web front\-end. For example, the DNS administrator could create a DNS entry for *ServiceName*.contoso.com with the corresponding virtual IP address.

    > [!NOTE]
    > For more detailed information about how to load\-balance a service tier by using a hardware load balancer, see [How to add networking components to a service template](How-to-add-networking-components-to-a-service-template.md) and [How to configure a hardware load balancer for a service tier](How-to-configure-a-hardware-load-balancer-for-a-service-tier.md).

### NLB workflow
The following list describes the NLB workflow to load balance a service tier. However, in service tiers running Linux, or in a service where the VM networks are configured with network virtualization, you cannot use the NLB workflow. Instead, use the [Hardware load balancer workflow](Configuring-load-balancing-in-VMM.md#BKMK_hw), listed earlier in this topic.

This is the NLB workflow:

1.  In the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] console, while creating a static IP address pool, the administrator configures a reserved range of virtual IP addresses.

    > [!NOTE]
    > This step can be performed at any time before deploying a service that uses a load balancer. You must have one virtual IP address for each service tier that uses load balancing.

2.  In the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] console, the administrator creates one or more VIP templates. Through the Load Balancer VIP Template wizard, the administrator defines the following:

    -   The port to use for the type of network traffic that will be load balanced

    -   The template type \(in this case, the Specific template type, set to Microsoft NLB\)

    -   The type of protocol to load balance \(TCP, UPD, or both\)

    -   Whether to enable session persistence

3.  A user \(typically a self\-service user\) configures a service template by doing the following:

    -   For the tier that will be load balanced, the user must specify a virtual machine template that meets the specific configuration requirements for NLB. For information about the configuration requirements, see [How to configure NLB for a service tier](How-to-configure-NLB-for-a-service-tier.md).

    -   In the Service Template Designer window, the user adds a load balancer, and then selects which VIP template to use.

    When the service is deployed, [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] automatically selects a virtual IP address from the reserved range in the static IP address pool and assigns it to a load\-balanced service tier. [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] also assigns static IP addresses to the virtual machines that make up the service tier.

4.  After the service is deployed, the administrator verifies in the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] console which virtual IP address is being used for a service. The administrator then contacts the DNS administrator to create a DNS entry for the assigned virtual IP address. For example, if the front\-end Web tier of a service is load balanced, the administrator can verify which virtual IP address is used for that tier. The DNS administrator can then create an entry in DNS for the name that users will specify to connect to the Web front\-end. For example, the DNS administrator could create a DNS entry for *ServiceName*.contoso.com with the corresponding virtual IP address.

    > [!NOTE]
    > For more detailed information about how to load\-balance a service tier by using NLB, see [How to configure NLB for a service tier](How-to-configure-NLB-for-a-service-tier.md).

## In this section
To configure load balancing in your virtualized environment, follow these procedures:

|Procedure|Description|
|-------------|---------------|
|[How to add hardware load balancers in VMM](How-to-add-hardware-load-balancers-in-VMM.md)|Describes how to add supported hardware load balancers to the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] environment so that you can load balance service requests. **Note:** If you want to use Microsoft Network Load Balancing \(NLB\), you do not have to add a hardware load balancer. When you install [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)], NLB is automatically included as a load balancer. To use NLB, you must create NLB virtual IP templates, described in the last row of this table.|
|[How to create VIP templates for hardware load balancers in VMM](How-to-create-VIP-templates-for-hardware-load-balancers-in-VMM.md)|Describes how to create VIP templates that you can use during service creation to help choose a hardware load balancer that best suits the need of the application.|
|[How to create VIP templates for Network Load Balancing &#40;NLB&#41; in VMM](How-to-create-VIP-templates-for-Network-Load-Balancing--NLB--in-VMM.md)|Describes how to create NLB VIP templates that you can use during service creation to configure NLB for a service tier.|

## See Also
[Overview: plan logical networks, network sites, and IP address pools in VMM](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md)
[Overview: plan logical switches and port profiles in VMM](Overview--plan-logical-switches-and-port-profiles-in-VMM.md)
[Prerequisites for gateways in VMM](Prerequisites-for-gateways-in-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


