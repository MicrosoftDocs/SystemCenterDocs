---
title: Deploy a Software Load Balancer using VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.service: virtual-network
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2f57fc14-4b23-41e9-87dc-51a0b998b321
---
# Deploy a Software Load Balancer using VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

## Introduction

This topic helps you evaluate the Software Defined Networking (SDN) features in [!INCLUDE[winthreshold_server_2_mdToken/winthreshold_server_2_md.md)] 5 and Virtual Machine Manager Technology Preview 5. In particular, this topic is focused on deploying and configuring Microsoft Software Load Balancer (SLB) using VMM Technical Preview 5.

After you use VMM to deploy a network controller and a SLB, you can leverage multiplexing and NAT capabilities in your Software Defined Networking (SDN) infrastructure.

## Prerequisites

Before you get into the details of the SLB deployment, make sure you have performed following steps:

* Deploy the network controller 

  You must have already deployed the network controller with VMM. After the network controller is successfully deployed, you have basic compute and network infrastructure ready to proceed for SLB deployment.

  For more information about network controller deployment using VMM, see [Deploy a Network Controller using VMM](Deploy-a-Network-Controller-using-VMM.md).

  If you haven’t yet deployed a network controller, please see the previous topic and come back to this section when complete.

* Prepare an SSL Certificate

  The SLB service template requires you to prepare an SSL certificate prior to importing the service template. You should already have these certificates ready as part of network controller deployment. See the **Prepare an SSL Certificate** section in [Deploy a Network Controller using VMM](Deploy-a-Network-Controller-using-VMM.md).

 Right-click the SSL certificate created earlier during network controller deployment and export it without a password in .CER format. Later, this certificate will be placed in the NCCertificate.CR folder. Details are provided later.

## Setup
This section covers the setup required for deploying the Software Load Balancer.

#### Topology overview 

Refer to the topology diagram in the following Microsoft TechNet Library topic: [Plan a Software Defined Network Infrastructure](https://technet.microsoft.com/library/mt605207.aspx)

The diagram shows a sample 4-node setup. The setup is highly available with three network controller nodes (virtual machines), and three SLB/MUX nodes. It shows two tenants with one virtual networks broken into two virtual subnets to simulate a web tier and a database tier. Both the infrastructure and tenant virtual machines can be redistributed across any physical host.

All the Software Load Balancer virtual machines must have [!INCLUDE[winthreshold_server_2_mdToken/winthreshold_server_2_md.md)] 5 with the Zero Day Patch as the operating system.

### Logical networks

In addition to the Management and HNV Provider logical networks that you already have configured during network controller deployment, you need the Transit (sometimes called Front End), Private VIP and Public VIP networks to deploy the SLB. Refer to the [Plan a Software Defined Network Infrastructure](https://technet.microsoft.com/library/mt605207.aspx) topic for more information about these networks.
                                                                                                                                    
Normally you would use the Transit network for BGP peering. But because of a limitation in [!INCLUDE[winthreshold_server_2_mdToken/winthreshold_server_2_md.md)] 5, the SLB actually uses the Management network for BGP peering. However, this doesn’t impact how you deploy the SLB.  

Active Directory and DNS must be available and reachable from these networks. You must have Domain Administrator credentials and the ability to create DNS entries in the domain.

##### To create the Transit logical network


1.  From the VMM console, start the **Create logical network Wizard**.

2.  Type a name and optional description for this network and click **Next**.

3.  On the **Settings** page, ensure you select **One Connected Network**. Check **Create a VM network with the same name** box to allow virtual machines to access this logical network directly and the **Managed by the network controller** box then click **Next**.

4.  On the **Network Site** panel, add the network site information for your subnet.

5.  Review the **Summary** information and complete the logical network wizard

##### To create an IP address pool for Transit logical network

This is the IP address pool where DIPs are assigned to the SLB/MUX virtual machines and BGP Peer virtual machine (if deployed).

Create the IP pool for the Transit network following the same procedure and steps as the HNV Provider network steps in [Deploy a Network Controller using VMM](Deploy-a-Network-Controller-using-VMM.md). 

Ensure you use the IP address range that corresponds to your Transit network IP address space.
>[!IMPORTANT] Don't include the first three IP addresses of your subnet in the IP pool you are about to create. For example, if your available subnet is from .1 to .254, start your range at .4.

After you create the Transit logical network, ensure you associate this logical network with the Management switch uplink port profile you created during the network controller deployment.

![VMM MGMT Uplink PP PropertiesImage/VMM-MGMT-Uplink-PP-Properties.png)

##### Private VIP logical network 

You need a private VIP address pool to assign a VIP to the Software Load Balancer Manager (SLBM) service.

You will create a Private VIP logical network in order to assign private VIP address to SLBM service.

###### To create a Private VIP logical network

1.  Start the **Create logical network Wizard**.

2.  Type a name and optional description for this network. Click **Next**.

3.  On the **Settings** page, ensure you select **One Connected Network**.  check **Create a VM network with the same name** box to allow virtual machines to access this logical network directly and the **Managed by the network controller** box then click **Next**.

4.  On the **Network Site** panel, add the network site information for your Private VIP logical network.

5.  Review the Summary information and complete the wizard.

###### To create a Public VIP logical network

1.  Start the **Create logical network Wizard**.

2.  Type a name and optional description for this network and click **Next**.

3.  On the **Settings** page, ensure you select **One Connected Network**. Check the **Create a VM network with the same name** box to allow virtual machines to access this logical network directly and the **Managed by the network controller** box. Also select **Public IP Address Network** and then click **Next**.

4.  On the **Network Site** panel, add the network site information for your Public VIP network. This should include the Host Group and subnet information for your Public VIP network.

5.  Review the **Summary** information and complete the logical network wizard


>[!IMPORTANT] At this point you can’t create a VIP Pool because the SLB is not deployed yet. But you can choose the last VIP from the Private VIP logical network subnet you just configured and use it later to assign to the SLB Manager VIP. Ensure this assigned VIP address is part of the Private VIP Pool you will create later.

## Deployment


Now you can deploy the SLB/MUX into your SDN infrastructure.

### Download the service template to a local computer

First, you need to download the SLB/MUX service template from the [Microsoft SDN GitHub repository](https://github.com/Microsoft/SDN/tree/master/VMM/Templates/SLB) and extract the contents to a folder on a local computer. You will see two custom resource folders named **NCCertificate.CR** and **EdgeDeployment.CR** in the downloaded content. You must copy these two folders into your VMM Library and refresh the library.

There are two Service Templates for the SLB at this location. The *SLB Production Generation 2 VM* template is for deploying the SLB Service on Generation 2 virtual machines and *SLB Production Generation 1 VM* is for deploying the SLB Service on Generation 1 virtual machines. Both the templates have a default count of three virtual machines which can be changed in the Service Template designer.

Copy the .CER certificate that you previously created to the **NCCertificate.CR** folder.

### To import the service template into the VMM library

Now you can import the SLB/MUX service template into the VMM library.

1.  In the VMM console, navigate to **Library**.

2.  In the top of the left pane, in the **Templates** section, select **Service Templates**.

3.  In the ribbon at the top, click **Import Template**.

4.  Browse to your service template directory, select the **SLB Production Generation 1 VM.xml** file and follow the prompts to import it.

5.  This service template uses the following virtual machine configuration parameters. Update the parameters to reflect your environment configuration.

Configuration parameters:

| Resource type| Resource name and description|
|--------------|------------------------------|
| Library Resources | Resource name: WinServer.vhd<br><br>Description: Windows Server Virtual Hard Disk. Format can be VHD or VHDX, depending on the service template you choose.<br>Select the base VHD image that you downloaded and imported to the VMM Library earlier during the network controller deployment.<br><br>Resource name: NCCertificate.cr<br><br>Description: A custom library resource that contains the trusted root certificate (.CER) for the network controller. This will be used for secure communications between the network controller and the SLB MUX instances.<br>Map to the NCCertificate.cr library resource in your VMM library.<br><br>Resource Name: EdgeDeployment.cr<br><br>Description: A custom library resource.<br>Select the **EdgeDeployment.cr** library resource that you prepared earlier and imported into you VMM library. |

### Configure the deployment

Use the following procedure to deploy an SLB/MUX service instance.

##### To configure the deployment

1.  Select the **SLB Production Generation 1 VM.xml** service template and click **Configure Deployment** to begin. Type a name and optional destination for the service instance. The destination must map to a Host Group that contains the hosts configured previously.

2.  In the **Network Settings** section, you must map the networks as follows.

| Network setting   | Value                                             |
|-------------------|---------------------------------------------------|
| TransitNetwork | Map this to your Transit VM network. |
| ManagementNetwork | Map this to your Management VM network.           |

After you are done with mapping the destination and network settings, the **Deploy Service** dialog appears. It is normal for the virtual machine instances to be initially red. Click **Refresh Preview** to automatically find suitable hosts for the virtual machine.

On the left side of the **Configure Deployment** window, there are a number of settings that you must configure. The table below summarizes each field:

| Setting| Requirement| Description|
|--------|------------|------------|
| Datacenter Network|Required| Your Transit VM network
|LocalAdmin|Required|Select a **Run as** account in your environment which will be used as the local Administrator on the virtual machines.<br>User name should be .\Administrator   
|Management Network|Required| Choose the Management VM network that you created for host management.                                                                                
| MgmtDomainAccount| Required| Select a **Run as** account that has the privilege to add the SLB/MUX virtual machines to the Active Directory Domain associated with the network controller. This can be the same account you used in MgmtDomainAccount while deploying the network controller.|
| MgmtDomainFQDN| Required| Fully qualified domain name for the Active directory domain that the SLB/MUX virtual machines will join.<br>Example: ``Contoso.com``                                                              
| SelfSignedConfiguration | Required| Enter True if the certificate you are using is self-signed|

##### Deploy the SLB/MUX service

After you configure these settings, click **Deploy Service** to begin the service deployment job. Deployment times will vary depending on your hardware but are typically between 30 and 60 minutes.

>[!IMPORTANT]If you are not using a Volume Licensed VHDX or if the VHDX is not supplied the Product Key using an Answer file, then the deployment will stop at the Product Key page during SLB/MUX virtual machine(s) provisioning. You need to manually access the virtual machine(s) desktop and either skip entering the product key or enter the product key if you have it handy.

If the SLB/MUX deployment fails, ensure you delete the failed instance of the Service using the following steps before you retry the SLB/MUX deployment.

#### To remove a failed SLB/MUX instance
1. Open the VMM console.
2. Select **VMs and Services**.
3. Click **All Hosts** and select the **Services** option.
4. Delete the failed SLB/MUX Service instance.

When the service deployment job has completed, verify that your service appears in the VMM console:

Open the **VMs and Services** workspace.

1.  Click **Services** in the ribbon.

2.  Verify that your SLB MUX service instance appears in the **VM Network Information for Services** window.

3.  Right-click the SLB MUX service and select **Properties** from the menu.

4.  Verify that the state is **Deployed**.

If you want to scale-in or scale-out a deployed Software Load Balancer Service instance, see [System Center: Virtual Machine Manager Engineering Blog](https://blogs.technet.microsoft.com/scvmm/2011/05/18/scvmm-2012-an-explanation-of-scale-in-and-scale-out-for-a-service/).

##### Configure the SLB role and SLB/MUX Instance Properties

Now that the service is deployed, you can configure its properties. This involves associating the SLB service instance that you deployed with network controller, and then configuring BGP peering between the SLB/MUX instance and a ToR switch or a BGP router peer.

##### Associate the SLB/MUX Instance with SLB Manager service 

1.  Open the **Fabric** workspace.

2.  Click **Network Service** to display the list of network services installed.

3.  Right-click the **network controller** service and select **Properties**.

4.  In the Wizard, Select the **Services** tab, and then click **Load Balancer Role**.

5.  Find the **Associated Service** field under **Service information** and click **Browse**.

6.  Select the SLB/MUX service instance you created earlier and click **OK**.

    ![VMM Add ServiceImage/VMM-Add-Service.png)

7.  Choose the appropriate Run as Account

8.  For the **Management IP address**, use the last IP address from the Private VIP pool you created earlier.

    ![VMM NC Properties SLBMUXImage/VMM-NC-Properties-SLBMUX.png)

9.  Optionally specify the IP address ranges to be excluded from the outbound NAT.

10.  Click the SLB/MUX instance listed under **Load Balancer Role** in the wizard.

11.  Type the local ASN for your datacenter and details for the devices or BGP peers the SLB/MUX can peer with.

12.  Click **OK**.

The SLB Service instance is now associated with the SLBM service, and you should see the SLB/MUX virtual machine instance with all the settings listed under the **Load Balancer role**.

As a quick validation step, you can also try to access the following URL from a browser on your VMM Server:
>
>``https://<RESTIP-or-FQDN>/networking/v1/loadbalancermuxes``
>
>Example:
>
>``https://10.184.108.56/networking/v1/loadbalancermuxes``
>
>This URL shows a JSON file with details about the SLB/MUX virtual machines. If the SLB/MUX is not on-boarded successfully, this URL will not be accessible.

>[!IMPORTANT]Due to a platform limitation in TP5, you must disable the IPv6 configuration from all the SLB/MUX virtual machine vNICs. 

Use the following steps to disable IPv6:

1. On the VMM Administrator Console, right-click the SLB/MUX virtual machine, select **Connect** and click **Connect via console**.
2. When you have console access to the virtual machine, press **Windows+R**, type **NCPA.cpl** and press **Enter**.
3. Select a vNIC on the Network Connections dialog, right-click the vNIC and select **Properties**.
4. Uncheck the **Internet Protocol Version 6(TCP/IPv6)** checkbox if its enabled as shown in the screenshot below
    a.  Repeat this step for all the vNICs in Network Connections.
![VMM Network ConnectionsImage/VMM-Network-Connections.png)    
5. Repeat Steps 1-4 for all the SLB/MUX virtual machines.

Since the SLB/MUX is now on-boarded and SLB Manager VIP is assigned, you can now proceed to create IP pools for the Private VIP and Public VIP logical networks you created earlier.

##### To create VIP address pool in the Private VIP logical network

1.  Right-click the Private VIP logical network in VMM and select **Create IP Pool** from the drop down menu.

2.  Provide a name and optional description for the IP Pool and ensure that the Private VIP logical network is selected for the logical network. Click **Next**.

3.  Accept the default network site and click **Next**.

4.  Choose a starting and ending IP address for your range.
    >[!IMPORTANT] Start your range on the fourth addresses of your available subnet. For example, if your available subnet is from .1 to .254, start your range at .4.  

5.  In the **IP addresses reserved for load balancer VIPs** box, type the IP addresses range in the subnet. This should match the range you used for starting and ending IP addresses.

6. You do not need to provide gateway, DNS or WINS information as this pool is used to allocate IP addresses for VIPs only via the network controller, so click **Next** to skip these screens.

7.  Review the summary information and complete the wizard.

##### To create an IP pool for Public VIP logical network

1.  Right-click the Public VIP logical network in VMM and select **Create IP Pool** from the drop down menu.

2.  Provide a name and optional description for the IP Pool and ensure that the VIP network is selected for the logical network. Click **Next**.

3.  Accept the default network site and click **Next**.

4.  Choose a starting and ending IP address for your range.
    >[!IMPORTANT] Start your range on the fourth addresses of your available subnet. For example, if your available subnet is from .1 to .254, start your range at .4.

5.  In the **IP addresses reserved for load balancer VIPs** box, type the IP addresses range in the subnet. This should match the range you used for starting and ending IP addresses.

6.  You do not need to provide gateway, DNS or WINS information as this pool is used to allocate IP addresses for VIPs only via the network controller, so click **Next** to skip these screens.

7.  Review the summary information and complete the wizard

## Validation

After you deploy the SLB/MUX, you can validate the deployment by configuring BGP peering between the SLB/MUX instance and a BGP router, assigning a public IP address to a tenant virtual machine or Service, and accessing the tenant virtual machine\service from outside the network.

### Configure BGP Peering between the SLB MUX instance and a router


To publish the VIP network and addresses to networks outside of your private cloud, you need to configure BGP peering between the SLB/MUX and your external router

Enter your external router details in the wizard similar to what is shown below:

![VMM NC Properties BGPImage/VMM-NC-Properties-BGP.png)

Click **OK** to complete the SLB/MUX service instance configuration.

Check the **Jobs** window to verify that the Update Fabric Role with required configuration and Associate service instance with fabric role jobs have completed successfully.

To complete the BGP peering operation you need to configure BGP to peer with your SLB/MUX instance on the router. If you use a hardware router, you need to consult your vendor’s documentation regarding how to setup BGP peering for that device. You also need to know the IP address of the SLB/MUX instance that you deployed earlier. To do this, you can either log on to the SLB MUX virtual machine and run ``ipconfig /all`` from the command prompt, or you can get the IP address from the VMM console.

After peering is completed for the SLB/MUX, you need to advertise all the VIP address pools that will be used by the SLB/MUX to the SLB Manager role using Windows PowerShell cmdlets. This also applies for the Public VIP address pool you may create later to configure an IPSec connection type after you deployed and on-boarded a gateway.

### Windows PowerShell for advertising VIP address pools to the SLB Manager                          
The following is a sample Windows PowerShell script that advertises your Private and Public VIP address pools to the SLBM. Substitute your own parameters from your datacenter.

    # Private VIP Logical Network
    $ipPool1 = Get-SCStaticIPAddressPool -Name "Private VIP Logical Network"
    $ipPool2 = Get-SCStaticIPAddressPool -Name "Public VIP Logical Network "
 
    # Get Fabric role 'config', the GUID used is associated with SLB Manager role
    $networkService = Get-SCNetworkService -Name "TP5_NC"
    $fabricRole = Get-SCFabricRole -Type LoadBalancer -NetworkService $networkService      

    $natIPExemptions = @()                                                                 
    
    $fabricRoleConfiguration = New-SCLoadBalancerRoleConfiguration -LBManagerIPAddress 
    "20.20.20.254" -NatIPExemptions $natIPExemptions -VipPools @($ipPool1, $ipPool2)  
 
    # Setting the configuration.                                                           
    $fabricRole = Set-SCFabricRole -FabricRole $fabricRole -LoadBalancerConfiguration 
    $fabricRoleConFiguration

### Provisioning VIPs for tenant virtual machines

You can provision VIPs for tenant virtual machines either individually for each virtual machine or via service templates.

Provisioning a VIP for a individual virtual machines is not a typical scenario, but for evaluation purposes it may be the easiest way to demonstrate this functionality. You will provision a VIP for two virtual machines using PowerShell.

##### To provision VIPs for virtual machines

To provision a VIP for two virtual machines that were deployed using a VM template, you need to: 
1. Deploy the virtual machine instances using a VM template. 
2. Create a VIP template in the VMM Console. 
3. Create a VIP and assign it to the virtual machines using PowerShell.

##### Create a VIP Template

Use the following procedure to create a VIP template.

1.  Navigate to the **Fabric Workspace** in the VMM console.

2.  Right click the **VIP Templates** node and select **Create VIP Template**, or alternately you can click the **Create VIP Template** in the ribbon toolbar.

3.  Type a name in the **Template Name** field and an optional description in the **Description** field.

4.  In the **Virtual IP Port** field, provide a value for the port you wish to test.

5.  For the **Backend Port**, provide a value for the port from which you wish to map traffic on the back end.

6.  Click **Next**.

7.  On the **Specify a Template Type** screen, click **Specific**, and select **Microsoft** for the **Manufacturer** and for the **Model**, select **Microsoft network controller**. Click **Next**.

8.  On the **Specify Protocol Options** screen, select the protocol you want to create a VIP mapping for. The HTTP and HTTPS options are commonly used, but for a simple example you can select the **Custom** option and chose **TCP** in the **Protocol Name** field. If TCP does not appear as an option in the drop-down menu, you can type it manually. This is a known issue in Technical Preview 5. Click **Next**.

9.  You can optionally select **enable persistence** if you wish to have the load balancer make the connection from the client “sticky”. Click **Next**.

10.  For the **Load Balancing method**, select **Round Robin** from the drop down list. Click **Next**.

11. **Health Monitors** are not implemented in Technical Preview 5, so click **Next** to move past this screen.

12. Confirm your settings and then click **Finish** when you are ready to create the VIP Template.

##### Create the VIP using PowerShell

The following sample PowerShell script creates a VIP for two virtual machines. In the script parameters section, substitute the actual values that match your test environment for the samples used in this script. The script should be run on the VMM server, or on a computer running the VMM Console.   

                                       
    param(

    [Parameter(Mandatory=$false)]
    # Name of the Network Controller Network Service
    # This value should be the name you gave the Network Controller service
    # when you on-boarded the Network Controller to VMM
    $LBServiceName = "NC",

    [Parameter(Mandatory=$false)]
    # Name of the VM instances to which you want to assign the VIP
    $VipMemberVMNames =  @("WGB-001","WGB-002"),

    [Parameter(Mandatory=$false)]
    # VIP address you want to assign from the VIP pool.
    # Pick any VIP that falls within your VIP IP Pool range.
    $VipAddress = "20.20.20.253",

    [Parameter(Mandatory=$false)]
    # Name of the VIP VM Network
    $VipNetworkName = "vip",

    [Parameter(Mandatory=$false)]
    # The name of the VIP template you created via the VMM Console.
    $VipTemplateName = "ADVWRKS-VIP",

    [Parameter(Mandatory=$false)]
    # Arbitrary but good to match the VIP you're using.
    $VipName = "scvmm_20_20_20_253_5001"

    )

    Import-Module virtualmachinemanager

    $lb = Get-scLoadBalancer | where { $_.Service.Name -like $LBServiceName};
    $vipNetwork = get-scvmnetwork -Name $VipNetworkName;

    $vipMemberNics = @();
    foreach ($vmName in $VipMemberVMNames)
    {
    $vm = get-scvirtualmachine -Name $vmName;
    #    if ($vm.VirtualNetworkAdapters[0].VMNetwork.ID -ne $vipNetwork.ID)
    #    {
    #        $vm.VirtualNetworkAdapters[0] | set-scvirtualnetworkadapter -VMNetwork $vipNetwork;
    #    }

    $vipMemberNics += $vm.VirtualNetworkAdapters[0];
    }

    $existingVip = get-scloadbalancervip -Name $VipName
    if ($existingVip -ne $null)
    {
    #    foreach ($mem in $existingVip.VipMembers)
    #    {
    #        $mem | remove-scloadbalancervipmember;
    #    }

    $existingVip | remove-scloadbalancervip;
    }

    $vipt = get-scloadbalancerviptemplate -Name $VipTemplateName;

    $vip = New-SCLoadBalancerVIP -Name $VipName -LoadBalancer $lb
    -IPAddress $VipAddress -LoadBalancerVIPTemplate $vipt
    -FrontEndVMNetwork $vipNetwork
    -BackEndVirtualNetworkAdapters $vipMemberNics;
    Write-Output "Created VIP " $vip;

    $vip = get-scloadbalancervip -Name $VipName;
    Write-Output "VIP with members " $vip;


### Configuring inbound and outbound NAT rules
To complete the BGP peering process, you need to configure a BGP to peer with your SLB/MUX instance on the router. If you use a hardware router, you need to consult your vendor’s documentation for instructions to setup BGP peering for that device. You also need to know the IP address of the SLB/MUX instance that you deployed earlier. To do this, you can log on to the SLB/MUX virtual machine and run ipconfig.

After you deploy and on-board the Software Load Balancer as a Network Service using VMM, you can use the VMM user interface to configure both inbound and outbound NAT rules.

Use the following steps to configure NAT:

1.  Open the VMM Administrator console and select the **VMs and Services** tab.
2.  Select the **VM Networks** tab and then double click the VM network you want to configure with NAT rules.
3.  Select the **Connectivity** tab on the property wizard.
4.  Check **Connect directly to an additional Network** and select **Network Address Translation (NAT)**.
5.  In **Gateway Device**, type your network controller service name. 
6.  Select the **Network Address Translation** tab.
7.  In the **IP address pool** field, choose your Public VIP pool.
8.  Leave the IP address field empty. A VIP address will be automatically assigned to this rule. This is a Technical Preview limitation.
9.  In **NAT rules** click **Add** and type the following values:
    1.  The name of the NAT rule.
    2.  The protocol to use.
    3.  The value for the incoming port.
    4.  Type the destination IP address for this NAT rule.
    5.  Type the destination port.

    ![VMM NATImage/VMM-NAT.png)
10. Click **OK**.

The existing NAT connections will not be visible when you close the network connectivity wizard and re-open it. You can, however, still add additional NAT connections through the user interface.
> 
>To see the existing NAT connections, you can use the following PowerShell cmdlet:
``Get-SCNATConnection``
    


