---
ms.assetid: 
title: Register the SCOM Managed Instance (preview) resource provider 
description: This article describes how to register the SCOM Managed Instance (preview) resource provider.
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

# Register the SCOM Managed Instance (preview) resource provider 

This article describes how to register the SCOM Managed Instance (preview) resource provider.

Provide a subscription that has the registration of both SCOM Managed Instance provider and a Compute provider. This enables the SCOM Managed Instance to create a managed resource group, set up a VMSS for Operations Manager Management servers, and implement a load balancer.

:::image type="Tenant" source="media/register-scom-mi-resource-provider/tenant.png" alt-text="Screenshot of tenant.":::

## To register the SCOM Managed Instance (preview) resource provider

To register the SCOM managed Instance (preview) resource provider, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com) and select **Subscriptions**.
2. Select the subscription where you want to deploy SCOM Managed Instance (preview).
3. Under **Settings**, select **Resource providers**.
4. Search for **SCOM** and register **Microsoft.Scom**.
5. On the **Subscription** page, under **Settings**, select **Resource providers** and search for **microsoft.insights**. If the **microsoft.insights** provider isn't registered, select the provider, and then select **Register**.

    :::image type="Microsoft insights resource provider" source="media/register-scom-mi-resource-provider/resource-provider.png" alt-text="Screenshot of the Microsoft insights provider.":::

>[!Important]
>To minimize the need for extensive communication with both your Active Directory admin and Network Admin, review the [**Self-verification**](/system-center/scom/scom-mi-self-verification-of-steps?view=sc-om-2022). This outlines the procedures through which the AD admin and network admin validate their configuration changes and ensure their successful implementation; thus, reducing unnecessary back-and-forth interactions with Operations Manager admin time.

## Next steps

- [Create separate subnet in a VNet](create-separate-subnet-in-vnet.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
