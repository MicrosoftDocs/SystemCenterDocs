---
ms.assetid: 
title: Register the Azure Monitor SCOM Managed Instance resource provider
description: This article describes how to register the SCOM Managed Instance resource provider.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 11/14/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: how-to
monikerRange: '>=sc-om-2019'
---

# Register the Azure Monitor SCOM Managed Instance resource provider

This article describes how to register the Azure Monitor SCOM Managed Instance resource provider.

>[!NOTE]
> To learn about the SCOM Managed Instance architecture, see [Azure Monitor SCOM Managed Instance](operations-manager-managed-instance-overview.md).

## Register the SCOM Managed Instance resource provider

To register the SCOM Managed Instance resource provider, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com) and select **Subscriptions**.
1. Select the subscription where you want to deploy SCOM Managed Instance.
1. Under **Settings**, select **Resource providers**.
1. Search for **SCOM** and register **Microsoft.Scom**.
1. On the **Subscription** page, under **Settings**, select **Resource providers** and search for **microsoft.insights**. If the **microsoft.insights** provider isn't registered, select the provider, and then select **Register**.
1. On the **Subscription** page, under **Settings**, select **Resource providers** and search for **microsoft.Compute**. If the **microsoft.Compute** provider isn't registered, select the provider, and then select **Register**.

    :::image type="Microsoft Insights resource provider" source="media/register-scom-managed-instance-resource-provider/resource-provider-inline.png" alt-text="Screenshot that shows the Microsoft insights provider." lightbox="media/register-scom-managed-instance-resource-provider/resource-provider-expanded.png":::

## Next steps

- [Create a separate subnet in a virtual network](create-separate-subnet-in-vnet.md)