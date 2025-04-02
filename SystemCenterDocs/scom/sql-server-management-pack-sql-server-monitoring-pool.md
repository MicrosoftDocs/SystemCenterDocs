---
ms.assetid: d69cf961-ec43-4dd8-9b53-14fddaf078fa
title: SQL Server monitoring pool in Management Pack for SQL Server
description: This article explains SQL Server monitoring pool
author: epomortseva
ms.author: v-fkornilov
manager: evansma
ms.date: 04/02/2025
ms.topic: article
ms.service: system-center
ms.subservice: operations-manager
---

# SQL Server Monitoring Pool

You can configure **SQL Server Monitoring Pool** manually by adding custom gateways and management servers. Custom management server resource pools are also supported for [Agentless](sql-server-management-pack-monitoring-modes.md#configuring-agentless-monitoring-mode) monitoring mode.

To configure SQL Server Monitoring Pool, follow these steps:

1. Navigate to **Administration | Resource Pools** and in the list of resource pools, right-click **SQL Server Monitoring Pool**.

2. Select the **Manual Membership** option and select **Properties**.

    ![Screenshot showing the Manual membership properties.](./media/sql-server-management-pack/resource-pool-manual-membership.png)

3. In the **SQL Server Monitoring Pool Properties** window, open the **Pool Membership** tab and select **Add** to populate the monitoring pool.

    ![Screenshot showing Adding pool membership.](./media/sql-server-management-pack/adding-pool-membership-manual.png)

4. If the pool is empty, it mirrors the contents of the **All Management Servers** pool. The pool can contain either gateways or management servers, but not both at the same time.

    ![Screenshot showing Configure pool membership.](./media/sql-server-management-pack/resource-pool-selecting-servers.png)

5. At the **Summary** step, check the settings and select **Save**.

    ![Screenshot showing the Review summary information.](./media/sql-server-management-pack/summary-resource-pool.png)
