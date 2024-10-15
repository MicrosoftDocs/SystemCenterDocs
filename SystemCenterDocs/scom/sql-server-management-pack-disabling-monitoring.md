---
ms.assetid: cddb1bfe-0eff-4417-ab61-e0b2da55c5ed
title: Disabling monitoring of specified SQL Servers and databases in Management Pack for SQL Server
description: This section explains how to disable monitoring of SQL Servers and Databases
author: Anastas1ya
ms.author: v-fkornilov
manager: evansma
ms.date: 11/01/2024
ms.topic: article
ms.service: system-center
ms.subservice: operations-manager
---

# Disabling Monitoring of Specified SQL Servers and Databases

This section explains how to disable monitoring of SQL Servers and Databases.

## Disabling Monitoring of Specified SQL Server Versions

Management Pack for SQL Server allows you to exclude certain versions of SQL Server instances from monitoring.

To exclude versions that you don't want to monitor, override the **Versions of SQL Server to be excluded** parameter in the **MSSQL on Windows: Discover SQL Server Database Engines (Local)** discovery with the versions that you want to exclude. Use comma to specify multiple versions.

For example, an override "2014,2012" instructs the management pack to skip instances of SQL Server 2012 and 2014.

![Screenshot showing Disabling Monitoring of Specified SQL Server Versions.](./media/sql-server-management-pack/overriding-version-parameter.png)

## Disabling Monitoring of Specified SQL Server Editions

Management Pack for SQL Server allows you to exclude certain editions of SQL Server instances from monitoring.

To exclude editions that you don't want to monitor, override the **Editions of SQL Server to be excluded** parameter in the **MSSQL on Windows: Discover SQL Server Database Engines (Local)** discovery with the editions that you want to exclude. Use comma to specify multiple editions.

The following table lists short names that you can use to override the **Editions of SQL Server to be excluded** parameter.

|Short Name|Covered Editions|
|-|-|
|Enterprise|Enterprise Edition, Enterprise Edition: Core-based Licensing|
|Standard|Standard Edition, Business Intelligence Edition|
|Web|Web Edition|
|Developer|Developer Edition|
|Express|Express Edition, Express Edition with Advanced Services|
|Evaluation|Enterprise Evaluation Edition|

![Screenshot showing Disabling Monitoring of Specified SQL Server Editions.](./media/sql-server-management-pack/overriding-edition-parameter.png)

## Disabling Monitoring of Specified Databases by Name

You can disable discovery and monitoring of databases by specifying database names in the **Exclude list** parameter available in the following discoveries:

- MSSQL on Windows: Discover SQL Server Databases for a Database Engine

- MSSQL on Linux: Discover SQL Server Databases for a Database Engine

Use commas to separate database names and asterisks to replace one or more characters. For example, when setting the **Exclude list** parameter to dev*, \*test*, *stage, dbnotmon, the monitoring behavior would be as follows:

|DB Name|Monitored/Not monitored|
|-|-|
|dev|Not monitored|
|dev_sales|Not monitored|
|sales_dev|Monitored|
|test|Not monitored|
|test_sales|Not monitored|
|sales_test|Not monitored|
|stage|Not monitored|
|stage_dev|Monitored|
|dev_stage|Not monitored|
|dbnotmon|Not monitored|
|dbnotmon_sales|Monitored|
|sales_dbnotmon|Monitored|

If you've \* (asterisk) in the list as a database name (for example, \*temp*, \*, \*dev* or \*temp,*), it disables monitoring of any database.
