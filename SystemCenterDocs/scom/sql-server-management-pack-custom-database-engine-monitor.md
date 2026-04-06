---
ms.assetid: dc45fd44-50ff-47af-bfdd-5407695c6cae
title: Custom database engine query-based monitors in System Center Management Pack for SQL Server
description: This article explains how to configure a custom database engine query monitor in System Center Management Pack for SQL Server.
author: epomortseva
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
ms.update-cycle: 1095-days
---

# Custom query-based database engine monitors

If the set of default monitors in System Center Management Pack for SQL Server isn't enough to cover your workflows, you can create a monitor that targets the SQL Server Database Engine for Windows and Linux platforms.

During the monitor creation process, you use *conditions* to define how the monitor will determine the state after it receives query results. The approach for creating query-based monitors is similar to the approach for creating SQL Server policies. If the query result matches the condition, the monitor state is healthy. If the result doesn't match the condition, the monitor is unhealthy and shows an alert.

There are two types of unit monitors based on custom queries that you can create for the SQL Server Database Engine: two-state monitors and three-state monitors.

> [!NOTE]
> Since the latest preview version of System Center Management Pack for SQL Server 7.1.0.0, the management pack for the custom monitoring feature is on a separate package installer: *SQLServerMP.CustomMonitoring.msi*. Be sure to import the management pack file *Microsoft.SQLServer.Core.CustomMonitoring.mpb* manually. The import process with the update option is not supported.

For detailed examples of how to use custom monitors targeting SQL Server Database Engine, refer to [Examples of usage](sql-server-management-pack-custom-monitoring-examples.md).

## Two-state custom database engine monitor

To create a two-state custom query-based monitor, perform the following steps:

1. In the System Center Operations Manager console, go to **Authoring** > **Management Pack Objects**. Right-click **Monitors**, select **Create a Monitor**, and then select **Unit Monitor**.

    ![Screenshot of selections for creating a two-state unit monitor.](./media/sql-server-management-pack/sql-creating-unit-monitor.png)

2. At the **Monitor Type** step, select **Microsoft SQL Server** > **DB Engine** > **User-defined SQL Query Two-State Monitor**.

3. From the **Select destination management pack** dropdown list, select a management pack that you want to use, or select **New** to create a new one. Then select **Next**.

    ![Screenshot of selecting a monitor type.](./media/sql-server-management-pack/sql-selecting-monitor-type.png)

4. At the **General Properties** step, enter the monitor name and an optional description. Make your selections for **Monitor target** and **Parent monitor**. If you want the monitor to be enabled by default, select the **Monitor is enabled** checkbox. Then select **Next**.

    ![Screenshot of selecting a monitor name and description.](./media/sql-server-management-pack/sql-custom-monitor-name-and-description.png)

5. At the **SQL Query** step, enter the database name, query text, and timeouts (in seconds). The default database is **master**.

    ![Screenshot that shows a target database name and SQL query.](./media/sql-server-management-pack/sql-unit-monitor-sql-query.png)

6. At the **Conditions** step, add one or more conditions to verify query results.

   Condition supports two modes of evaluation:

   - **ANY** - if any of the conditions are violated, the monitor switches to an unhealthy state.
  
   - **ALL** - if all the conditions are violated, the monitor switches to an unhealthy state.

    To add a new condition, select **Add**, and then select one of the available conditions:

    - **Empty Result Set**

      Checks if the specified result set that the query returned is empty.

    - **Not Empty Result Set**

      Checks if the specified result set that the query returned isn't empty.

    - **Scalar Value**

      Checks the scalar value in the specified cell of the result set. Only equal comparison is available at this moment. If you need complex logic, you can cover that with the query.

    ![Screenshot that shows adding new conditions.](./media/sql-server-management-pack/sql-unit-monitor-conditions.png)

    When you add a condition, you must specify **Friendly name** and **Configuration** details for a specific check to be performed.

    ![Screenshot that shows scalar values.](./media/sql-server-management-pack/sql-editing-test-conditions.png)

    You can use a scalar value with two options:

    - **Is NULL** is a true\false verification option. If the value is false, the monitor is unhealthy. Otherwise, the monitor is healthy.
    - Use **Equal to** to insert the specific value. If the result of the query matches the number value, the monitor is healthy. Otherwise, the monitor is unhealthy.

      > [!NOTE]
      > The **Equal to** option is culture-independent (invariant) for a single value only and can't parse a range of values. Example of use: *3.14*, *2023-05-25*, or an arbitrary text.

    You can make more than one condition. If you want to add, edit, or remove a condition, select the condition and use the appropriate button.

    ![Screenshot that shows multiple conditions.](./media/sql-server-management-pack/sql-unit-monitor-multiple-conditions.png)

    After you finish setting all the required conditions, select **Next**.

7. At the **Property Bag** step, add one or more conditions to parse the sql query result into a property bag to add properties to the alert context. This step can be skipped if the default alert context is sufficient for display.

    ![Screenshot of configuring property bag.](./media/sql-server-management-pack/sql-unit-monitor-property-bag.png)


    To add a new condition, select **Add**, and then select **Scalar Value**. When you add a condition, you must specify **Friendly name** and **Configuration** details for a specific check to be performed.

    ![Screenshot of property bag condition.](./media/sql-server-management-pack/sql-unit-monitor-alert-condition.png)

  
    After you finish setting all the required conditions, select **Next**.

8. At the **Schedule** step, configure a query execution schedule and synchronization time.

    ![Screenshot of configuring a schedule.](./media/sql-server-management-pack/sql-unit-monitor-schedule.png)

9. At the **Schedule Filter** step, select the schedule filtering mode with the following options:

    - **Always process data**

      This is the regular mode, in which the monitor processes the data all the time. This mode doesn't support the time range schedule and excludes day options.

    - **Only process data during the specified time**
  
      In this mode, you schedule monitoring by selecting a date and time range during the week.

    - **Process data except during the specified time**

      In this mode, you exclude days so that the monitor doesn't track the specified time periods. You can exclude it temporarily by using the **Exclude days** button. You can exclude it permanently by using the time range schedule.

   ![Screenshot of schedule filter creation in custom monitors.](./media/sql-server-management-pack/sql-unit-monitor-schedule-filter.png)

   To specify the time range for both **Only process data during the specified time** and **Process data except during the specified time** modes, use the **Add** button and select the days and times.

   ![Screenshot of selecting a time range for a monitor.](./media/sql-server-management-pack/sql-unit-monitor-select-time-range-in-filter.png)

   To exclude some days from the schedule, use the **Exclude days** button and choose the date range by using the **Start** and **End** fields. Complete the description, if applicable.

   ![Screenshot of the button for excluding days in schedule filter creation.](./media/sql-server-management-pack/exclude-days-in-filter.png)

   You can use both options to exclude time ranges and days at the same time.

   ![Screenshot that shows using both schedule filtering options.](./media/sql-server-management-pack/schedule-filter-with-filled-options.png)

10. At the **Configure Health** step, select the health state that the monitor should generate. Change the **Operational State** information if needed.

    ![Screenshot of configuring health.](./media/sql-server-management-pack/custom-monitor-configure-health.png)  

11. At the **Configure Alerts** step, enable the generating of alerts and edit the **Alert properties** area if needed.

    If you need to activate alerts for the monitor, select the **Generate alerts for this monitor** checkbox, and set up an alert name and description to be shown when conditions fail. Change priority and severity, and resolve the alert mode.

    Use the `$Data/Context/Property[@Name=’Message’]$` placeholder to show the list of failed conditions in the alert description.

    When you're finished configuring alert properties, select **Create**.

    ![Screenshot of editing alerts.](./media/sql-server-management-pack/custom-monitor-editing-alerts.png)  

> [!TIP]
> By default, a custom query-based monitor works for all SQL Server instances. To avoid alert storming you need to override the monitor target only to a specific instance of the SQL Server. To do that, in the monitor's override properties set the **Enabled = False** for the **MSSQL on Windows: DB Engine class**, and set the **Enabled = True** for the **specific SQL Server DB Engine** object.

## Three-state monitor

Creating a three-state custom query-based monitor is similar to creating a two-state monitor. The main difference is that you select **User-defined SQL Query Three-State Monitor** at the **Monitor Type** step. Then, you can specify details for **Warning Conditions** and **Critical Conditions** steps.

A critical state has a higher priority than a warning in three-state monitors, and it's verified first. If one or more critical conditions fail, the monitor switches to the critical state, and warning conditions aren't verified.

![Screenshot that shows a warning and a critical condition for a three-state monitor.](./media/sql-server-management-pack/sql-unit-monitor-warning-and-critical-conditions.png)

When you use the **Equal to** condition in a three-state monitor:

- Choose a value.
- Use conditions with unhealthy states that will be determined for the desired monitor's operational state.
- Keep in mind the alert priority: the critical state is verified first.
