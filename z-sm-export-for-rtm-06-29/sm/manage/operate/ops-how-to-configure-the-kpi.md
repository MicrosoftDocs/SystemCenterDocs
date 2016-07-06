---
title: How to Configure the KPI
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6440f22b-85ee-474f-be4c-573102d8c4b6
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
# How to Configure the KPI
Use the following procedures to configure the key performance indicators \(KPIs\) that you created in the [How to Build the Resolved Incidents Scorecard](../../../sm/manage/operate/How-to-Build-the-Resolved-Incidents-Scorecard.md) topic. You will later use this information in a PerformancePoint dashboard.  
  
 In the first procedure, you configure the Resolved Incidents KPI number formats and threshold values. In the second procedure, you configure the Resolved Incidents Scorecard and add the Incident Classification hierarchy to allow browsing of the KPI by the hierarchy members. In addition, you will format the scorecard. In the dashboard, the selection of members of the Incident Classification hierarchy will filter a report.  
  
### To configure the KPI  
  
1.  Using Dashboard Designer, open the file you saved previously that contains the Incident Resolved Scorecard.  
  
2.  In the **Workspace Browser**, click **Resolved Incidents KPI**.  
  
3.  To configure the thresholds for the Target metric, select the **Target** metric.  
  
4.  In the **Thresholds** section, modify the value for **Threshold 2** to **50%**, and the value for **Threshold 1** to **25%**.  
  
5.  In the Thresholds section, modify the value for **Best** to **100%**.  
  
6.  To save the KPI, in the **Workspace Browser**, right\-click **Resolved Incidents KPI**, and then click **Save**.  
  
### To configure the Resolved Incidents KPI  
  
1.  In the **Workspace Browser**, select the scorecard named **Resolved Incidents Scorecard**.  
  
2.  To refresh the scorecard with the updated KPI definition, on the **Edit** ribbon tab, inside the **View** group, click **Update**.  
  
3.  To add the Incident Classification hierarchy to the scorecard rows, in the **Details** pane, expand **Dimensions**, expand the **IncidentDim\_IncidentClassification** dimension, and then drag **IncidentClassificationValue** onto the **Incident** scorecard cell.  
  
4.  In the **Select Members** dialog box, expand the **All** member list, select all the values other than the empty value, and then click **OK**.  
  
5.  To refresh the scorecard, on the **Edit** ribbon tab, inside the **View** group, click **Update**.  
  
## See Also  
 [Creating and Deploying Dashboards](../../../sm/manage/operate/Creating-and-Deploying-Dashboards.md)