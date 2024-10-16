---
ms.assetid: b75145ed-5980-4952-866e-41c617938f66
title: Add a network virtualization gateway to the VMM fabric
description: This article provides information about adding a gateway to the VMM fabric
ms.custom: engagement-fy23, UpdateFrequency2
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 08/21/2024
ms.topic: article
ms.service: system-center
ms.subservice: virtual-machine-manager
---

# Add a network virtualization gateway to the VMM fabric



Read this article to learn about setting up network virtualization gateways in the System Center Virtual Machine Manager (VMM) networking fabric.

By default, if you're using isolated VM networks in your VMM fabric, VMs associated with a network can only connect to machines in the same subnet. If you want to connect VMs further than the subnet, you'll need a gateway.

## Network virtualization

You set up network virtualization so that multiple VM networks are overload on the VMM logical networks that model your physical network topology and thus decouple the VM networks from the physical network infrastructure. Network virtualization uses NVGRE (Network Virtualization using Generic Routing Encapsulation) to virtualize IP addresses. Review the following to learn more about [NVGRE](/windows-hardware/drivers/network/network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload?f=255&MSPPError=-2147217396).

To figure out whether you need a network virtualization gateway in your network, consider:

- Do you need to connect from VMs in isolated VM networks to other on-premises apps?
- Do you need to connect from isolated VMs to the Internet?
- Do you need to connect from isolated VM networks to shared services such as DNS?

You can set up your gateway in many ways depending on your requirements:

- Connectivity to a public network can be achieved through NAT.
- Connectivity to an on-premises network is over a VPN tunnel (with or without Border Gateway Protocol (BGP))
- Direct routing without NAT can be used for connectivity between different VM networks.


## Prerequisites

- **Provider software**: If you want to use a non-Windows gateway device, you'll need the provider and an account with permissions to configure the gateway. You install the provider on the VMM server. If certificates are required (for example, if the gateway is in an untrusted domain), you'll need to be able to view thumbprint information for those certificates.

::: moniker range="sc-vmm-2016"
- **Windows Server gateway**: If you want to configure a gateway running Windows Server, you can use a predefined template available from the Microsoft Download Center. The template supports System Center 2012 R2 or later versions.
::: moniker-end
::: moniker range=">sc-vmm-2016"
- **Windows Server gateway**: If you want to configure a gateway running Windows Server, you can use a predefined template available from the Microsoft Download Center.
::: moniker-end
- **Logical networks**: You need logical networks (you'll need more than one if you want the gateway to connect from VM networks in one logical network to VM networks in another).
- **Remote VPN settings**: If you want to connect the gateway to a remote VPN server, you'll need:
    - The remote server IP address and information about on-premises subnets or the BGP address, if relevant.
    - You'll need to identify how you'll authenticate with the remote VPN server. If it uses a preshared key, you can authenticate with a Run As account and specify the shared key as the password. Or you can authenticate with a certificate. The certificate can be either a certificate that the remote VPN server selects automatically or a certificate that you've obtained and placed on your network.
    - Check whether you need specific VPN connection settings (encryption, integrity checks, cipher transforms, authentication transforms, Perfect Forward Secrecy (PFS) group, Diffie-Hellman group, and VPN protocol) or you can use the default settings.

## Add a Windows Server Gateway

The service template provides a highly available Windows Server Gateway deployment in active-standby mode.

1. You'll need to download the template from the [Download Center](https://download.microsoft.com/download/0/D/1/0D189100-07B7-4CBF-B774-7A3F43960145/Windows%20Server%202012%20R2%20HA%20Gateway.zip).

::: moniker range="sc-vmm-2016"
> [!NOTE]
> The templates downloaded are applicable for VMM 2012 R2, and 2016.
::: moniker-end

2. The download is a compressed zip file. You'll need to extract the file. Files include a user guide, two service templates, and a custom resource folder (a folder with a .cr extension) that contains files required for the service templates.
3. You'll need to decide which template to use, and then follow the instructions in the Quick Start Guide. The guide includes prerequisites for the template deployment, and instructions for setting up logical networks, creating a scale-out file server, preparing virtual hard disks for the gateway VM, and copying the custom resource file to the library. After you've set up the infrastructure, it describes how to import and customize the template and how to deploy it. There's also troubleshooting information if issues arise.


## Add a non-Windows gateway

> [!NOTE]
> You'll need to install the provider software on the VMM management server and add the gateway to the fabric.
> Obtain the provider software. You can review a list of supported providers in **Settings** > **Configuration Providers**.

Use the following procedure to add the non-Windows gateway:

1. Select **Fabric** > **Network Service**. Right-click and select **Add Network Service** to open the Network Service wizard. Network services include gateways, virtual switch extensions, network managers, and top-of-rack (TOR) switches. Or on Home, select  **Add Resources** > **Network Service**.
2. In **Add Network Service Wizard** > **Name**, specify a name and description for the gateway.
3. In **Manufacturer and Model**, select the required settings.
4. In **Credentials**, specify a Run As account with permissions in the domain to which the gateway is connected.
5. In **Connection String**, enter the string that the gateway must use. The string syntax is defined by the gateway vendor.
6. In **Certificates**, if listed, verify the thumbprints of the certificates match those installed on the gateway. Select to confirm that the certificates can be imported. If none is listed, the gateway probably doesn't need certificate authentication. If they're needed, ensure that they're installed correctly on the gateway.
7. In **Gather Information**, select **Scan Provider** to run the basic validation test against the gateway.
8. In **Host Group**, select one or more host groups to which the gateway will be available.
9. In **Summary**, review the settings and select **Finish**.
10. After the gateway is added, find its listing in **Network Services**, and right-click > **Properties** > **Connectivity**.
11. Select **Enable front end connection**, and select the gateway network adapter and network site that provides connectivity outside the enterprise datacenter or hosting provider. Select **Enable back end connection**, and select a gateway network adapter and network site in a logical network within the enterprise. The network must have network virtualization enabled, and the network site must have a static IP address.
12. When you create a VM network, you can assign the gateway to it and select the required connectivity options.
