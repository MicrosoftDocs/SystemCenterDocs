---
title: Register the SPF endpoint in Microsoft Azure Pack
description: Provides information about registering the SPF endpoint in Microsoft Azure Pack
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 08/07/2023
ms.topic: article
ms.prod: system-center
ms.technology: service-provider-foundation
ms.custom: UpdateFrequency2, engagement-fy24
---



# Register the SPF endpoint in Microsoft Azure Pack

::: moniker range=">= sc-spf-1801 <= sc-spf-1807"

[!INCLUDE [eos-notes-service-provider-foundation.md](../includes/eos-notes-service-provider-foundation.md)]

::: moniker-end


For System Center - Service Provider Foundation (SPF) to provide services and connectivity for delivering IaaS in Microsoft Azure Pack, you need to register it.

1. On the SPF server, note the credentials used for the Admin, VMM, Usage, and Provider Application Pool identity in IIS.
2. Register the SPF endpoint with the Azure Pack management portal. After registration, you can enable the VM Clouds service from the portal.