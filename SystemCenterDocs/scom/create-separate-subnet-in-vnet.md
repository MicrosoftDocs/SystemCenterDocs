---
ms.assetid: 
title: Create a separate subnet in a VNet
description: This article describes how to create a separate subnet in a VNet.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 08/23/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Create a separate subnet in a VNet

This article describes how to create a separate subnet in a VNet for a SCOM Managed Instance and enable NAT gateway on SCOM Managed Instance subnet.

## To create a separate subnet in a VNet

For more information on how to create a VNet, see [Quickstart: Use the Azure portal to create a virtual network](/azure/virtual-network/quick-create-portal).

We need a NAT gateway for outbound internet access from SCOM Managed Instance subnet. Edit the subnet to add a NAT gateway. In Azure, add a NAT gateway to the subnet where the SCOM managed instance will be created. A NAT gateway is needed for outbound internet access from SCOM Managed Instance subnet. For more information, see [What is Virtual Network NAT?](/azure/virtual-network/nat-gateway/nat-overview).

To create a NAT gateway, follow these steps:

1. Create a NAT gateway in the same region where the virtual network is present.
1. Create a NAT gateway in the same subscription that you use for SCOM Managed Instance (preview).
1. Create a public IP.

   :::image type="NAT gateway" source="media/create-separate-subnet-in-vnet/nat-gateway.png" alt-text="Screenshot of public IP information for a NAT gateway.":::

1. Select a virtual network and subnet for SCOM Managed Instance (preview).

## Next steps

- [Create SQL MI](create-sql-mi.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
