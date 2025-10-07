---
ms.assetid: 847ad457-3a51-4ecd-8aac-dde7539339c5
title: Managed instance monitoring pool in Management Pack for Azure SQL Managed Instance
description: This article explains how to configure monitoring pool in Management Pack for Azure SQL Managed Instance
author: epomortseva
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.topic: how-to
ms.service: system-center
ms.subservice: operations-manager
ms.custom: engagement-fy23
---

# Azure SQL Managed Instance Monitoring Pool

You can configure Azure SQL MI Monitoring Pool manually by adding custom gateways and management servers. Custom management server resource pools are also supported.

To configure a monitoring pool using the Operations Manager console, perform the following steps:

1. Navigate to **Administration | Resource Pools**, right-click **Azure SQL MI Monitoring Pool**.

2. Select the **Manual Membership** option, then right-click again **Azure SQL MI Monitoring Pool** and select **Properties**.

   ![Screenshot showing the Manual membership properties.](./media/managed-instance-management-pack/resource-pool-manual-membership.png)

3. In the **Azure SQL MI Monitoring Pool** Properties window, open the **Pool Membership** tab and select **Add** to populate the monitoring pool.

    ![Screenshot showing Added pool members.](./media/managed-instance-management-pack/resource-pool-and-members.png)

4. If the pool is empty, it mirrors the contents of the **All Management Servers** pool. The pool can contain either gateways or management servers, but not both at the same time.

    ![Screenshot showing Configure pool membership.](./media/managed-instance-management-pack/resource-pool-selecting-servers.png)

5. At the **Summary** step, check the settings and select **Save**.

    ![Screenshot showing the Review summary information.](./media/managed-instance-management-pack/summary-resource-pool.png)
