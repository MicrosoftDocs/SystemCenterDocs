---
ms.assetid: 613e32b0-3f29-45f2-b7ca-897789564f5c
title: Management Pack for SQL Server Replication configuration
description: This article explains management pack configuration
author: TDzakhov
ms.author: v-tdzakhov
manager: evansma
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Management Pack Configuration

Management Pack for Microsoft SQL Server Replication is sealed; you cannot change any of the original settings.

To change original settings, you can create a custom management pack to keep overrides and new monitoring objects.

Creating a custom management pack for storing overrides has the following advantages:

- Quick export of customized settings from the test environment to production environment.

- You do not have to remove dependencies when removing the management pack with overrides.

- If customizations for all management packs are saved to the default management pack and you want to remove a single pack, you must first remove the default management pack, which also removes customizations for other management packs.

To create a new management pack, perform the following steps:

1. Open the System Center Operations Manager console.

2. In the **Administration** view, right-click **Management Packs**, and select **Create New Management Pack**.

    ![Creating New Management Pack for Customizations](./media/sql-replication-management-pack/creating-new-management-pack.png)

3. Enter a new name, click **Next**, and click **Create**.
