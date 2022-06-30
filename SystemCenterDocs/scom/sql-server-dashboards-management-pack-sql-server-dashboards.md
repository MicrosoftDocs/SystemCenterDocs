---
ms.assetid: e972e309-dfc8-4613-a181-e2be233e8053
title: SQL Server web dashboards in Management Pack for SQL Server Dashboards
description: This article explains SQL Server web dashboards
author: Anastas1ya
ms.author: v-asimanovic
manager: evansma
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# SQL Server Web Dashboards

With System Center Operations Manager 2019 and later, you can access SQL Server dashboards using a web browser.

To open web dashboards, perform the following steps:

1. Navigate to http://localhost/OperationsManager using a web browser.

2. Open the **Monitoring** view, navigate to **Monitoring** > **Microsoft SQL Server**, and click **Summary**.

    Make sure that you have installed the **Web console** component.

![Summary](./media/sql-server-dashboards-management-pack/web-summary.png)

On the **Summary** page, click a tile to drill-down and review detailed information about the state and alerts.

![Web alerts and state](./media/sql-server-dashboards-management-pack/state-alerts.png)

The **Filter** column in the left pane shows objects that might be in the **Critical**, **Warning**, or **Healthy** state. You can select an object to review its details, such as **Monitoring Type**, **Principal Name**, **Authentication Mode** etc. in the **Details** column.

![Filter](./media/sql-server-dashboards-management-pack/filtering-states.png)

The right pane consists of tiles that show the health state of various components that belong to the object that you select in the **Filter** column.

In the right pane, you can click the first tile in the top-left corner that shows **State** and **Alerts** to drill-down into the health hierarchy even further.

![Drilling the health hierarchy](./media/sql-server-dashboards-management-pack/filtered-health-state.png)

To get back to the previous view, you can click **Back**. You can also launch **Health Explorer**.

![Back](./media/sql-server-dashboards-management-pack/getting-back.png)
