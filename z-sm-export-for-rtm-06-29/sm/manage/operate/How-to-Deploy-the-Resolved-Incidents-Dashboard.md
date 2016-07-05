---
title: How to Deploy the Resolved Incidents Dashboard
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7c082c5-e63a-4542-8604-d4c5d01454f7
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
# How to Deploy the Resolved Incidents Dashboard
Use the following procedure to deploy the Resolved Incidents Dashboard to the SharePoint Dashboards library.  
  
 In this procedure you deploy the Resolved Incidents Dashboard to the SharePoint Dashboards library using the selected master page. Each dashboard is published as a folder that consists of a web page for each page in the dashboard.  
  
 After you deploy the dashboard, you can select values in the Resolved Incidents Scorecard to show information that applies only to that classification. For example, if you select an E\-Mail Problems value, only incidents with the E\-Mail Problems classification appear in the scorecard portion of the report.  
  
### To deploy the Resolved Incidents Dashboard  
  
1.  Open Dashboard Designer, connect to the server that hosts the DWASDataBase, and then select **Service Manager WorkItems Cube**. Or, if you have previously saved a designer workspace file that contains the connection information, open that file.  
  
2.  In the Workspace Browser, right\-click the **Resolved Incidents Dashboard**, and then select **Deploy to SharePoint**.  
  
3.  In the **Deploy To** dialog box, notice the selection of the Dashboards library.  
  
4.  In the **Master Page** list, select **Minimal**, and then click **OK**.  
  
5.  Internet Explorer starts and opens the first dashboard page.  
  
## See Also  
 [Creating and Deploying Dashboards](../../../sm/manage/operate/Creating-and-Deploying-Dashboards.md)