---
ms.assetid: de3c13d3-f817-4c1d-875b-f878e53f0ba8
title: Integrate load balancing with VMM service templates
description: This article provides guidance for setting up load balancing for VMM service tiers
author: jyothisuri
ms.author: jsuri
ms.date: 08/21/2024
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy24
---


# Integrate load balancing with VMM service templates



Read this article to learn about integrating Windows network load balancing (NLB) and hardware load balancers with System Center Virtual Machine Manager (VMM) service templates.


Service templates group VMs together to provide an app. They contain information about a service, including the VMs that are deployed as part of the service, the applications installed on VMs, and the network settings that must be used. You can add VM templates, network settings, applications, and storage to a service template.

Service templates can be single or multi-tier. A single tier service contains one VM used as a specific app. A multi-tier service contains multiple VMs. [Learn more](library-service-templates.md).



## Set up load balancing for a service tier

You can add a load balancer to load balance requests to VMs in a service tier. You can use a hardware load balancer or NLB for round robin balancing.

To add a load balancer, you'll need to do the following:

- Ensure you have [logical networks configured](network-logical.md). The logical networks must have associated network sites. Those network sites must have one or more associated subnets from which you can create static IP address pools. In addition, associate each network site with the host group where the service will be deployed.
- [Create an IP address pool](network-pool.md) for the logical networks. The IP pool must contain a reserved range of virtual IP addresses that can be assigned to the load balancer. You must set up the static IP address pools for the load balancer and for the virtual machines behind the load balancer. These can be from the same pool or from different pools, but you'll need both VIPs and IP addresses for the virtual machines.
- [Create VM networks](network-virtual.md) on top of logical networks.
- [Create VIP templates](network-nlb.md#create-vip-templates): A virtual IP (VIP) template contains load balanced settings for a specific type of network traffic. After you create a VIP template, you can specify it when you set up load balancing in a service template.
- [Set up a hardware load balancer](network-nlb.md#set-up-a-hardware-load-balancer): If you want to enable hardware load balancing in a service template, there are many prerequisites you'll need to prepare.
- [Set up NLB](network-nlb.md#set-up-nlb): If you don't want to use a hardware load balancer, you can use NLB. There are some requirements and limitations.

### Create VIP templates

1. In the VMM console, select **Fabric** > **Networking** > **VIP Templates**.
2. Select **Home** > **Show** > **Fabric Resources**  > **Create** > **Create VIP Template**.
3. In the **Load Balancer VIP Template Wizard** > **Name**, specify the template name and description. In **VIP port**, specify the port that will be used for the type of network traffic you want to balance. For example, 443 for HTTPS traffic. In **Backend port**, specify the portal on which the backend server is listening for requests.
4. In **Type**, do the following:

	- To use NLB, select **Microsoft** in the manufacturer list and **Microsoft network controller** in **Model**.
	- To use a hardware load balancer, select **Generic** to create a template for any supported hardware load balancer. Select **Specific** to create a template for a specific load balancer and specify the manufacturer and model.

5. In **Protocol**, select the protocol for which you want to create the VIP template.

	- If you select **HTTPS**, you'll need to specify where the traffic terminates.
	- Select **HTTPS passthrough** to pass the traffic to the VM without decrypting it.
	- Select **HTTPS terminate** to terminate and decrypt the HTTPS traffic at the load balancer. This option gives the load balancer more information, such as cookies and headers. To use this option, specify the subject name of a certificate on the load balancer that can be used for HTTPS authentication. With this option, you can enable **Re-Encrypt** to re-encrypt the HTTPS traffic from the load balancer to the VM.
	- Select **Custom** to specify **TCP**, **UDP**, or both.

6. In **Persistence**, select **Enable persistence** to make the client session sticky (affinity). This setting means that the load balancer will always try to direct the same client to the same VM. It's based on the specified source IP address and subnet mask, the destination IP address, and other parameters that vary depending on the protocol.
7. In **Health Monitors**, you can optionally specify that a verification must run against the load balancer at regular intervals. To add a health monitor, specify the protocol and the request. For example, entering the command GET? makes an HTTP GET request for the home page of the load balancer and checks for a header response. You can also modify the response type, monitoring interval, timeout, and retries.

> [!NOTE]
> The timeout must be less than the interval.

8. In **Load Balancing**, select which load balancing method you want to use. You can configure new connections to be directed based on the least connections or the fastest response time, using round robin, or using a custom method supported by the load balancer. If you're enabling NLB, select **Round Robin**.
9. On the **Summary** page, review the settings and select **Finish**. The **Jobs** dialog appears. Wait for a **Completed** status. Then verify that the template appears in the **VIP Templates** pane.


### Set up a hardware load balancer

Set up a hardware load balancer as follows:

- **Get a configuration provider**: To add a supported hardware load balancer, you'll need to download and install a configuration provider available from the load balancer manufacturer. VMM currently supports [Brocade ServerIron ADX load balancer provider](http://www.brocade.com/partnerships/technology-alliance-partners/partner-details/microsoft/microsoft-systems-center/index.page) and [Citrix NetScaler load balancer provider](https://www.citrix.com/community.html). The provider is a VMM plug-in that translates VMM PowerShell commands to the load balancer API. After you've installed the provider, you must restart the VMM service (**net stop scwmmservice** > **net start scvmmservice**).
- **Set up an account**: Create a VMM Run As account with a username and password with permissions to configure the downloaded load balancer.
- **Add the load balancer to VMM**: Add a hardware load balancer to VMM using the Add Load Balancer Wizard.

#### Add the hardware load balancer to VMM

During the wizard, select the host groups for which the load balancer is available, specify the load balancer model, specify the address and port used to manage the load balancer, specify affinity to VMM logical network, select the configuration provider, and test the connection. You'll need to configure the hardware load balancer before you deploy a service. After the service is deployed, a load balancer can't be added.

1. Select **Fabric** > **Networking** > **Load Balancers** > **Fabric Resources** > **Home** > **Add** > **Add Resources** > **Load Balancer**.
2. In **Add Load Balancer Wizard** > **Credentials**, select the Run As account with the load balancer credentials.
3. In **Host Group**, select each host group where the service will be deployed. Hosts must be able to access the load balancer. In addition, a physical network adapter on the host must be configured to use the same logical network as the service tier.
4. In **Manufacturer and Model**, select the appropriate entries.
5. In **Address**, specify the **IP address** and **FQDN** or **NetBIOS** names of the load balancer. Specify the port on which the load balancer listens for requests.
6. In **Logical Network Affinity**, specify the affinity to logical networks. 

>[!NOTE]
> - For frontend affinity, you'll select the logical network from which the load balancer obtains its VIP. The VIP is the IP address that's assigned to the load balancer when you deploy it in a service template.
> - For frontend affinity, based on the logical networks, VMM determines the static IP address pools that are accessible from both the load balancer and from the relevant host group.
> - When selecting logical networks for frontend affinity, the associated network site with the reserved VIP address range must be available to the host groups associated with the load balancer.
> - For backend affinity, you'll select the logical networks to which you want to make the load balancer available for connections from the VMs in a service tier.

7. In **Provider**, select the load balancer provider. Select **Test** to check the configuration.
8. In **Summary**, verify the settings and select **Finish**. The **Job** dialog box appears. Wait for a **Completed** status and check in the **Provider** column that the provider is active.

### Set up NLB

NLB is automatically included as a load balancer in VMM. As long as you've set up an NLB VIP template, no other action is required, but note that:

- NLB can't be used if VM networks are configured with network virtualization.
- NLB can't be used in service tiers running Linux VMs.

### Enable load balancing
1. If the service template isn't open, select **Library** > **Templates** > **Service Templates** and open it.
2. Select **Actions** > **Open Designer**.
3. In the Service Template Designer, select the **Service Template Components** group > **Add Load Balancer**.
4. Select the load balancer object. You'll identify it with the VIP template name.
5. Select **Tool** > **Connector**. Select the **Server connection** associated with template and then select a **NIC** object to connect the load balancer to the adapter. In the NIC properties, check the address types and that the MAC address is static.
6. With the **Connector** enabled, select the **Client connection** associated with the load balance and then select a logical network object.
7. Save the service template in **Service Template** > **Save and Validate**.

### Set up the hardware VIP for user access

When the service is deployed, VMM automatically selects a VIP from the reserved range in the static IP address pool and assigns it to the load-balanced service tier. To enable users to connect to the service, after the service is deployed, you need to determine the VIP and configure a DNS entry for it.

1. After the service is deployed, select **Fabric** > **Networking** > **Load Balancers**.
2. Select **Show** > **Service** > **Load Balancer Information for Services** and expand the service to see which VIP is assigned.
3. Request that the DNS administrator manually create a DNS entry for the VIP. The entry must be the name that users will specify to connect to the service. For example, servicename.contosol.com.

## Next steps

You can also [set up a software load balancer](sdn-slb.md) in a software defined networking (SDN) infrastructure in the VMM fabric.
