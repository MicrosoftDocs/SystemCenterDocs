---
title: View and analyze an OLAP data cube with Excel
description: Explains how to view and analyze a Service Manager OLAP data cube with Excel.
manager: carmonm
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
ms.assetid: c8f51e1b-061e-4ec2-8a21-b0b17eb31aee
---

# View and analyze a Service Manager OLAP data cube with Excel

>Applies To: System Center 2016 - Service Manager

You can use the following procedure to view and analyze a Microsoft Online Analytical Processing \(OLAP\) data cube from System Center 2016 - Service Manager with Microsoft Excel. You can also save your workbooks into an analysis library. Using the PivotTable field list, you can drag and drop fields from the cube into the workbook. For more information about using Excel slicers, see [Creating and Using Excel Slicers](ops-creating-and-using-excel-slicers.md).  

 You must have Microsoft Excel 2007 or later installed on the computer running the Service Manager console in order to use the following procedure.  

> [!NOTE]  
>  The first time you analyze a cube with Excel, it can take a few minutes to load.  

### To view and analyze an OLAP data cube with Excel  

1.  In the Service Manager console, click **Data Warehouse**, expand the **Data Warehouse** node, and then click **Cubes**.  

2.  In the **Cubes** pane, select a cube name, and then under **Tasks**, click **Analyze Cube in Excel**. For example, select **SystemCenterWorkItemsCube** and analyze it.  

3.  When the worksheet opens in Excel, you can drag and drop fields from the PivotTable Field List and create slicers and charts.  

    -  For example, if you want to see the total number of incidents currently open, expand **IncidentDimGroup**, and then select **Incidents Opened**.  

    -  You can add additional fields to generate a more complex analysis. For example, you can add computers from the **ComputerDim** dimension by selecting the **DisplayName** field to see the number of incidents that affect different computers.  

4.  Optionally, you can save the workbook to a shared folder or other shared location, such as the analysis library. For more information about the analysis library, see [How to Use the Analysis Library](ops-how-to-use-the-analysis-library.md).  
