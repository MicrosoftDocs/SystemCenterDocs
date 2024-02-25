---
ms.assetid: b4dbae9a-cf0d-4598-96d8-421e10681e45
title: SQL Server reporting in Management Pack for SQL Server
description: This article explains SQL Server reporting
author: Anastas1ya
ms.author: v-ekaterinap
manager: evansma
ms.date: 3/17/2021
ms.topic: article
ms.service: system-center
ms.subservice: operations-manager
---

# SQL Server Reporting

Management Pack for SQL Server introduces the **Database Files Space Usage Forecast** report that provides the following information about Windows objects:

- Initially consumed file space (GB)
- Finally consumed file space (GB)
- File space consumption forecast (GB)

> [!IMPORTANT]
> The **Database Files Space Usage Forecast** report relies on several performance collection rules and discoveries that are disabled by default. These ***must*** be enabled and allowed to run for *several days* before this report will generate any data. Please create overrides for the below rules and discoveries for either All Objects of Class, or individual objects if you only want to collect data from certain SQL instances:
> 
>**Discoveries**
> - MSSQL on Windows: Discover SQL Server DB Files
> - MSSQL on Windows: Discover SQL Server DB Filegroups
>
>**Rules**
> - MSSQL on Windows: ROWS Data Allocated Free Space (MB)
> - MSSQL on Windows: ROWS Data Free Space Total (MB) 
> - MSSQL on Windows: ROWS Data Allocated Free Space (%)
> - MSSQL on Windows: ROWS Data Free Space Total (%)To open the report, perform the following steps:

Once these rules and discoveries have had time to collect data to report on, the report can be executed by:

1. In the **Reporting** view, double-click **Database Files Space Usage Forecast**.

    ![Screenshot showing Database usage forecast.](./media/sql-server-management-pack/database-files-space-usage-forecast.png)
   
1. Using the **Add Group** option in the parameters, add a group of DB Engine objects, a default option is "MSSQL on Windows: DB Engine Group". If adding an individual object, use the **Add Object** option and ensure to select the **DB Engine** object for the SQL Instance you want a forecast report for.

    ![Screenshot showing Adding objects and groups.](./media/sql-server-management-pack/adding-objects-and-groups.png)
   
1. Select a period and the corresponding time zone for the report. Also, select the number of days for the file space consumption forecast.

    ![Screenshot showing the Forecast period.](./media/sql-server-management-pack/forecast-period.png)
   
1. Select **Run**.

    The report displays a separate chart for each selected object or a group of objects.

    ![Screenshot showing Forecast chart.](./media/sql-server-management-pack/forecast-chart.png)
<br>
    A space usage forecast can be reviewed in a separate table.

    ![Screenshot showing Forecast space usage.](./media/sql-server-management-pack/forecast-space-usage.png)
