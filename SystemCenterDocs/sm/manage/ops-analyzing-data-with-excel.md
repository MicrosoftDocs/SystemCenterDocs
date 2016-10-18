---
title: Analyzing Data with Excel
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57102204-4876-4a97-9da4-ef6dac619721
---

# Analyzing Data with Excel

>Applies To: System Center 2016 - Service Manager

Service Manager includes predefined Microsoft Online Analytical Processing \(OLAP\) data cubes that connect to the data warehouse to retrieve data so that you can manipulate it by using Microsoft Excel in a tabular fashion. When it is opened, a data cube is presented as a worksheet containing a blank PivotTable report. Information defining the OLAP data source is embedded in a worksheet. When you open a report or when you refresh the data connection, Excel uses Microsoft SQL&nbsp;Server Analysis Services \(SSAS\) to connect to the data warehouse to retrieve key performance indicators \(KPIs\) and other data. After it is opened, the current worksheet contains a snapshot or subset of data from the data warehouse. If you save a worksheet, the data source connection information, KPIs, and any other customizations you have made are saved with it. If you save the worksheet to an analysis library, you can later reopen it without having to use the Service Manager console.  

 KPIs included in Service Manager data cubes are predefined, special, calculated measures that are defined on the server that make it possible for you to track KPIs, such as status \(does the current value meet a specific number?\) and trend \(what is the value over time?\). When these KPIs are displayed in a PivotTable, the server can send related icons that are similar to the new Excel icon set to indicate status levels that are above or below a certain threshold \(for example, with a stop light icon\) or whether a value is trending up or down \(for example, with a directional arrow icon\).  

 PivotTables can help you quickly and easily create useful reports. PivotTables that appear in Service Manager data cubes include many predefined KPI categories, called measure groups or dimensions. These groups are the highest level of categorization, and they help you examine the data and focus your analysis. In turn, most measure groups have many additional levels of subcategories and individual fields. All the categories, subcategories, and fields are contained in the PivotTable Field List. For example, you can create a straightforward report using the following steps:  

1.  Using the PivotTable Field List, select a category and add it as a row.  

2.  Select a second category and add it as a column.  

3.  Select a category or subcategory to add values.  

 After you have created your report, you can add any level of additional complexity by sorting, filtering, formatting, and adding calculations and charts. You can also go in and out of categories as you continue your analysis.  

 To view a demonstration of creating a report and manipulating data in Excel using data from an OLAP data cube in a PivotTable, see [Drill into PivotTable data](https://support.office.com/en-US/article/Drill-into-PivotTable-data-C1B11240-FC8F-4FDD-A697-629BF6F7EE0B).  
