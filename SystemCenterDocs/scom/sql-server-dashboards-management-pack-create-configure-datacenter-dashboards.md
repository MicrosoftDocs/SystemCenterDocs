---
ms.assetid: bcce1331-7f00-413c-ba3d-25f03cc63741
title: Configuring datacenter dashboard in Management Pack for SQL Server Dashboards
description: This article explains how to create and configure datacenter dashboards
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Configuring Datacenter Dashboard

It is recommended to store datacenter dashboards in a separate management pack to allow easy exporting and re-using configured views.

## Creating Management Pack

To create a new management pack, perform the following steps:

1. Open the **Administration** view and click **Management Packs**.

2. Right-click **Management Packs** and select **Create Management Pack**.

## Creating Datacenter Dashboard

To create a new datacenter dashboard, perform the following steps:

1. Open the Operations Manager console.

2. In the **Monitoring** view, right-click a folder for a new dashboard, and select **New** > **Dashboard View**.

3. At the **Template** step, select **SQL Server Dashboards** and click **Next**.

    ![Select a template](./media/sql-server-dashboards-management-pack/selecting-template.png)

4. At the **General Properties** step, specify a name and description for the template.

    ![General properties](./media/sql-server-dashboards-management-pack/general-properties.png)

5. At the **Summary** step, click **Create** and wait until the dashboard view is created.

    ![Summary information](./media/sql-server-dashboards-management-pack/summary.png)

6. At the **Completion** step, click **Close**.

    ![Final step of the wizard](./media/sql-server-dashboards-management-pack/completion.png)

A new dashboard has no groups by default and only the **Home** note (not clickable) that represents the root of breadcrumbs and datacenter menu is available.

While the dashboard is in the **Loading…** state, the hamburger button and the **Home** title are not displayed.
