---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Prerequisites for gateways in VMM
ms.technology:  virtual-machine-manager
ms.assetid:  678c8589-fd09-49fc-bd1b-2638b5e56297
---

# Prerequisites for gateways in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

If you want to add a gateway to your configuration in Virtual Machine Manager (VMM), you must have provider software for the gateway. If the gateway is a non-Microsoft gateway, you must obtain the provider software from the manufacturer of the gateway device, install the provider on the VMM management server, and then restart the System Center Virtual Machine Manager service. Then you can add the gateway to the list of resources in VMM. For more information about setting up a specific non-Microsoft gateway device, refer to the manufacturer�s documentation.

> [!TIP]
> VMM in System Center 2016 Technical Preview considers  a gateway to be a "network service," and the gateway requires additional configuration steps, as described in [How to add a non-Windows gateway in VMM](How-to-add-a-non-Windows-gateway-in-VMM.md) or [How to add a Windows Server Gateway in VMM](How-to-add-a-Windows-Server-Gateway-in-VMM.md).

After you add a gateway to VMM, to use the gateway to connect a VM network through a VPN tunnel to another site, for the VM network, you must select the **Connectivity** setting called **Connect to another network through a VPN tunnel**. Before you configure this setting for a VM network, gather the necessary information from your tenant, customer, or client. The following list provides more details:

-   Obtain the IP address of the remote VPN server (on the premises of the tenant, customer, or client). Also obtain information about the subnets on the premises of the tenant, customer, or client. These are the subnets that are used by the tenant�s virtual machines or other virtual or physical resources. In addition, if the tenant, customer, or client uses Border Gateway Protocol (BGP), obtain the relevant BGP peer IP addresses and Autonomous System Numbers (ASNs).

-   Identify the authentication method to use with the remote VPN server. If the remote VPN server is configured to use a pre-shared key, you can authenticate by using a **Run As** account in which you specify the pre-shared key as the password. Alternatively, you can authenticate with a certificate. The certificate can be either a certificate that the remote VPN server selects automatically or a certificate that you have obtained and placed on your network.

-   Determine whether to use the default VPN connection settings or to specify these settings. You can specify settings for the encryption, integrity checks, cipher transforms, authentication transforms, Perfect Forward Secrecy (PFS) group, Diffie-Hellman group, and VPN protocol.

The information that you gather helps you complete the gateway configuration for the VM network.

## See Also
[Configuring gateways in VMM](Configuring-gateways-in-VMM.md)
[Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)



