---
title: How to Build the Resolved Incidents Scorecard
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 81f18253-039e-40ad-b902-7dd15a8a4f2a
translation.priority.mt: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to Build the Resolved Incidents Scorecard
Before you can use a scorecard in a dashboard in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], you must create the scorecard. Use the following procedure to use a wizard to create an example scorecard called Resolved Incidents Scorecard. The wizard also creates key performance indicators \(KPIs\) from the SystemCenterWorkItemsCube data source.  
  
### To build the Resolved Incidents Scorecard  
  
1.  Open Dashboard Designer, connect to the server that hosts the DWASDataBase, and then select **Service Manager WorkItems Cube**. Or, if you have previously saved a designer workspace file that contains the connection information, open the file.  
  
2.  On the **Home** tab, click **Add Lists**. In the **Add Lists** box, click **PerformancePoint Content**, and then click **OK**.  
  
3.  To add a scorecard to the workspace, in the **Workspace Browser**, right\-click the **PerformancePoint Content** list, point to **New**, and then click **Scorecard**.  
  
4.  In the **Select a Scorecard Template** window, in the **Category** tree, ensure that **Microsoft** is selected. In the **Template** list, select **Analysis Services**, and then click **OK**.  
  
5.  In the Create an Analysis Services Scorecard Wizard, on the **Select a data source page**, select the **SystemCenterWorkItemsCube** data source, and then click **Next**.  
  
    > [!NOTE]  
    >  When you use the wizard to create a scorecard based on an Analysis Services data source, there are two options that enable the creation of KPIs. You can use the first option to create KPIs based on the measures of the cube. You can use the second option to import KPIs from the cube, if the cube contains KPIs.  
  
6.  On the **Select a KPI Source** page, select **Create KPIs from Analysis Services measures**, and then click **Next**.  
  
7.  On the **Select KPIs to Import** page, click **Add KPI** and then in the new row, type **Resolved Incidents KPI** for the name.  
  
8.  Select **Incidents Resolved Count** under **Actual**.  
  
9. Select **Increasing is Better** under **Band Method**.  
  
10. Select **Incidents Opened** under **Targets** and then click **Next**.  
  
11. On the **Add Measure Filters** page, click **Next**.  
  
12. On the **Add Member Columns** page, click **Next**.  
  
13. On the **Locations** page, click **Finish**.  
  
14. Notice that the KPI and scorecard are added to the workspace and that the scorecard opens in the design pane. In the **Workspace Browser**, modify the name of the new scorecard to **Resolved Incidents Scorecard**, and then press **Enter**.  
  
15. Save the information in **Designer Workspace**.  
  
## See Also  
 [Creating and Deploying Dashboards](../../../sm/manage/operate/Creating-and-Deploying-Dashboards.md)