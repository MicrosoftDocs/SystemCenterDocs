---
ms.assetid: 
title: Examples of custom query-based monitors in the System Center Management Pack for SQL Server
description: This article shows examples of configuring custom query monitors and performance rules in the System Center Management Pack for SQL Server.
manager: evansma
author: fkornilov
ms.author: v-fkornilov
ms.date: 06/21/2024
ms.topic: article
ms.service: system-center
ms.subservice: operations-manager
---

# Examples of usage

All examples of using custom query-based monitors and performance rules based on the `AdventureWorks` sample database that can be found on the [installation](/sql/samples/adventureworks-install-configure) page or directly within the [SQL Server samples](https://github.com/microsoft/sql-server-samples) GitHub repository.

## Prerequisites

- [SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).
- [AdventureWorks2022](/sql/samples/adventureworks-install-configure) database.

## Installing AdventureWorks2022 database

If you don't have a running instance of `AdventureWorks2022` database, you can follow these steps to install it:

- Download [AdventureWorks2022.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2022.bak) database sample backup with OLTP data, that is for most typical online transaction processing workloads. If you're not sure what sample you need, start with the OLTP version that matches your SQL Server version.
- [Restore AdventureWorks sample database](/sql/samples/adventureworks-install-configure?tabs=tsql#restore-to-sql-server) to your SQL Server using the `.bak` file. You can do so using the [RESTORE (Transact-SQL)](/sql/t-sql/statements/restore-statements-transact-sql) command, or using the graphical interface (GUI) in [SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).

## Custom query-based two-state monitor

There are two types of unit monitors based on custom queries that you can create: two-state monitors and three-state monitors. This article shows typical examples of the usage of two-state monitors.

## Example 1 with "Empty Result Set"

In this example, we consider the condition under which the `Sales.CreditCard` table is checked that there are no entries in the `ExpYear` column with the 2005 year:

```SQL
SELECT * FROM [Sales].[CreditCard]
WHERE ExpYear = 2005
```

As a result of this query, several records are returned:

![Screenshot of executing the query for the first example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-1-select-result.png)

To create a monitor that changes its state to unhealthy if the following table contains records with an expiration year of 2005, follow these steps:

  1. In the System Center Operations Manager console, go to **Authoring** > **Management Pack Objects**. Right-click **Monitors**, select **Create a Monitor**, and then select **Unit Monitor**.
  
        Select the **Microsoft SQL Server** > **DB Engine** > **User-defined SQL Query Two-State Monitor**.

        From the **Select destination management pack** dropdown list, select a management pack that you want to use, or select **New** to create a new one. Then select **Next**.

        ![Screenshot of selecting a monitor type.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-type-step.png)

  2. At the **General Properties** step, enter the monitor name as `[Sales].[CreditCard] table with Expiration Year values = 2005` and an optional description as `This monitor checks the [Sales].[CreditCard] table to find the rows with ExpYear values = 2005.`
  
        Make your selections for **Monitor target** as `MSSQL on Windows: Local DB Engine` and **Parent monitor** as any of the Entity Health options.
  
        If you want the monitor to be enabled by default, select the **Monitor is enabled** checkbox. Then select **Next**.

        ![Screenshot of selecting a monitor name and description.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-1-general-properties-step.png)

  3. At the **SQL Query** step, enter the database name as `AdventureWorks2022`, query text and timeouts (in seconds).

        ![Screenshot that shows a target database name and SQL query for the first example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-1-sql-query-step.png)

  4. At the **Conditions** step, select **ANY** condition that means if any of the added conditions are violated, the monitor switches to an unhealthy state; for this example, only 1 condition is needed.
  
        To add a new condition, select **Add**, and then select an **Empty Result Set** - this condition checks if the specified result set that the query returned is empty.

        ![Screenshot that shows adding empty result set condition for the first example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-1-conditions-edit-step.png)

        Thus, the monitor operates based on a condition that checks the query result if no rows corresponding to the expiring year 2005 are returned. Otherwise, the monitor switches to an unhealthy state.

        ![Screenshot that shows added new condition for the first example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-1-conditions-step.png)

  5. At the **Schedule** and **Schedule Filter** steps, leave the default values; the monitor will process the data without schedule, once per 15 minutes.

  6. At the **Configure Health** step, select the `Critical` health state that the monitor should generate if it's failed. Change the **Operational State** information if needed.

        ![Screenshot that shows configuring health for the first example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-configure-health-step.png)

  7. At the **Configure Alerts** step, enable the generating alerts and edit the **Alert properties**.
  
        Set the **Alert name** as `[Sales].[CreditCard] table with ExpYear values = 2005`.
  
        Set the **Alert description** as `The following conditions violated: $Data/Context/Property[@Name='Message']$ The [Sales].[CreditCard] table has rows with ExpYear values = 2005. Consider updating the table to eliminate outdated values.`

        When you're finished configuring alert properties, select **Create**.

        ![Screenshot that shows configuring alerts for the first example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-1-configure-alerts-step.png)

After the custom monitor is created and works, you can see how it changed its state and generated an alert. In our example, the monitor should switch to the critical state, since the resulting query returns several records in the `Sales.CreditCard` table with the expiring year 2005.

![Screenshot that shows alert properties for the first example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-1-monitor-alert-properties.png)

> [!TIP]
> By default, a custom query-based monitor works for all SQL Server instances. To avoid alert storming on instances where the sample database does not exist, you need to override the monitor target only to a specific instance of the SQL Server that hosts the AdventureWorks2022 database. To do that, in the monitor's override properties set the **Enabled = False** for the **MSSQL on Windows: DB Engine** class, and set the **Enabled = True** for the specific **SQL Server DB Engine** object that **hosts the AdventureWorks2022** sample database.

## Example 2 with "Empty Result Set"

In this example, we consider the condition under which the `Production.Illustration` table is checked that for each IllustrationID record is also exists an entry in the `Production.ProductModelIllustration` table since the Illustration table has the schema-bound dependency for the ProductModelIllustration table:

```SQL
SELECT *
FROM [Production].[Illustration] PIL
LEFT JOIN [Production].[ProductModelIllustration] PMI
ON PIL.IllustrationID = PMI.IllustrationID
WHERE PMI.IllustrationID IS NULL
```

As a result of this query, one record without a model illustration in the `Production.ProductModelIllustration` table returned:

![Screenshot of executing the query for the second example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-2-select-result.png)

To create a monitor that changes its state to unhealthy if the Illustration table does not contain models in the dependent ProductModelIllustration table, follow these steps:

  1. In the System Center Operations Manager console, go to **Authoring** > **Management Pack Objects**. Right-click **Monitors**, select **Create a Monitor**, and then select **Unit Monitor**.
  
        Select the **Microsoft SQL Server** > **DB Engine** > **User-defined SQL Query Two-State Monitor**.

        From the **Select destination management pack** dropdown list, select a management pack that you want to use, or select **New** to create a new one. Then select **Next**.

        ![Screenshot of selecting a monitor type for the second example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-type-step.png)

  2. At the **General Properties** step, enter the monitor name as `[Production].[Illustration] table has values w/o model in the [Production].[ProductModelIllustration] table` and an optional description as `This monitor checks the [Production].[Illustration] table to find the values with missed models in [Production].[ProductModelIllustration] table.`
  
        Make your selections for **Monitor target** as `MSSQL on Windows: Local DB Engine` and **Parent monitor** as any of the Entity Health options.
  
        If you want the monitor to be enabled by default, select the **Monitor is enabled** checkbox. Then select **Next**.

        ![Screenshot of selecting a monitor name and description for the second example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-2-general-properties-step.png)

  3. At the **SQL Query** step, enter the database name as `AdventureWorks2022`, query text and timeouts (in seconds).

        ![Screenshot that shows a target database name and SQL query for the second example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-2-sql-query-step.png)

  4. At the **Conditions** step, select **ANY** condition that means if any of the added conditions are violated, the monitor switches to an unhealthy state; for this example, only 1 condition is needed.
  
      To add a new condition, select **Add**, and then select an **Empty Result Set** - this condition checks if the specified result set that the query returned is empty.

      ![Screenshot that shows adding empty result set condition for the second example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-2-conditions-edit-step.png)

      Thus, the monitor operates based on a condition that checks the query result if no Illustration IDs without Models corresponding are returned. Otherwise, the monitor switches to an unhealthy state.

      ![Screenshot that shows added new condition for the second example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-2-conditions-step.png)

  5. At the **Schedule** and **Schedule Filter** steps, leave the default values; the monitor will process the data without schedule, once per 15 minutes.

  6. At the **Configure Health** step, select the `Critical` health state that the monitor should generate if it's failed. Change the **Operational State** information if needed.

        ![Screenshot that shows configuring health for the second example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-configure-health-step.png)

  7. At the **Configure Alerts** step, enable the generating alerts and edit the **Alert properties**.
  
        Set the **Alert name** as `[Production].[Illustration] table has values w/o model in the [Production].[ProductModelIllustration] table`.
  
        Set the **Alert description** as `The following conditions violated: $Data/Context/Property[@Name='Message']$ The [Production].[Illustration] table has rows without the following models in [Production].[ProductModelIllustration] table. Consider updating the [Production].[ProductModelIllustration] table to add missing data.`

        When you're finished configuring alert properties, select **Create**.

        ![Screenshot that shows configuring alerts for the second example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-2-configure-alerts-step.png)

After the custom monitor is created and works, you can see how it changed its state and generated an alert. In our example, the monitor should switch to the critical state, since the resulting query returns a record in the `Product.Illustration` table whereas there is no data for the `Product.ProductModelIllustration` table.

![Screenshot that shows alert properties for the second example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-2-monitor-alert-properties.png)

## Example 3 with "Not Empty Result Set and Scalar Value"

In this example, we consider the condition under which the `Person.Address` table is checked that for the `Kansas City` record the number of employees from the `Person.BusinessEntityAddress` table is no more than 1, furthermore, the result set of the query should not be empty - that means that the `Kansas City` record exists in the `Person.Address` table:

```SQL
SELECT PA.City, COUNT(PBEA.AddressID) NoOfEmployees
FROM Person.BusinessEntityAddress PBEA
INNER JOIN Person.Address PA
ON PBEA.AddressID = PA.AddressID
WHERE PA.City like 'Kansas City'
GROUP BY PA.City
```

As a result of this query, the `Kansas City` record exists and the number of employees for that city is 2:

![Screenshot of executing the query for the third example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-3-select-result.png)

To create a monitor that changes its state to unhealthy if the `Person.Address` table contains a `Kansas City` record with more than 1 employee, follow these steps:

1. In the System Center Operations Manager console, go to **Authoring** > **Management Pack Objects**. Right-click **Monitors**, select **Create a Monitor**, and then select **Unit Monitor**.
  
      Select the **Microsoft SQL Server** > **DB Engine** > **User-defined SQL Query Two-State Monitor**.

      From the **Select destination management pack** dropdown list, select a management pack that you want to use, or select **New** to create a new one. Then select **Next**.

      ![Screenshot of selecting a monitor type for the second example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-type-step.png)

2. At the **General Properties** step, enter the monitor name as `[Person].[Address] table has a specific city w/ extra NoOfEmployees values` and an optional description as `This monitor checks the number of employees from the [Person].[BusinessEntityAddress] table for the "Kansas City" record in the [Person].[Address table].`
  
      Make your selections for **Monitor target** as `MSSQL on Windows: Local DB Engine` and **Parent monitor** as any of the Entity Health options.
  
      If you want the monitor to be enabled by default, select the **Monitor is enabled** checkbox. Then select **Next**.

      ![Screenshot of selecting a monitor name and description for the third example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-3-general-properties-step.png)

3. At the **SQL Query** step, enter the database name as `AdventureWorks2022`, query text and timeouts (in seconds).

      ![Screenshot that shows a target database name and SQL query for the third example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-3-sql-query-step.png)

4. At the **Conditions** step, select **ANY** condition that means if any of the added conditions are violated, the monitor switches to an unhealthy state; for this example, both conditions are needed because the monitor checks not only the number of employees for a certain city, but also existing this city in the table:
  
      To add a first condition, select **Add**, and then select a **Not Empty Result Set** - this condition checks if the specified result set that the query returned is not empty:

      ![Screenshot that shows adding a not empty result set condition for the third example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-3-condition-1.png)

      To add a second condition, select **Add**, and then select a **Scalar Value** - this condition checks in the specified result set, specified row number, and specified column name that is cell value is equal to 1:

      ![Screenshot that shows adding a scalar value condition for the third example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-3-condition-2.png)

      Thus, the monitor operates based on conditions that checks that the query result is not empty and the number of employees is equal to 1. Otherwise, the monitor switches to an unhealthy state.

      ![Screenshot that shows all the conditions for the third example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-3-all-conditions-step.png)

5. At the **Schedule** and **Schedule Filter** steps, leave the default values; the monitor will process the data without schedule, once per 15 minutes.

6. At the **Configure Health** step, select the `Critical` health state that the monitor should generate if it's failed. Change the **Operational State** information if needed.

      ![Screenshot that shows configuring health for the third example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-configure-health-step.png)

7. At the **Configure Alerts** step, enable the generating alerts and edit the **Alert properties**.
  
      Set the **Alert name** as `[Person].[Address] table has a specific city w/ extra NoOfEmployees values`.
  
      Set the **Alert description** as `The following conditions violated: $Data/Context/Property[@Name='Message']$ The number of employees in the [Person].[Address] table 'Kansas City' value is not equal to 1.`

      When you're finished configuring alert properties, select **Create**.

      ![Screenshot that shows configuring alerts for the third example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-3-configure-alerts-step.png)

After the custom monitor is created and works, you can see how it changed its state and generated an alert. In our example, the monitor should switch to the critical state, since the resulting query returns a record in the `Person.Address` table alongside there are 2 employees for the `Kansas City` in the `Person.BusinessEntityAddress` table.

![Screenshot that shows alert properties for the third example.](./media/sql-server-custom-monitoring-management-pack/two-state-monitor-example-3-monitor-alert-properties.png)
