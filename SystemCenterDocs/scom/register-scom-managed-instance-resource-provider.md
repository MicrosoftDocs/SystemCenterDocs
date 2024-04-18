---
ms.assetid: 
title: Register the Azure Monitor SCOM Managed Instance resource provider
description: This article describes how to register the SCOM Managed Instance resource provider.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/15/2024
ms.custom: UpdateFrequency.5
ms.service: system-center
ms.subservice: operations-manager-managed-instance
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
1. On the **Subscription** page, under **Settings**, select **Resource providers** and search for **Microsoft.Scom**. If the **Microsoft.Scom** provider isn't registered, select the provider, and then select **Register**.

    :::image type="Microsoft resource provider" source="media/register-scom-managed-instance-resource-provider/resource-providers-inline.png" alt-text="Screenshot that shows the Microsoft provider." lightbox="media/register-scom-managed-instance-resource-provider/resource-providers-expanded.png":::

1. On the **Subscription** page, under **Settings**, select **Resource providers** and search for **microsoft.insights**. If the **microsoft.insights** provider isn't registered, select the provider, and then select **Register**.

    :::image type="Microsoft Insights resource provider" source="media/register-scom-managed-instance-resource-provider/resource-provider-insights-inline.png" alt-text="Screenshot that shows the Microsoft insights provider." lightbox="media/register-scom-managed-instance-resource-provider/resource-provider-insights-expanded.png":::

1. On the **Subscription** page, under **Settings**, select **Resource providers** and search for **Microsoft.Compute**. If the **Microsoft.Compute** provider isn't registered, select the provider, and then select **Register**.

    :::image type="Microsoft compute resource provider" source="media/register-scom-managed-instance-resource-provider/resource-provider-compute-inline.png" alt-text="Screenshot that shows the Microsoft compute provider." lightbox="media/register-scom-managed-instance-resource-provider/resource-provider-compute-expanded.png":::

## Next steps

- [Create a separate subnet in a virtual network](create-separate-subnet-in-vnet.md)