---
title: View Orchestrator data with PowerPivot
description: Describes how to use PowerPivot for Excel to analyze operations data in System Center - Orchestrator.
ms.date: 04/09/2025
ms.update-cycle: 1095-days
ms.service: system-center
ms.subservice: orchestrator
ms.topic: how-to
author: jyothisuri
ms.author: jsuri
ms.custom: UpdateFrequency3, engagement-fy24
---

# View Orchestrator data using PowerPivot

You can use Microsoft PowerPivot for Microsoft Excel to create reports for System Center - Orchestrator. You configure PowerPivot to use the Orchestrator web service as a data feed, filter the Source Tables for the data you want to use, and import the tables into the PowerPivot worksheet. PowerPivot lets you create relationships between tables, and manipulate the data to fit your requirements. By using the PivotTable feature in PowerPivot, you can generate a report that uses any of the data contained within the PowerPivot workbook.  

## Install PowerPivot  

You must install PowerPivot for Excel to enable the product. [Learn more](/previous-versions/sql/sql-server-2012/gg413462(v=sql.110)).  

## Create a connection to an Orchestrator feed  

Use PowerPivot to configure a connection to Orchestrator web service. Orchestrator uses the Open Data Protocol \(OData\), which PowerPivot can consume.  

> [!NOTE]  
> The OData provider in PowerPivot does not support the data contained in the Runbook Diagram box. Attempts to add a Runbook Diagram table will fail.  

To create a connection to an Orchestrator feed, follow these steps:

1. Open Excel.  
2. Select the **PowerPivot** tab above the ribbon.  
3. Select **PowerPivot Window** on the ribbon. A **PowerPivot for Excel** book opens.  
4. Select **From Data Feeds** on the ribbon. A **Table Import Wizard** opens.  
5. Enter the Orchestrator web service URL in the **Data Feed URL** box. The web service URL is on port 81 of the Orchestrator SQL Server. For example, http:\/\/orchestrator:81\/Orchestrator2016\/Orchestrator.svc.  
6. Select **Test Connection**.  
7. If the test connection is successful, select **OK** and proceed to the next step.  

    If the test connection fails, do the following:  

    1. Selectlick **OK**.  
    2. Select **Advanced**. The **Advanced** dialog box opens.  
    3. In the **Security** section, change **Integrated Security** to **Basic**.  
    4. Change **Persist Security Info** to **True**.  
    5. Enter your **User ID** and **Password** in the appropriate boxes.  
    6. Select **Test Connection**.  
    7. Select **OK** and select **OK**.  

8. Select **Next**.  
9. Select the check boxes of the table or tables that you want to import.  
10. To filter columns, select a table, select **Preview & Filter**, clear any boxes to exclude, and then select **OK**.  
11. Select **Finish**. The data is imported.  
12. Select **Close**.  

## Create a summary of runbook results

The following procedure describes the steps to create a pivot table containing a list of all runbooks and the count of results, grouped by the runbook server that ran the runbook instance.  

> [!NOTE]  
> For this example, the orchestration database must contain results from at least one runbook for PowerPivot to import a table.  

## Create a connection to the data&nbsp;feed  

To create a connection to the data&nbsp;feed, follow these steps:

1. Open Excel.  
2. Select the **PowerPivot** tab above the ribbon.  
3. Select **PowerPivot Window** on the ribbon. A **PowerPivot for Excel** book opens.  
4. Select **From Data Feeds** on the ribbon. A **Table Import** wizard opens.  
5. Enter the Orchestrator web service URL in the **Data Feed URL** box.  
6. Select **Next**.  
7. Select the check boxes of the **Runbooks**, **RunbookInstances**, and **RunbookServers** tables.  
8. Select **Finish**. The data is imported.  
9. Select **Close**.  

## Create relationships in PowerPivot  

To create relationships in PowerPivot, follow these steps:

1. In the **PowerPivot for Excel** window, select the **RunbookInstance** tab.  
2. Right-click the header of the **RunbookId** column to select **Create Relationship**.  
3. In the **Related Lookup Table** list, select **Runbooks**, and in the **Related Lookup Column** list, select **Id**, and then select **Create**.  
4. Right-click the header of the **RunbookServerId** column to select **Create Relationship**.  
5. In the **Related Lookup Table** list, select **RunbookServers**, and in the **Related Lookup Column** list, select **Id**, and then select **Create**.  

## Create a pivot table  

To create a pivot table, follow these steps:

1. In the **PowerPivot for Excel** window, select **PivotTable** on the ribbon, and select **PivotTable**.  
2. In the **Create PivotTable** dialog box, select **New Worksheet**, and then select **OK**.  
3. In the **PowerPivot Field List**, under **RunbookServers**, click and drag **Name** to the **Row Labels** box.  
4. In the **PowerPivot Field List**, under **Runbooks**, click and drag **Name** to the **Row Labels** box.  
5. In the **PowerPivot Field List**, under **RunbookInstances**, click and drag **Status** to the **Column Labels** box.  
6. In the **PowerPivot Field List**, under **RunbookInstances**, click and drag **RunbookId** to the **Sum Values** box.  
7. Right-click **RunbookId** to select **Summarize by**, and then select **Count**.  

You can now modify the default labels and format your table for presentation.  

- [Learn more ](learn-about-orchestrator.md) about the runbook workflows and jobs.
- [Learn more ](/previous-versions//ee835651(v=technet.10)) about PowerPivot for Excel.
