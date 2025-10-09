---
ms.assetid: 4c078131-cb8b-4c43-b651-182f8060c19f
title: Configure Encrypted Networks in System Center Virtual Machine Manager
description: This article explains about how to configure encrypted networks in SDN using VMM.
ms.date: 08/21/2025
author: Jeronika-MS
ms.author: v-gajeronika
ms.update-cycle: 1095-days
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
monikerRange: '>sc-vmm-2016'
ms.custom:
  - UpdateFrequency3
  - engagement-fy24
  - sfi-image-nochange
---

# Configure encrypted networks in SDN using VMM



This article explains how to encrypt the VM networks in software defined network (SDN) using  System Center Virtual Machine Manager (VMM).

Network traffic can be encrypted by the guest OS or an application using technologies like IPSec and TLS. However, these technologies are difficult to implement because of their inherent complexity and challenges related to interoperability between systems because of the nature of implementation.

Using the encrypted networks feature in VMM, end-to-end encryption can be easily configured on the VM networks by using the Network Controller (NC). This encryption prevents traffic between two VMs on the same VM network and same subnet from being read and manipulated.

The control of encryption is at the subnet level, and encryption can be enabled/disabled for each subnet of the VM network.

This feature is managed through the SDN Network Controller (NC). If you don't already have a Software Defined Network (SDN) infrastructure with an NC, for more information, see [deploy SDN](deploy-sdn.md).

> [!NOTE]
> This feature currently provides protection from non-Microsoft and network admins and doesn’t offer any protection against fabric admins.

## Before you start

Ensure the following prerequisites are met:

- At least two hosts for tenant VMs to validate the encryption.
- HNV-based VM network with encryption enabled and a certificate, which can be created and distributed by fabric administrator. 
    > [!NOTE]
    > The certificate, along with its private key, must be stored in the local certificate store of all the hosts where the VMs (of that network) reside.

## Configure encrypted networks

To configure encrypted networks, follow these steps:

1. Create a certificate and then place the certificate in the local certificate store of all the hosts where you plan to place the tenant VMs for this validation.

2. You can either create a self-signed certificate or get a certificate from a CA. For information on how to generate self-signed certificates and place them in the appropriate locations of each host you'll be using, see [Configure Encryption for a Virtual Subnet](/windows-server/networking/sdn/vnet-encryption/sdn-config-vnet-encryption#step-1-create-the-encryption-certificate).

    > [!NOTE]
    > Make a note of the **Thumbprint** of the certificate that you generate.
    > In the article above in step 2, you don't have to perform the actions detailed in **Creating a Certificate Credential** and **Configuring a Virtual Network for Encryption**. You will configure those settings using VMM in the following steps.

3. Set up an HNV provider network for tenant VM connectivity, which will be managed by the NC. [Learn more](sdn-controller.md#validate-the-deployment).
4. Create a tenant VM Network and a subnet. While creating the subnet, select **Enable Encryption** under **VM Subnets**. [Learn more](sdn-controller.md#validate-the-deployment).

    In the next step, paste the thumbprint of the certificate that you created.

    :::image type="content" source="./media/encrypt-networks/enable-encryption.png" alt-text="Screenshot of network encryption.":::

    :::image type="content" source="./media/encrypt-networks/details-encrypted-network.png" alt-text="Screenshot of encryption details.":::

5.	Create two VMs on two separate physical hosts and connect them to the above subnet. [Learn more](sdn-controller.md#validate-the-deployment).
6.	Attach any packet sniffing application on the two network interfaces of the two hosts where the tenant VMs are placed.
7.	Send traffic, ping, HTTP, or any other packets between the two hosts, and check the packets in the packet sniffing application. The packets must not have any discernible plain text like the parameters of an HTTP request.
