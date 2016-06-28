---
title: How to add a non-Windows gateway in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6fcb27a4-2141-4cd6-856d-173b6490856c
---
# How to add a non-Windows gateway in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

You can connect a VM network to other networks by using a gateway in Virtual Machine Manager (VMM).

> [!IMPORTANT]
> This topic is for non-Windows gateways. For information about Windows Server gateways, see [How to add a Windows Server Gateway in VMM](How-to-add-a-Windows-Server-Gateway-in-VMM.md).

After you add the gateway, you can configure a VM network to use the gateway. You have several choices for the VM network settings. You can choose the setting for a connection through a VPN tunnel, with or without Border Gateway Protocol (BGP), or the setting for connecting directly to an additional logical network, with or without network address translation (NAT).

## Prerequisites
If you want to add a gateway to your configuration in VMM, you must first perform the following tasks:

1.  Obtain provider software from the manufacturer of the gateway device, install the provider on the VMM management server, and then restart the System Center Virtual Machine Manager service. If you have installed a high-availability VMM management server on a cluster, be sure to install the provider on all nodes of the cluster. For more information about installing the provider, refer to the manufacturer’s documentation.

2.  Make sure that you know the manufacturer and model of your gateway, the name of an account that has permission to configure the gateway, the connection string that the gateway will use, and the host groups for which the gateway should be available. If certificates are required for the gateway, for example, if the gateway is in an untrusted domain, make sure you know how to view the thumbprint information for those certificates.

3.  As a best practice, in the operating system of the gateway, ensure that network adapters (physical network adapters, virtual network adapters, or both) have adapter names that indicate their intended use. For example, if your adapters have the default names Ethernet, Ethernet 2, and Ethernet 3, a best practice would be to rename them for their intended uses, such as Management, External, and Tenant. This makes them easy to recognize when you see them in a list in VMM.

4.  Ensure that the logical networks (and the associated network sites) that will be connected to the gateway have been configured. The VM networks that will use the gateway must be based on logical networks that use network virtualization and IP address pools.

    > [!NOTE]
    > Configure the IP address pools even if you use NAT. IP addresses used by NAT are allocated through the IP address pools.

5.  Ensure that the relevant virtual switches on the affected hosts have been configured, either through port profiles and logical switches, or through direct configuration of the ports and capabilities in the virtual switch.

6.  Obtain information from your tenant, customer, or client as described in [Prerequisites for gateways in VMM](Prerequisites-for-gateways-in-VMM.md).

#### To add a gateway in VMM

1.  Confirm that the necessary provider software for the gateway device has been installed. To do this, open the **Settings** workspace, and in the **Settings** pane, click **Configuration Providers**. In the **Configuration Providers** pane, review the list of installed provider software.

2.  Open the **Fabric** workspace.

3.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

4.  In the **Fabric** pane, expand **Networking**, and then click **Network Service**.

    Network services include gateways, virtual switch extensions, network managers, and top-of-rack (TOR) switches.

5.  On the **Home** tab, in the **Add** group, click **Add Resources**, and then click **Network Service**.

    The **Add Network Service Wizard** opens.

6.  On the **Name** page, type a name and an optional description for the gateway, and then click **Next**.

7.  On the **Manufacturer and Model** page, in the **Manufacturer** list, click a provider manufacturer, and in the **Model** list, click a model. Then click **Next**.

8.  On the **Credentials** page, either click **Browse** and then on the **Select a Run As Account** dialog box, select an account, or click **Create Run As Account** and create a new account. The account must have appropriate permissions in the domain that the gateway is connected to. After you have selected or created an account, click **Next**.

9. On the **Connection String** page, in the **Connection string** box, type the connection string for the gateway to use, and then click **Next**.

    > [!IMPORTANT]
    > The syntax of the connection string is defined by the manufacturer of the gateway. For more information about the required syntax, refer to the manufacturer’s documentation.

10. On the **Certificates** page, if certificates are listed, verify that the thumbprints of those certificates match the thumbprints of the certificates that are installed on the gateway. Then select the check box to confirm that the certificates can be imported to the trusted certificate store. Click **Next**.

    > [!NOTE]
    > If no certificates are listed, the connection string that was provided probably does not require certificates, and you can continue to the next page of the wizard. However, if no certificates are listed but your gateway requires them, confirm that the certificates were installed correctly on your gateway. Then, to refresh the display on the **Certificates** page of the wizard, click **Previous** and then click **Next**.

11. On the **Provider** page, in the **Configuration provider** list, select an available provider, and then click **Test** to use the selected provider to run basic validation tests against the gateway. If the tests indicate that the provider works correctly for the gateway, click **Next**.

12. On the **Host Group** page, select one or more host groups to which the gateway will be available.

13. On the **Summary** page, review and confirm the settings, and then click **Finish**.

14. After the gateway is created, under **Network Services**, find the listing for the gateway. Right-click the listing, click **Properties**, click **Connectivity**, and then specify the following:

    -   Select **Enable front end connection**, and then select the gateway network adapter and the network site that provide connectivity outside the hosting-provider or enterprise datacenter. If you will allow VPN connections, the network site needs to be routable to and from the Internet. Also, the network site must have a static IP address pool.

    -   Select **Enable back end connection**, and then select a gateway network adapter and network site in a logical network within the hosting-provider or enterprise datacenter. The logical network must have Hyper-V network virtualization enabled. Also, the network site must have a static IP address pool.

When you are ready to configure the VM network that uses the newly added gateway, open the wizard or property sheet for the VM network, and on the **Connectivity** page or tab, choose the appropriate setting for the connectivity of the gateway. You can choose the setting for a connection through a VPN tunnel, with or without Border Gateway Protocol (BGP), or the setting for connecting directly to an additional logical network, with or without network address translation (NAT). For more information, see [Prerequisites for gateways in VMM](Prerequisites-for-gateways-in-VMM.md).

## See Also
[Configuring gateways in VMM](Configuring-gateways-in-VMM.md)
[How to create a VM network for a VLAN in VMM](How-to-create-a-VM-network-for-a-VLAN-in-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)



