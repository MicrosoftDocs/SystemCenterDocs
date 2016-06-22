---
title: View and Analyze an OLAP Data Cube with Excel
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a3b43a0-d777-452a-987b-5f41f58e62d0
---
# View and Analyze an OLAP Data Cube with Excel
You can use the following procedure to view and analyze a Microsoft Online Analytical Processing \(OLAP\) data cube from System Center 2016 Technical Preview \- Service Manager with Microsoft Excel. You can also save your workbooks into an analysis library. Using the PivotTable field list, you can drag and drop fields from the cube into the workbook.

You must have Microsoft Excel 2007 or later installed on the computer running the Service Manager console in order to use the following procedure.

> [!NOTE]
> The first time you analyze a cube with Excel, it can take a few minutes to load.

### To view and analyze an OLAP data cube with Excel

1.  In the Service Manager console, click **Data Warehouse**, expand the **Data Warehouse** node, and then click **Cubes**.

2.  In the **Cubes** pane, select a cube name, and then under **Tasks**, click **Analyze Cube in Excel**. For example, select **SystemCenterWorkItemsCube** and analyze it.

3.  When the worksheet opens in Excel, you can drag and drop fields from the PivotTable Field List and create slicers and charts.

    1.  For example, if you want to see the total number of incidents currently open, expand **IncidentDimGroup**, and then select **Incidents Opened**.

    2.  You can add additional fields to generate a more complex analysis. For example, you can add computers from the **ComputerDim** dimension by selecting the **DisplayName** field to see the number of incidents that affect different computers.

4.  Optionally, you can save the workbook to a shared folder or other shared location, such as the analysis library .


