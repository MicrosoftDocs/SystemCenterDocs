---
ms.assetid: 8285d0f9-7069-4abf-b83e-ba5898dd73ff
title: Enable Agent Proxy option in management pack for SQL Server
description: This article explains how to enable the agent proxy option
author: Anastas1ya
ms.author: v-gajeronika
ms.date: 07/22/2025
ms.topic: how-to
ms.service: system-center
ms.subservice: operations-manager
---

# Enable Agent Proxy Option

The **Agent Proxy** option should be enabled in cases when the agent workflow scenarios discover any non-hosted objects created by the management pack for each SQL Server instance.

## Enable Agent Proxy

To enable the **Agent Proxy** option, follow these steps:

1. Open the System Center Operations Manager console.

2. In the **Administration** view, select **Agent Managed**.

3. Double-click an agent.

4. On the **Security** tab, select the **Allow this agent to act as a proxy and discover managed objects on other computers** checkbox, and select **OK**.

    ![Screenshot showing Enable agent proxy option.](./media/sql-server-management-pack/enabling-agent-proxy-option.png)
