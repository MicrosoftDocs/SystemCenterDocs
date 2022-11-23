---
title: Register the SPF endpoint in Microsoft Azure Pack
description: Provides information about registering the SPF endpoint in Microsoft Azure Pack
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 11/18/2022
ms.topic: article
ms.prod: system-center
ms.technology: service-provider-foundation
ms.custom: engagement-fy23
---



# Register the SPF endpoint in Microsoft Azure Pack

::: moniker range=">= sc-spf-1801 <= sc-spf-1807"

[!INCLUDE [eos-notes-service-provider-foundation.md](../includes/eos-notes-service-provider-foundation.md)]

::: moniker-end


For System Center - Service Provider Foundation (SPF) to provide services and connectivity for delivering IaaS in Microsoft Azure Pack,  you need to register it.

1. On the SPF server, note the credentials used for the Admin, VMM, Usage, and Provider Application Pool identity in IIS.
2. Register the SPF endpoint with the Azure Pack management portal. After registration, you can enable the VM Clouds service from the portal.