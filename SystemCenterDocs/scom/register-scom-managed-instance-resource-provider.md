---
ms.assetid: 
title: Register the Azure Monitor SCOM Managed Instance (preview) resource provider
description: This article describes how to register the SCOM Managed Instance (preview) resource provider.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 09/06/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Register the Azure Monitor SCOM Managed Instance (preview) resource provider

This article describes how to register the SCOM Managed Instance (preview) resource provider.

>[!Note]
> To know about the SCOM Managed Instance (preview) Architecture, see [Azure Monitor SCOM Managed Instance (preview)](operations-manager-managed-instance-overview.md).

## Register the SCOM Managed Instance resource provider

To register the SCOM managed Instance (preview) resource provider, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com) and select **Subscriptions**.
2. Select the subscription where you want to deploy SCOM Managed Instance (preview).
3. Under **Settings**, select **Resource providers**.
4. Search for **SCOM** and register **Microsoft.Scom**.
5. On the **Subscription** page, under **Settings**, select **Resource providers** and search for **microsoft.insights**. If the **microsoft.insights** provider isn't registered, select the provider, and then select **Register**.
6. On the **Subscription** page, under **Settings**, select **Resource providers** and search for **microsoft.Compute**. If the **microsoft.Compute** provider isn't registered, select the provider, and then select **Register**.

    :::image type="Microsoft Insights resource provider" source="media/register-scom-managed-instance-resource-provider/resource-provider-inline.png" alt-text="Screenshot of the Microsoft insights provider." lightbox="media/register-scom-managed-instance-resource-provider/resource-provider-expanded.png":::

## Next steps

- [Create separate subnet in a VNet](create-separate-subnet-in-vnet.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).