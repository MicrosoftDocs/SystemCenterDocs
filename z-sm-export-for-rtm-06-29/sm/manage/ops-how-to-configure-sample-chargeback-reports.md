---
title: How to Configure Sample Chargeback Reports
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d0f6ff4-b4b6-4edb-af2a-8d9a2fa19563
 

















---
# How to Configure Sample Chargeback Reports
You can use the following procedure to configure the sample Microsoft Excel chargeback report \(ChargebackReport.xlsx\) that is included with System Center 2012 - Service Manager Service Pack&nbsp;1. This sample report is designed for you to modify for use in your organization. You can update the report any way you like. The sample report contains the following tabs:  
  
-   Dashboard - This tab shows a chart of the top 3 cost centers, clouds, VMM user roles, price sheets, spending trend, and overall spending for the period that you select.  
  
-   Chargeback Daily Details - This tab shows a comprehensive list of daily costs detailing virtual machine cloud level and other costs assigned to price sheets for the year and month you select. It also includes a graph showing the top 3 clouds within cost centers.  
  
-   Chargeback Monthly Details - This tab shows a comprehensive list of costs assigned to price sheets for the year and month you select.  
  
> [!NOTE]  
>  The first time you open the file in with Excel, you must configure the workbook data connection so that it can retrieve information from OLAP data cubes in the Service Manager data warehouse management server.  
  
### To configure the sample workbook connection  
  
1.  Using Windows Explorer, navigate to the Service Manager installation folder and then open the Chargeback child folder.  
  
2.  Open the ChargebackReport.xlsx file, click the **Data** tab, and then click **Connections**.  
  
3.  In the **Workbook Connections** dialog box, for each connection, view its **Properties** and replace \<LocalHost\> with the server name of your Service Manager data warehouse management server. If your data warehouse analysis database name is not DWASDataBase, then replace the database name with the one that you use.  
  
4.  Optionally, you can save the workbook to a shared folder or other shared location, such as the analysis library. For more information about the analysis library, see [How to Use the Analysis Library](../../../sm/manage/operate/How-to-Use-the-Analysis-Library.md).  
  
## See Also  
 [How to Use the Analysis Library](../../../sm/manage/operate/How-to-Use-the-Analysis-Library.md)
