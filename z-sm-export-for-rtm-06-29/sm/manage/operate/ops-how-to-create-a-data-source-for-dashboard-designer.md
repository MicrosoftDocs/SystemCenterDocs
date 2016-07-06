---
title: How to Create a Data Source for Dashboard Designer
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 80eae04f-925d-4d3f-8460-1957309e3de5
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
# How to Create a Data Source for Dashboard Designer
You can use the following information to create a new data source in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] and save it by using Dashboard Designer.  
  
 The workspace is an XML document that defines the PerformancePoint item definitions for a particular project. The saved workspace items are stored in SharePoint lists and libraries. You can add existing stored items to a workspace, based on the project requirements.  
  
### To create a data source for Dashboard Designer  
  
1.  Open PerformancePoint Dashboard Designer, and in the **Workspace Browser**, select **Data Connections**.  
  
2.  Click the **Create** tab, and then click **Data Source**.  
  
3.  In the **Select a Data Source Template** dialog box, select **Analysis Services**, and then click **OK**.  
  
4.  In the **New Data Source** pane, ensure that the **Editor** tab is selected, and then type information for the connection settings for the data source using the examples in the following table.  
  
    |Property|Value|  
    |--------------|-----------|  
    |Server|\<YourServerName\>|  
    |Database|DWASDataBase|  
    |Cube|ServiceManager WorkItems Cube|  
  
5.  To save the data source, in the **Workspace Browser** pane, right\-click the new data source, and then click **Save**. As an option, you can rename the data source.  
  
6.  To save the workspace, click **Save As**, and save the Dashboard Designer Workspace in the folder that you want.  
  
## See Also  
 [Creating and Deploying Dashboards](../../../sm/manage/operate/Creating-and-Deploying-Dashboards.md)