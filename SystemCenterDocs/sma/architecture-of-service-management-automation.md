---
title: Service Management Automation Architecture in System Center
description: Provides an overview of the architecture in System Center Service Management Automation (SMA).
ms.topic: concept-article
author: Jeronika-MS
ms.author: v-gajeronika
ms.service: system-center
ms.date: 08/20/2025
ms.subservice: service-management-automation
ms.custom: UpdateFrequency2, engagement-fy24
---

# Service Management Automation architecture

This article shows a diagram that illustrates System Center - Service Management Automation (SMA) features.

![SMA architecture diagram.](./media/architecture-of-service-management-automation/smaarchitecture.png)

>[!NOTE]
>As Windows Azure Pack is now deprecated, you can use PowerShell ISE add-on as an alternative. For more information, see [Introducing Service Management Automation ISE add-on](https://techcommunity.microsoft.com/blog/systemcenterblog/introducing-service-management-automation-ise-add-on/351500).

## Features

- The SMA web service communicates with Windows Azure Pack and authenticates users.
- The SQL Server databases store and retrieve many components. These include runbooks, runbook assets, activities, integration modules, and runbook job information.
- Runbook workers run the runbooks, and they can be used for load balancing.
  The management portal in Windows Azure Pack is where you author, debug, start, and stop runbooks.

## Next steps

Learn [what's new](./whats-new-in-sma.md) in the latest version of SMA.
