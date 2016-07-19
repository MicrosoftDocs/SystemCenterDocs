---
title: How to Add Non-Service Manager Reports to the Report Catalog
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc180722-14a7-434f-9d28-f2629ee7f629


















---
# How to Add Non-Service Manager Reports to the Report Catalog
You can display SQL Server Reporting Services \(SSRS\) reports from any source using the Reporting workspace in the Service Manager console. The Reports workspace in System Center 2012 - Service Manager displays the folders and reports that are contained in the System Center\\Service Manager folder on the SSRS server. Therefore, you can add any reports that you want to the folder. For example, you might have a financial report that you want to view from the Reporting workspace.  
  
### To add a custom report to the report catalog  
  
1.  On the server that hosts SSRS, open Report Manager. For example, open http:\/\/\<ReportServerName:80\>\/Reports.  
  
2.  Navigate to the System Center\\ServiceManager reports folder, create a new folder, and give it a name. For example, name the folder **Financial Management**.  
  
3.  In the new folder, click **New Data Source**, and then add the data source of the new report.  
  
4.  Add the new report that uses the new data source.  
  
5.  Open the Service Manager console, select the **Reporting** workspace, and then navigate to the folder that contains the report.  
  
6.  In the **Tasks** pane, click **Run Report**.  
  
## See Also  
 [Using and Managing Standard Reports](../../../sm/manage/operate/Using-and-Managing-Standard-Reports.md)
