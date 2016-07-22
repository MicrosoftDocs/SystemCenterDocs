---
title: How to Create the Resolved Incidents Dashboard
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 200f0b9f-be5c-4458-b9aa-511caf4fa2d3


















---
# How to Create the Resolved Incidents Dashboard
Use the following procedure to create and assemble the Resolved Incidents Dashboard. This involves the Resolved Incidents Scorecard and the Incidents by Analyst report. You will then create connections to pass values between the dashboard items.  
  
### To create the Resolved Incidents Dashboard  
  
1.  Open Dashboard Designer, connect to the server that hosts the DWASDataBase, and then click **Service Manager WorkItems Cube**. Or, if you have previously saved a designer workspace file that contains the connection information, open that file.  
  
2.  In the **Select a Dashboard Page Template** window, select the **2 Columns** template, and then click **OK**.  
  
3.  In the **Workspace Browser**, modify the name of the dashboard to **Resolved Incidents Dashboard**, and then press **Enter**.  
  
4.  To add the **Resolved Incidents Scorecard** to the dashboard, in the **Details** pane, expand **Scorecards**, expand the **PerformancePoint Content** list, and then drag the **Resolved Incidents Scorecard** into the **Left Column** zone.  
  
5.  To add the Incidents by Analyst report to the dashboard, in the **Details** pane, expand **Reports**, expand the **PerformancePoint Content** list, and then drag the **Incidents by Analyst** report into the **Right Column** zone.  
  
6.  To create the connection between the scorecard and the report, in the **Right Column** zone, click **Incidents by Analyst**.  
  
7.  On the **Edit** ribbon tab, click **Create Connection**.  
  
8.  In the **Connection** dialog box, in the **Get Values From** list, select **Left Column - \(1\) Resolved Incidents Scorecard**.  
  
9. Click the **Values** tab, and in **Connect To**, select the **Incident Classification IncidentClassificationValue** hierarchy.  
  
10. In the **Source Value** list, select **Member Row: Member Unique Name**, and then click **OK**.  
  
11. Save the dashboard and the workspace.  
  
## See Also  
 [Creating and Deploying Dashboards](../../../sm/manage/operate/Creating-and-Deploying-Dashboards.md)