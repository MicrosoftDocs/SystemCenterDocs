---
title: How to View Orchestrator Data by Using PowerPivot
description: Describes how to use PowerPivot for Excel to analyze operations data in System Center 20106 - Orchestrator.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7707e8ac-d885-4453-b72f-14f208eaf531
author: cfreemanwa
ms.author: raynew
manager: carmonm
---

# How to View Orchestrator Data by Using PowerPivot

> Applies To: System Center 2016 - Orchestrator

You can use Microsoft PowerPivot for Microsoft Excel to create reports for System Center 2016 - Orchestrator. You configure PowerPivot to use the Orchestrator web service as a data feed, filter the Source Tables for the data you want to use, and import the tables into the PowerPivot worksheet. PowerPivot lets you create relationships between tables, and manipulate the data to fit your requirements. By using the PivotTable feature in PowerPivot, you can generate a report that uses any of the data contained within the PowerPivot workbook.  

## Connect the Orchestrator web service to PowerPivot for Excel  
You must install PowerPivot for Excel to enable the product.  

PowerPivot for Excel requires Excel 2010 \(64\-bit or 32\-bit\).  

### To install PowerPivot  

-  Follow the instructions found at [Install PowerPivot for Excel](https://go.microsoft.com/fwlink/p/?LinkID=184678).  

Use PowerPivot to configure a connection to Orchestrator web service. Orchestrator uses the Open Data Protocol \(OData\), which PowerPivot can consume.  

> [!NOTE]  
> The OData provider in PowerPivot does not support the data contained in the Runbook Diagram box. Attempts to add a Runbook Diagram table will fail.  

#### To create a connection to an Orchestrator feed  

1.  Open Excel.  
2.  Click the **PowerPivot** tab above the ribbon.  
3.  Click **PowerPivot Window** on the ribbon. A **PowerPivot for Excel** book opens.  
4.  Click **From Data Feeds** on the ribbon. A **Table Import Wizard** opens.  
5.  Enter the Orchestrator web service URL in the **Data Feed URL** box. The web service URL is on port 81 of the Orchestrator SQL Server. For example, http:\/\/orchestrator:81\/Orchestrator2016\/Orchestrator.svc.  
6.  Click **Test Connection**.  
7.  If the test connection is successful, click **OK** and proceed to the next step.  

    If the test connection fails, do the following:  

    1.  Click **OK**.  
    2.  Click **Advanced**. The **Advanced** dialog box opens.  
    3.  In the **Security** section, change **Integrated Security** to **Basic**.  
    4.  Change **Persist Security Info** to **True**.  
    5.  Enter your **User ID** and **Password** in the appropriate boxes.  
    6.  Click **Test Connection**.  
    7.  Click **OK** and click **OK**.  

8.  Click **Next**.  
9. Select the check boxes of the table or tables that you want to import.  
10. To filter columns, select a table, click **Preview & Filter**, clear any boxes to exclude, and then click **OK**.  
11. Click **Finish**. The data is imported.  
12. Click **Close**.  

## Create a Summary of Runbook Results  
The following procedure describes the steps to create a pivot table containing a list of all runbooks and the count of results, grouped by the runbook server that ran the runbook instance.  

> [!NOTE]  
> For this example, the orchestration database must contain results from at least one runbook for PowerPivot to import a table.  

### To create a connection to the data&nbsp;feed  

1.  Open Excel.  
2.  Click the **PowerPivot** tab above the ribbon.  
3.  Click **PowerPivot Window** on the ribbon. A **PowerPivot for Excel** book opens.  
4.  Click **From Data Feeds** on the ribbon. A **Table Import** wizard opens.  
5.  Enter the Orchestrator web service URL in the **Data Feed URL** box.  
6.  Click **Next**.  
7.  Select the check boxes of the **Runbooks**, **RunbookInstances**, and **RunbookServers** tables.  
8.  Click **Finish**. The data is imported.  
9. Click **Close**.  

### To create relationships in PowerPivot  

1.  In the **PowerPivot for Excel** window, select the **RunbookInstance** tab.  
2.  Right-click the header of the **RunbookId** column to select **Create Relationship**.  
3.  In the **Related Lookup Table** list, select **Runbooks**, and in the **Related Lookup Column** list, select **Id**, and then click **Create**.  
4.  Right-click the header of the **RunbookServerId** column to select **Create Relationship**.  
5.  In the **Related Lookup Table** list, select **RunbookServers**, and in the **Related Lookup Column** list, select **Id**, and then click **Create**.  

### To create a pivot table  

1.  In the **PowerPivot for Excel** window, click **PivotTable** on the ribbon, and select **PivotTable**.  
2.  In the **Create PivotTable** dialog box, select **New Worksheet**, and then click **OK**.  
3.  In the **PowerPivot Field List**, under **RunbookServers**, click and drag **Name** to the **Row Labels** box.  
4.  In the **PowerPivot Field List**, under **Runbooks**, click and drag **Name** to the **Row Labels** box.  
5.  In the **PowerPivot Field List**, under **RunbookInstances**, click and drag **Status** to the **Column Labels** box.  
6.  In the **PowerPivot Field List**, under **RunbookInstances**, click and drag **RunbookId** to the **Sum Values** box.  
7.  Right-click **RunbookId** to select **Summarize by**, and then click **Count**.  

You can now modify the default labels and format your table for presentation.  

For more information about the workflow of a runbook and an explanation of runbook jobs and runbook instances, see [Orchestrator Architecture](~/orchestrator/learn-about-orchestrator.md) in the [getting started with system center 2016 - orchestrator](../orch/get-started/get-started-with-orchestrator.md).  

For more information about PowerPivot for Excel, see [Introducing PowerPivot for Excel](https://go.microsoft.com/fwlink/p/?LinkID=187006).  

## Next steps 
[Administering System Center 2016 - Orchestrator](../orch/manage/administering-orchestrator.md)  
