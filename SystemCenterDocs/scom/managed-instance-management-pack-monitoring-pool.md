---
ms.assetid: 847ad457-3a51-4ecd-8aac-dde7539339c5
title: Managed instance monitoring pool in Management Pack for Azure SQL Managed Instance
description: This article explains how to configure monitoring pool in Management Pack for Azure SQL Managed Instance
author: TDzakhov
manager: evansma
ms.author: jsuri
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Managed Instance Monitoring Pool

To configure a monitoring pool using the Operations Manager console, perform the following steps:

1. Navigate to **Administration | Resource Pools**, right-click **Azure SQL MI Monitoring Pool**, and select the **Manual Membership** option.

2. Click **Properties**.

3. At the **General Properties** step, enter a name and description for the resource pool, and click **Next**.

    ![Configure general properties](./media/managed-instance-management-pack/resource-pool-name-and-description.png)

4. At the **Pool Membership** step, click **Add**, select management or gateway servers and click **OK**.

    If the pool is empty, it mirrors the contents of the **All Management Servers** pool. The pool can contain either gateways or management servers, but not both at the same time.

    ![Configure pool membership](./media/managed-instance-management-pack/selecting-servers.png)

5. Click the **Next**.

    ![Review added members](./media/managed-instance-management-pack/resource-and-members.png)

6. At the **Summary** step, check the settings and click **Save**.

    ![Review summary information](./media/managed-instance-management-pack/summary-pool.png)

7. At the **Completion** step, click **Close**.
