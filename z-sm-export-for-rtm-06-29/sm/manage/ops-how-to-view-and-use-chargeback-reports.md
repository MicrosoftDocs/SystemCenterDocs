---
title: How to View and Use Chargeback Reports
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc590491-99dc-4147-8922-faefbe04bb97
 

















---
# How to View and Use Chargeback Reports
You can use the following procedure to view and analyze a Microsoft Online Analytical Processing \(OLAP\) data cube from System Center 2012 - Service Manager with Microsoft Excel. You can also save your workbooks into an analysis library. Using the PivotTable field list, you can drag and drop fields from the cube into the workbook. For more information about using Excel slicers, see [Creating and Using Excel Slicers](../../../sm/manage/operate/Creating-and-Using-Excel-Slicers.md).  
  
 You must have Excel, or a viewer capable of opening Excel data files, installed on the computer running the Service Manager console in order to use the following procedure.  
  
> [!NOTE]  
>  The first time you analyze a cube with Excel, it can take a few minutes to load.  
  
### To view and use chargeback report information in an OLAP data cube with Excel  
  
1.  In the Service Manager console, click **Data Warehouse**, expand the **Data Warehouse** node, and then click **Cubes**.  
  
2.  In the **Cubes** pane, select a cube name, and then under **Tasks**, click **Analyze Cube in Excel**. For example, select **SystemCenterServiceManagerChargebackCube** and analyze it.  
  
3.  When the worksheet opens in Excel, you can drag and drop fields from the PivotTable Field List and create slicers and charts.  
  
    1.  For example, if you want to see costs assigned to various cloud resources, expand **ServiceManagerInfraDailyChargeback**, and then select **Cloud Cost**.  
  
    2.  You can add additional fields to generate a more complex analysis. For example, you can add additional values from the **ServiceManagerInfraDailyChargeback** MeasureGroup by selecting the **VM Cost** and **VM Total Cost** to see the value of virtual machines in the clouds.  
  
4.  Optionally, you can save the workbook to a shared folder or other shared location, such as the analysis library. For more information about the analysis library, see [How to Use the Analysis Library](../../../sm/manage/operate/How-to-Use-the-Analysis-Library.md).  
  
## See Also  
 [Creating and Using Excel Slicers](../../../sm/manage/operate/Creating-and-Using-Excel-Slicers.md)   
 [How to Use the Analysis Library](../../../sm/manage/operate/How-to-Use-the-Analysis-Library.md)   
 [Using OLAP Cubes for Advanced Analytics](../../../sm/manage/operate/Using-OLAP-Cubes-for-Advanced-Analytics.md)
