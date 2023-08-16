---
ms.assetid: 
title: Create a static IP
description: This article describes how to create a static IP for load balancer in a dedicated subnet of SCOM Managed Instance.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 08/16/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Create a static IP

This article describes how to create a static IP for load balancer in a dedicated subnet of SCOM Managed Instance. Additionally, insert an entry into the DNS server, ensure that it resolves to one of the gMSA principal names.

## Create a static IP and configure the DNS name

For all the System Center Operations Manager components to communicate with the load balancer that the SCOM Managed Instance (preview) service creates, you need a static IP and DNS name for the load balancer's front-end configuration.

Ensure that the static IP is in the subnet that you created during virtual network creation. Create a DNS name (according to your organization's policy) for the static IP.

:::image type="DNS manager" source="media/create-static-ip/dns-manager.png" alt-text="Screenshot of host information in DNS Manager.":::

>[!Important]
>To minimize the need for extensive communication with both your Active Directory admin and Network Admin, review  [**Self-verification**](/system-center/scom/scom-mi-self-verification-of-steps?view=sc-om-2022). The outlines the procedures through which the AD admin and network admin validate their configuration changes and ensure their successful implementation; thus, reducing unnecessary back-and-forth interactions with Operations Manager admin time.

## Next steps

- [Configure the network firewall](configure-network-firewall.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
