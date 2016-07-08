---
title: How to Create the Incidents by Analyst Report
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0dc86873-059e-4afa-b1be-7d88d08c613e


















---
# How to Create the Incidents by Analyst Report
Use the following procedure to create an Analytic Grid report named Incidents by Analyst.  
  
### To create the Incidents by Analyst report  
  
1.  Open Dashboard Designer, connect to the server that hosts the DWASDataBase, and then click **Service Manager WorkItems Cube**. Or, if you have previously saved a designer workspace file that contains the connection information, open that file.  
  
2.  In the **Workspace Browser**, right\-click the **PerformancePoint Content** list, select **New**, and then click **Report**.  
  
3.  In the **Select a Report Template** dialog box, select the **Analytic Grid** template, and then click **OK**.  
  
4.  In the Create an Analytic Grid Report wizard, on the **Select a Data Source** page, select the **SystemCenterWorkItems** data source, and then click **Finish**.  
  
5.  In the **Workspace Browser**, modify the name of the report to **Incidents by Analyst**, and then press **Enter**.  
  
6.  To configure the report, in the **Details** pane, expand **Dimensions**, expand the **AssignedToUserDim** dimension, and then drag the **User Name** attribute into the **Rows** drop zone.  
  
7.  To configure the hierarchy member selection, in the **Rows** drop zone, click the down arrow to the right of the **AssignedToUserDim** hierarchy to open the **Select Members** dialog box.  
  
8.  In the **Select Members** dialog box, right\-click **All members** member, point to **Autoselect Members**, click **Select “User Name”**, and then click **OK**.  
  
9. In the **Details** pane, expand **Measures**, and then drag the **IncidentDimCount** and **Incidents Resolved Count** measures into the **Columns** drop zone.  
  
10. Right\-click the **Incidents Resolved Count** column heading, point to **Sort**, and then click **Smallest to Largest**.  
  
11. Right\-click anywhere in table, point to **Filter**, and then click **Filter Empty Rows**.  
  
12. In the **Details** pane, expand **Dimensions**, expand the **IncidentDim\_IncidentClassification** dimension, and then drag **IncidentClassificationValue** into the **Background** drop zone.  
  
13. On the **Edit** ribbon tab, in the **View** group, click **Settings**.  
  
14. In the **View Settings** window, click **Show Information Bar**, and then click **OK**.  
  
15. In the design pane, click the **Query** tab, and then review the MDX expression that was created automatically to support the report design.  
  
16. To save the report, in the **Workspace Browser**, right\-click the **Incidents by Analyst** report, and then click **Save**.  
  
## See Also  
 [Creating and Deploying Dashboards](../../../sm/manage/operate/Creating-and-Deploying-Dashboards.md)