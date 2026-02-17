---
ms.assetid: bcce1331-7f00-413c-ba3d-25f03cc63741
title: Configuring datacenter dashboard in Management Pack for SQL Server Dashboards
description: This article explains how to create and configure datacenter dashboards
author: Anastas1ya
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.topic: how-to
ms.service: system-center
ms.subservice: operations-manager
ms.update-cycle: 1095-days
---

# Configuring Datacenter Dashboard

It's recommended to store datacenter dashboards in a separate management pack to allow easy exporting and reusing configured views.

## Creating Management Pack

To create a new management pack, perform the following steps:

1. Open the **Administration** view and select **Management Packs**.

2. Right-click **Management Packs** and select **Create Management Pack**.

## Creating Datacenter Dashboard

To create a new datacenter dashboard, perform the following steps:

1. Open the Operations Manager console.

2. In the **Monitoring** view, right-click a folder for a new dashboard, and select **New** > **Dashboard View**.

3. At the **Template** step, select **SQL Server Dashboards** and select **Next**.

    ![Screenshot showing Select a template.](./media/sql-server-dashboards-management-pack/selecting-template.png)

4. At the **General Properties** step, specify a name and description for the template.

    ![Screenshot showing General properties.](./media/sql-server-dashboards-management-pack/general-properties.png)

5. At the **Summary** step, select **Create** and wait until the dashboard view is created.

    ![Screenshot showing Summary information.](./media/sql-server-dashboards-management-pack/summary.png)

6. At the **Completion** step, select **Close**.

    ![Screenshot showing Final step of the wizard.](./media/sql-server-dashboards-management-pack/completion.png)

A new dashboard has no groups by default and only the **Home** note (not clickable) that represents the root of breadcrumbs and datacenter menu is available.

While the dashboard is in the **Loading…** state, the hamburger button and the **Home** title aren't displayed.
