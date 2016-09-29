---
title: Managing Chargeback Reports in Service Manager
manager:  cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d96dba21-6e3d-4e81-86d6-f168605359a3
---

# Managing Chargeback Reports in Service Manager

>Applies To: System Center 2016 - Service Manager

This section provides an overview of how to view chargeback reports and how to configure the sample reports in Service Manager. Before you can use the reports they must be installed and configured for your installation of Service Manager. For more information, see [Installing and Configuring Chargeback Reports](admin-installing-and-configuring-chargeback-reports-in-system-center-2016-service-manager.md).  


## How to View and Use Chargeback Reports

You can use the following procedure to view and analyze a Microsoft Online Analytical Processing \(OLAP\) data cube from Service Manager with Microsoft Excel. You can also save your workbooks into an analysis library. Using the PivotTable field list, you can drag and drop fields from the cube into the workbook. For more information about using Excel slicers, see [Creating and Using Excel Slicers](ops-creating-and-using-excel-slicers.md).  

 You must have Excel, or a viewer capable of opening Excel data files, installed on the computer running the Service Manager console in order to use the following procedure.  

> [!NOTE]  
>  The first time you analyze a cube with Excel, it can take a few minutes to load.  

### To view and use chargeback report information in an OLAP data cube with Excel  

1.  In the Service Manager console, click **Data Warehouse**, expand the **Data Warehouse** node, and then click **Cubes**.  

2.  In the **Cubes** pane, select a cube name, and then under **Tasks**, click **Analyze Cube in Excel**. For example, select **SystemCenterServiceManagerChargebackCube** and analyze it.  

3.  When the worksheet opens in Excel, you can drag and drop fields from the PivotTable Field List and create slicers and charts.  

    1.  For example, if you want to see costs assigned to various cloud resources, expand **ServiceManagerInfraDailyChargeback**, and then select **Cloud Cost**.  

    2.  You can add additional fields to generate a more complex analysis. For example, you can add additional values from the **ServiceManagerInfraDailyChargeback** MeasureGroup by selecting the **VM Cost** and **VM Total Cost** to see the value of virtual machines in the clouds.  

4.  Optionally, you can save the workbook to a shared folder or other shared location, such as the analysis library. For more information about the analysis library, see [How to Use the Analysis Library](ops-how-to-use-the-analysis-library.md).  

## How to Configure Sample Chargeback Reports

You can use the following procedure to configure the sample Microsoft Excel chargeback report \(ChargebackReport.xlsx\) that is included with Service Manager. This sample report is designed for you to modify for use in your organization. You can update the report any way you like. The sample report contains the following tabs:  

-   Dashboard - This tab shows a chart of the top 3 cost centers, clouds, VMM user roles, price sheets, spending trend, and overall spending for the period that you select.  

-   Chargeback Daily Details - This tab shows a comprehensive list of daily costs detailing virtual machine cloud level and other costs assigned to price sheets for the year and month you select. It also includes a graph showing the top 3 clouds within cost centers.  

-   Chargeback Monthly Details - This tab shows a comprehensive list of costs assigned to price sheets for the year and month you select.  

> [!NOTE]  
>  The first time you open the file in with Excel, you must configure the workbook data connection so that it can retrieve information from OLAP data cubes in the Service Manager data warehouse management server.  

### To configure the sample workbook connection  

1.  Using Windows Explorer, navigate to the Service Manager installation folder and then open the Chargeback child folder.  

2.  Open the ChargebackReport.xlsx file, click the **Data** tab, and then click **Connections**.  

3.  In the **Workbook Connections** dialog box, for each connection, view its **Properties** and replace &lt;LocalHost&gt; with the server name of your Service Manager data warehouse management server. If your data warehouse analysis database name is not DWASDataBase, then replace the database name with the one that you use.  

4.  Optionally, you can save the workbook to a shared folder or other shared location, such as the analysis library. For more information about the analysis library, see [How to Use the Analysis Library](ops-how-to-use-the-analysis-library.md).  
