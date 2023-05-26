---
ms.assetid: b4dbae9a-cf0d-4598-96d8-421e10681e45
title: SQL Server reporting in Management Pack for SQL Server
description: This article explains SQL Server reporting
author: Anastas1ya
ms.author: v-ekaterinap
manager: evansma
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# SQL Server Reporting

Management Pack for SQL Server introduces the **Database Files Space Usage Forecast** report that provides the following information about Windows objects:

- Initially consumed file space (GB)
- Finally consumed file space (GB)
- File space consumption forecast (GB)

To open the report, perform the following steps:

1. In the **Reporting** view, double-click **Database Files Space Usage Forecast**.

    ![Screenshot showing Database usage forecast.](./media/sql-server-management-pack/database-files-space-usage-forecast.png)

2. In the **Add Group** window, add an object or a group of objects.

    ![Screenshot showing Adding objects and groups.](./media/sql-server-management-pack/adding-objects-and-groups.png)

3. Select a period and the corresponding time zone for the report. Also, select the number of days for the file space consumption forecast.

    ![Screenshot showing the Forecast period.](./media/sql-server-management-pack/forecast-period.png)

4. Select **Run**.

The report displays a separate chart for each selected object or a group of objects.

![Screenshot showing Forecast chart.](./media/sql-server-management-pack/forecast-chart.png)

A space usage forecast can be reviewed in a separate table.

![Screenshot showing Forecast space usage.](./media/sql-server-management-pack/forecast-space-usage.png)
