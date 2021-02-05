---
ms.assetid: b4dbae9a-cf0d-4598-96d8-421e10681e45
title: SQL Server Reporting
description: This article explains SQL Server Reporting
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 2/5/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# SQL Server Reporting

Management Pack for SQL Server introduces the **Database Files Space Usage Forecast** report that provides the following information:

- Initially consumed file space (GB)

- Finally consumed file space (GB)

- Initial average free file space (%)

- Final average free file space (%)

- File space consumption forecast (GB)

Note that this report works with Windows objects only.

To open the report, perform the following steps:

1. In the **Reporting** view, double-click **Database Files Space Usage Forecast**.

    ![Database files Space Usage Forecast](./media/ssmp/database-files-space-usage-forecast.png)

2. In the **Add Group** window, add an object or a group of objects.

    ![Database files Space Usage Forecast](./media/ssmp/adding-objects-and-groups.png)

3. Select a period and the corresponding time zone for the report. Also, select the number of days for the file space consumption forecast.

    ![Database files Space Usage Forecast](./media/ssmp/forecast-period.png)

4. Click **Run**.

The report displays a separate chart for every selected object or a group of objects.

![Database files Space Usage Forecast](./media/ssmp/forecast-chart.png)

A space usage forecast can be reviewed in a separate table.

![Database files Space Usage Forecast](./media/ssmp/forecast-space-usage.png)