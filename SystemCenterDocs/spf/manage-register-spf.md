---
title: Register the SPF endpoint in Windows Azure Pack
description: Provides information about registering the SPF endpoint in Windows Azure Pack
<<<<<<< HEAD
author: JYOTHIRMAISURI
ms.author: v-jysur
=======
author: jyothisuri
ms.author: jsuri
>>>>>>> 73a7e82ddcf68c0a533d66b4273e8c40205fb9d1
manager: carmonm
ms.date: 01/22/2018
ms.topic: article
ms.prod: system-center
ms.technology: service-provider-foundation
---



# Register the SPF endpoint in Windows Azure Pack

::: moniker range=">= sc-spf-1801 <= sc-spf-1807"

[!INCLUDE [eos-notes-service-provider-foundation.md](../includes/eos-notes-service-provider-foundation.md)]

::: moniker-end


For System Center - Service Provider Foundation (SPF) to provide services and connectivity for delivering IaaS in Windows Azure Pack,  you need to register it.

1. On the SPF server, note the credentials used for the Admin, VMM, Usage, and Provider Application Pool identity in IIS.
2. Register the SPF endpoint with the Azure Pack management portal. After it's registered you can enable the VM Clouds service from the portal.
