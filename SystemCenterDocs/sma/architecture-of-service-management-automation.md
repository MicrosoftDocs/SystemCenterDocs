---
title: Service Management Automation architecture in System Center
description: Provides an overview of the architecture in System Center Service Management Automation (SMA)
manager: mkluck
ms.topic: article
author: jyothisuri
ms.author: jsuri
ms.prod: system-center
ms.date: 02/22/2023
ms.technology: service-management-automation
ms.custom: engagement-fy23
---

# Service Management Automation architecture

::: moniker range=">= sc-sma-1801 <= sc-sma-1807"

[!INCLUDE [eos-notes-service-management-automation.md](../includes/eos-notes-service-management-automation.md)]

::: moniker-end

This article shows a diagram that illustrates System Center - Service Management Automation (SMA) features.


![SMA architecture diagram.](/system-center/sma/media/architecture-of-service-management-automation/smaarchitecture.png)

 ## Features

  - The SMA web service communicates with Microsoft Azure Pack and authenticates users.
  - The SQL Server databases store and retrieve many components. These include runbooks, runbook assets, activities, integration modules, and runbook job information.
  - Runbook workers run the runbooks, and they can be used for load balancing.
  The management portal in Microsoft Azure Pack is where you author, debug, start, and stop runbooks.

## Next steps

- Learn [what's new](./whats-new-in-sma.md) in the latest version of SMA.
