---
title: How to add a Windows Server Gateway in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 26b83ffb-bb6a-4153-915c-5730fd122a2a
---
# How to add a Windows Server Gateway in VMM
In Virtual Machine Manager \(VMM\) in System Center 2016 Technical Preview, you can connect a VM network to other networks by using a gateway.

> [!IMPORTANT]
> This topic is for Windows Server Gateways only. For information about non\-Windows gateways, see [How to add a non-Windows gateway in VMM](How-to-add-a-non-Windows-gateway-in-VMM.md).

## <a name="BKMK_gateway"></a>Gateway configuration and options
A gateway running Windows Server Technical Preview is also called a Windows Server Gateway. The configuration uses a host cluster that runs Windows Server Technical Preview, and the gateway itself is virtual\-machine based. The gateway consists of a pair of virtual machines that work with the host cluster to help provide high availability and good performance for the gateway. For information about the hardware requirements for a Windows Server Gateway, see[Windows Server Gateway Hardware and Configuration Requirements](http://technet.microsoft.com/library/dn423897.aspx).

You can configure the gateway in a variety of ways, as described in the second half of [Windows Server Gateway](http://technet.microsoft.com/library/dn313101.aspx). One of the main choices that you make when configuring a Windows Server Gateway is whether to make it a forwarding gateway:

-   A gateway configured without forwarding provides communication between a network that uses network virtualization and another network. After you add the gateway, when you configure a VM network to use the gateway, you can choose among multiple connectivity settings for the VM network. You can choose the setting for a connection through a virtual private network \(VPN\) tunnel, with or without Border Gateway Protocol \(BGP\), or the setting for connecting directly to an additional logical network with network address translation \(NAT\). For descriptions and diagrams of these connectivity options for a gateway, see:

    -   [Windows Server Gateway as a site-to-site VPN gateway for hybrid cloud environments](http://technet.microsoft.com/library/dn313101.aspx#bkmk_hybrid) in the Windows Server Gateway topic

    -   [Multitenant Network Address Translation (NAT) for VM Internet access](http://technet.microsoft.com/library/dn313101.aspx#bkmk_nat) in the Windows Server Gateway topic

    -   [Multitenant remote access VPN connections](http://technet.microsoft.com/library/dn313101.aspx#bkmk_vpn) in the Windows Server gateway topic

-   A forwarding gateway can bridge a single virtualized IP address space with a physical IP address space by using direct routing. To create a forwarding gateway, ensure that the connection string for the gateway includes **DirectRoutingMode\=True**, as described in the procedure that follows. For a description and diagram of a forwarding gateway, see [Windows Server Gateway as a forwarding gateway for private cloud environments](http://technet.microsoft.com/library/dn313101.aspx#bkmk_private).

    > [!IMPORTANT]
    > After you add a gateway configured with **DirectRoutingMode\=True**, when you configure a VM network to use the gateway, choose the connectivity setting for connecting directly to an additional logical network, and do not choose the NAT setting.

For more information about the connectivity settings for VM networks, see [Prerequisites for gateways in VMM](Prerequisites-for-gateways-in-VMM.md).

**Prerequisites for adding a Windows Server gateway**

Before you can add a gateway that runs Windows Server Technical Preview to your configuration in VMM, you must perform the tasks in this section.

**Preparatory task**: Download the compressed file \(with a .zip extension\) for the Windows Server Gateway from the [Microsoft Download Center](http://download.microsoft.com/download/0/D/1/0D189100-07B7-4CBF-B774-7A3F43960145/Windows%20Server%202012%20R2%20HA%20Gateway.zip). Extract the files contained within the download. These files include a Quick Start Guide, two service templates, and a custom resource folder \(a folder with a .cr extension\) that contains files required for the service templates. You will choose one of the two service templates for your gateway. The template with 2NIC in the filename is designed for a host cluster configured with two network adapters, and the template with 3NIC in the filename is designed for a host cluster configured with three network adapters.

Review the Quick Start Guide, especially the network requirements and the gateway architecture diagram near the beginning of the guide. However, do not try to import a service template into VMM yet. Instead, proceed with the following tasks, which are also described in the Quick Start Guide.

1.  Review your domain structure, and choose the domain location that you will use for the host cluster. This domain will also be the domain for the gateway virtual machines that run on the host cluster. If the gateway will be facing untrusted networks, such as the public Internet, we recommend that you place the host cluster and the VMM server in two different domains that do not have a trust relationship.

2.  Ensure that the logical networks \(and the associated network sites\) that will be connected to the gateway have been configured in VMM. If you want to configure network settings on the host cluster by using a port profile and logical switch, also create those now.

    > [!IMPORTANT]
    > Review both the list and the table that follow before creating the logical networks.

    The following list outlines the actions that are required for all three of the logical networks:

    -   Create at least one network site on each of the logical networks.

    -   The network virtualization logical network should be created as a connected network.

    -   Configure IP address pools on each of the logical networks, unless you want to use DHCP on the "Infrastructure" \(management\) network—if so, omit the IP address pool for that network.

    The following table outlines the logical networks and the specific requirements for each logical network:

    |Example name|Logical network description|Settings|
    |----------------|-------------------------------|------------|
    |Network Virtualization|The back end network. This is the logical network on which VM networks using network virtualization will be created. On this network, encapsulated packets will be sent to and received from the tenant virtual machines.  This network must be used for network virtualization only.|**One connected network**<br />**Allow new VM networks created on this logical network to use network virtualization**|
    |External|The front end network. This is the network through which your virtual networks can access outside networks.<br /><br />If you will use your gateway for site\-to\-site VPN, this network must have an Internet\-routable IP address space.|**One connected network**<br />**Create a VM network with the same name to allow virtual machines to access this logical network directly**|
    |Infrastructure|The management network. This is the network that connects the VMM server with the host cluster and the gateway \(virtual machines\). There must be a domain controller and a DNS server available on this network. You can configure a static IP address pool for this network, or use a DHCP server to provide IP addresses.|**One connected network**<br />**Create a VM network with the same name to allow virtual machines to access this logical network directly**|

    After you have finished creating the logical networks, network sites, and IP address pools, review the following:

    -   If you added an IP address pool on the "Infrastructure" \(management\) network, determine whether the "Infrastructure" network and the “External” \(front end\) network route to the same network at any point. If they do,  for each IP address pool, right\-click the pool and then click **Properties**. On the **Gateway** tab, review the value in the **Metric** column. Ensure that the **Metric** for the "Infrastructure" network is set to a higher value than the **Metric** for the “External” network.

    -   If you added an IP address pool on the "Infrastructure" \(management\) network, right\-click the pool and then click **Properties**. On the **IP address range** tab, under **IP addresses to be reserved for other uses**, specify an IP address that is within the range of addresses in the IP address pool. Record this IP address. You will use it later when you deploy the gateway.

    -   If you want to use a logical switch on the host cluster, in that logical switch, create or select uplink port profiles that include the network sites in the three logical networks that you created.

        For information about logical switches \(specifically, the **Uplinks** page of the logical switch wizard\), see [How to create a logical switch in VMM](How-to-create-a-logical-switch-in-VMM.md).

3.  Ensure that your VMM resources include a Scale\-Out File Server. Also ensure that the Scale\-Out File Server contains a share.

    -   For background information about a Scale\-Out File Server, see [Scale-Out File Server for Application Data Overview](http://technet.microsoft.com/library/hh831349.aspx).

    -   If you already have a Scale\-Out File Server in your datacenter, ensure that it has been added to VMM. For more information, see [How to add an existing Scale-Out File Server to storage in VMM](How-to-add-an-existing-Scale-Out-File-Server-to-storage-in-VMM.md).

    -   For information about using Windows Server Technical Preview to deploy a Scale\-Out File Server, see [Deploy Scale-Out File Server](http://technet.microsoft.com/library/hh831359.aspx). For information about adding the Scale\-Out File Server to VMM, see [How to add an existing Scale-Out File Server to storage in VMM](How-to-add-an-existing-Scale-Out-File-Server-to-storage-in-VMM.md).

    -   For information about using VMM to deploy a Scale\-Out File Server, see  [Deploying Hyper-V hosts or host clusters from bare metal with VMM](Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md).

    > [!IMPORTANT]
    > To confirm that the Scale\-Out File Server has been added to VMM and the share is being managed in VMM, open the **Fabric** workspace, expand **Storage**, and then click **File Servers**. In the list, find the file server, and confirm that the **Type** is **Scale\-Out File Server** and the **Status** is **OK**. Expand the listing for the Scale\-Out File Server, right\-click the share, and then click **Properties**. Ensure that the **File share managed by Virtual Machine Manager** check box is selected.

4.  Create three virtual hard disks that will be used in your configuration:

    -   Create a virtual hard disk containing the Windows Server Technical Preview operating system. Ensure that the virtual hard disk has been generalized by using the Sysprep tool. The virtual hard disk can use the .vhd or .vhdx format. Copy the virtual hard disk into the VMM library, in the subfolder where you store virtual machine hard disk files. For more information, see[How to Add File-Based Resources to the VMM Library](https://technet.microsoft.com/library/gg610607.aspx).

    -   Make two copies of the small blank .vhdx files that are included in the VMM library. Provide them with names that help identify them as the virtual hard disk files for a Cluster Shared Volume \(CSV\) and a quorum resource. In the VMM library, create a folder named **Windows Server Gateway**, and then copy the two blank .vhdx files into that folder.

5.  Navigate to the resources that you downloaded, and locate the folder called **VMClusterSetup.cr**. The .cr filename extension is a standard extension in VMM that indicates a custom resource folder. Copy the entire folder and its contents into the **Windows Server Gateway** folder that you just created. Confirm that the **VMClusterSetup.cr** folder is a subfolder in the **Windows Server Gateway** folder.

    To confirm that the virtual hard disks and the custom resource folder for the gateway are in the VMM library, in VMM, open the **Library** workspace, right\-click the library server or library share, click **Refresh**, and then review the items in the list.

6.  Collect the following information:

    -   The fully\-qualified domain name \(FQDN\) of the domain that you chose in prerequisite 1. This is the domain that the host cluster and the virtual machines that comprise the gateway will join.

    -   The name that you will give to the host cluster.

    -   The name of the host groups for which the gateway should be available.

    -   The name of the shared folder on the Scale\-Out File Server that you will use with the gateway.

    -   The name of a domain account that has permissions to add computers to the domain in the first item in this list. Also, from this domain account, create a Run As account in VMM, and record the name of the Run As account. For more information, see [How to create a Run As account in VMM](How-to-create-a-Run-As-account-in-VMM.md).

        Because this account will be used by VMM to manage the gateway, the service template will add this account to the local **Administrators** group on the virtual machines that together comprise the gateway.

    -   The name of a domain user account. The service template will add this account to the local **Administrators** group on the virtual machines that comprise the gateway, to ensure that administrative access to the virtual machines is always available. Create a Run As account in VMM from this domain account also.

    -   Product keys for the operating system on the virtual machines that comprise the gateway. If you have these product keys, have this information available as you configure the gateway.

        If you do not have product keys and you are creating an evaluation deployment, you must edit your chosen service template to remove the configurable service setting called **@ProductKey@**. Then, at the end of the deployment process, you must connect to the virtual machines that comprise the gateway, and, when prompted, select **Skip** to skip the product key and complete the deployment of the virtual machines.

    -   The name that you will use for the gateway itself \(the virtual machines that comprise the gateway and that run on the host cluster\). Choose a new, valid NetBIOS name containing no more than 15 characters.

    -   The IP address reserved for the gateway, if you added an IP address pool on the "Infrastructure" \(management\) network. This is the address that you specified in the properties of the IP address pool, under **IP addresses to be reserved for other uses**. However, if you are using DHCP for the "Infrastructure" network, make a note to avoid entering a value for this setting, which in the service templates is called **VMClusterStaticIPAddress**.

    -   The name of the virtual switch to be used on the back end connection. However, ensure that you do not specify this information until you reach the last step of the procedure that follows.

#### To use a server running Windows Server Technical Preview as a gateway with VMM


1.  Open the Quick Start Guide that was included in the file that you downloaded in the preparatory step at the beginning of the Prerequisites. Follow instructions in the Quick Start Guide to import the appropriate service template into the VMM library.

 When you import the template, ensure that you configure references to the following items:

- The custom resource folder, called **VMClusterSetup.cr**.
- The virtual hard disk containing the Windows Server Technical Preview operating system.
- The blank virtual hard disk that you added to the library for the CSV that the gateway will use.
- The blank virtual hard disk that you added to the library for the quorum resource that the gateway will use.

Also follow the instructions in the Quick Start Guide that describe how to customize the service template for your environment.

2.  Create a two\-node host cluster that runs Windows Server Technical Preview with the Hyper\-V role, and add it to VMM. As with any cluster, in the network infrastructure that connects the cluster nodes, avoid having single points of failure. Ensure that the host cluster is in an appropriate domain, as described in prerequisite 1. For information about the hardware requirements for the host cluster \(the servers that run Hyper\-V\), see [Windows Server Gateway Hardware and Configuration Requirements](http://technet.microsoft.com/library/dn423897.aspx). When you deploy the host cluster, be sure to run the Validate a Configuration Wizard and confirm that the cluster passes the cluster validation tests.

    -   For more information about using Windows Server Technical Preview to deploy a host cluster, see [Deploy a Hyper-V Cluster](http://technet.microsoft.com/library/jj863389.aspx). Then, for more information about adding the host cluster to VMM, see [How to add existing servers or clusters as Hyper-V hosts or host clusters in VMM](How-to-add-existing-servers-or-clusters-as-Hyper-V-hosts-or-host-clusters-in-VMM.md).

    -   For more information about using VMM to deploy a host cluster, see  [Deploying Hyper-V hosts or host clusters from bare metal with VMM](Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md).

3.  Verify that the host cluster was successfully added by performing the following actions:

    1.  Open the **Fabric** workspace.

    2.  On the **Home** tab, in the **Show** group, ensure that **Fabric Resources** is selected.

    3.  In the **Fabric** pane, click **Servers**.

    4.  Expand the host group where you added the host cluster, click the host cluster, and then in the **Hosts** pane, verify that the host status is **OK**.

4.  Associate the logical networks that you created with the appropriate physical adapters on the nodes in the host cluster. In other words, ensure that the relevant virtual switches on both nodes of the new host cluster have been configured so that the switches specify the correct network sites. You can do this by using the port profile and logical switch that you created as prerequisites, or through direct configuration of the ports in the virtual switches. For more information about configuring these settings on a host cluster, see the following topics:

    -   [How to configure network settings on a Hyper-V host in VMM](How-to-configure-network-settings-on-a-Hyper-V-host-in-VMM.md)

    -   [How to configure network settings on a host by using a logical switch in VMM](How-to-configure-network-settings-on-a-host-by-using-a-logical-switch-in-VMM.md)

5.  Add a file share from the Scale\-Out File Server to the host cluster. To add the file share, on the properties sheet for the host cluster, click the **File Share Storage** tab, and then click **Add**. Select the appropriate file share. If the file share does not appear, review prerequisite 2 in the list of prerequisites.

    After you close the properties sheet and the job completes, open the host cluster properties again, click the **File Share Storage** tab, and confirm that the share is listed with a check mark under **Access Status**.

6.  Configure the hosts as dedicated network virtualization gateways. To do this, perform the following steps:

    1.  In the **Hosts** pane, right\-click one of the hosts \(not the host cluster\), and then click **Properties**.

    2.  Click the **Host Access** tab and then select the check box labeled **This host is a dedicated network virtualization gateway, as a result it is not available for placement of virtual machines requiring network virtualization**. Then click **OK**.

    3.  Repeat the process on the other host.

7.  On the host cluster, deploy the service. To do this, follow the instructions in the Quick Start Guide that was included in the download. The result will be a pair of virtual machines that use a guest cluster internally for high availability, although they do not use the property in VMM called **Make this virtual machine highly available**. However, the pair of virtual machines together, when deployed on a host cluster, constitute a highly available gateway. The gateway runs Windows Server Technical Preview and is configured with multiple virtual network adapters and with the necessary role, role services, and features.

8.  Perform the following verification tasks to ensure that the service deployment was successful:

    -   Confirm that the backend virtual network adapter on the gateway is not connected \(it should not be connected yet\). In VMM, in the **VMs and Services** workspace, on the **Home** tab, in the **Show** group, click **Services**. Expand **All Hosts** and then click the host group that the host cluster is in. In the **Services** pane, expand the service until you can see the gateway virtual machines, right\-click a gateway virtual machine, click **Properties**, and then in the properties sheet, click the **Hardware Configuration** tab. Under **Network Adapters**, confirm that there are three network adapters, and that one of them is labeled **Not connected**.

    -   Start the new service and confirm that the virtual machines enter the **Running** state.

    -   With the virtual machines running, on the VMM server, open a command prompt as an administrator, and then type **ping** followed by the name or IP address of the gateway itself. Press Enter and confirm that a response is received from the gateway. If a response is not received, review possible causes, such as DNS settings, firewall settings, and the state of the gateway cluster.

    > [!IMPORTANT]
    > -   On the virtual machines that constitute a gateway, avoid directly specifying VLAN information for the virtual network adapters. The provider software requires this information to be supplied through network sites configured in VMM.
    > -   On the virtual machines that constitute a gateway, if you must disable any integration services \(which are all enabled by default\), be sure that you do not disable the integration service called **Data Exchange**, which is a required service.

9. Open the **Fabric** workspace.

10. On the **Home** tab, in the **Show** group, ensure that **Fabric Resources** is selected.

11. In the **Fabric** pane, expand **Networking**, and then click **Network Service**.

    Network services include gateways, virtual switch extensions, network managers, and top\-of\-rack \(TOR\) switches.

12. On the **Home** tab, in the **Add** group, click **Add Resources**, and then click **Network Service**.

    The Add Network Service Wizard opens.

13. On the **Name** page, enter a name and optional description for the gateway, and then click **Next**.

14. On the **Manufacturer and Model** page, in the **Manufacturer** list, select **Microsoft**, and in the **Model** list, select **Microsoft Windows Server Gateway**. Then click **Next**.

15. On the **Credentials** page, specify the domain account that has permissions to add computers to the domain. This is the account that you specified for **DomainUserRAA** in the service template. To specify this account, click **Browse** and then on the **Select a Run As Account** dialog box, select the account. Then click **Next**.

16. On the **Connection String** page, in the **Connection string** box, type the connection string for the gateway to use, and then click **Next**. For a gateway running Windows Server Technical Preview, include the following items in the connection string, separated by semicolons \(;\).

    -   **VMHost\=** followed by the name of the host cluster.

    -   **GatewayVM\=** followed by the name of the virtual machine.

    -   **BackendSwitch\=** followed by the name of the virtual switch used on the back end connection. When you specify this, you complete the network connections in the correct way, which is to use the connection string to connect the third virtual network adapter to the correct virtual switch.

    You can also include one or more of the following items in the connection string, separated by semicolons:

    -   **DirectRoutingMode\=True** as the option that specifies a forwarding gateway \(optional\). If you include this option, configure only one VM network to use the gateway. When you configure that VM network, choose the connectivity setting for connecting directly to an additional logical network, and do not choose the NAT setting. Using other connectivity settings will not work with a forwarding gateway.

        If you include **DirectRoutingMode\=True**, you must also include the following parameter:

        -   **FrontEndServerAddress\=** followed by the IP address of this routing gateway on the external network. Network routing devices on the external network should point to this endpoint to get access to the VM network behind the gateway.

    -   **VPNServerAddress\=** followed by the IP address of this VPN endpoint to report to tenants.  This is only required if this gateway is behind an external load balancer.

    -   **MaxVMNetworksSupported\=** followed by the number of VM networks that can be used with this gateway.  If **DirectRoutingMode** is not specified or is not set to **True**, the default value is 50, and the maximum value is 100. If **DirectRoutingMode** is set to **True**, the default value is 1, and it cannot be set any higher.

    For example, you might enter the following connection string. Note that this is a connection string for a gateway that does not use forwarding:

    **VMHost\=GatewayHost1.contoso.com;GatewayVM\=GatewayVM1.contoso.com;BackendSwitch\=VirtualSwitch1**

17. On the **Certificates** page, click **Next**.

18. On the **Provider** page, in the **Configuration provider** list, ensure that **Microsoft Windows Server Gateway Provider** is selected, and then click **Test** to use the selected provider to run basic validation tests against the gateway. If tests indicate that the provider works correctly for the gateway, click **Next**.

    Results that say **Passed** or **Failed** indicate whether the provider works as expected. One possible cause of failure is insufficient permissions in the Run As account. Results that say **Implemented** and **Not implemented** are informational only, and indicate whether the provider supports a particular API.

19. On the **Host Group** page, select one or more host groups to which the gateway will be available. Ensure that you include the host groups that are associated with the network sites that you plan to connect to the gateway.

20. On the **Summary** page, review and confirm the settings, and then click **Finish**.

21. After the gateway is created, under **Network Services**, find the listing for the gateway. Right\-click the listing, click **Properties**, click **Connectivity**, and then specify the following:

    -   Select the **Enable front end connection** check box, and then select the virtual network adapter and the network site that provides connectivity outside the hosting\-provider or enterprise datacenter. If you will allow VPN connections, the network site needs to be routable to and from the Internet. Also, the network site must have a static IP address pool.

    -   Select the **Enable back end connection** check box, and then select the **BackEnd** virtual network adapter and a network site in a logical network within the hosting\-provider or enterprise datacenter. The logical network must have Hyper\-V network virtualization enabled. Also, the network site must have a static IP address pool.

    > [!NOTE]
    > If you do not see the network sites that you expect, ensure that the network settings of the host cluster have been configured as intended. Also, in the gateway properties, on the **Host Group** tab, confirm that you have added all the host groups that are associated with the network sites that you want to select.

A variety of network diagnostic tools are available for reviewing the state of the gateway. For information about tools such as the Windows PowerShell cmdlet [Test-VMNetworkAdapter](http://technet.microsoft.com/library/dn464286.aspx), see[New Networking Diagnostics with PowerShell in Windows Server 2012 R2](http://blogs.technet.com/b/networking/archive/2013/07/31/new-networking-diagnostics-with-powershell-in-windows-server-r2.aspx).

When you are ready to configure the VM network that uses the newly added gateway, first obtain IP address and authentication details provided by your tenant, customer, or client, as described in [Prerequisites for gateways in VMM](Prerequisites-for-gateways-in-VMM.md). Specify those settings in the wizard or property sheet for the VM network. Also, in the same wizard or property sheet, on the **Connectivity** page or tab, choose the appropriate setting for the connectivity of the gateway. The settings are described in the bulleted list under [Gateway configuration and options](How-to-add-a-Windows-Server-Gateway-in-VMM.md#BKMK_gateway) earlier in this topic.

## See Also
[Configuring gateways in VMM](Configuring-gateways-in-VMM.md)
[Windows Server Gateway](http://technet.microsoft.com/library/dn313101.aspx)
[Windows Server Gateway Hardware and Configuration Requirements](http://technet.microsoft.com/library/dn423897.aspx)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)
[How to create a VM network for a VLAN in VMM](How-to-create-a-VM-network-for-a-VLAN-in-VMM.md)


