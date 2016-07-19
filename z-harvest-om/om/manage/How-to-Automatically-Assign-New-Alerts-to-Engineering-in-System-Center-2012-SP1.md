---
title: How to Automatically Assign New Alerts to Engineering in System Center 2012 SP1
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18037830-1797-40c1-945e-811718969977
author:mgoedtel
manager:cfreemanwa
---
# How to Automatically Assign New Alerts to Engineering in System Center 2012 SP1
[!INCLUDE[sc2012sp1notetopic](../../om/manage/includes/sc2012sp1notetopic_md.md)]  
  
Through Team Foundation Server \(TFS\) synchronization, you can establish automatic work item routing for alerts that are raised in [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] in [!INCLUDE[sc2012sp1_long](../../om/manage/includes/sc2012sp1_long_md.md)]. This can be helpful if your information technology \(IT\) department uses TFS or if your process model requires that all application alerts must be tracked in TFS. Additionally, you can specify which alert resolution states that are defined in [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] will automatically create work items in TFS.  
  
### To route alerts to TFS automatically  
  
1.  In the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, click **Authoring**, expand **Management Pack Objects**, and then click **Rules**.  
  
2.  To set the scope of displayed rules, click **Scope**, click **View all targets**, locate and select **TFS Connector**, and then click **OK**.  
  
3.  In the list of scoped rules, right\-click **TFS Work Items Creation Rule**, click **Overrides**, click **Override the Rule**, and then click **For all objects of class: TFS Connector**.  
  
4.  Add an override for the parameter **Assign To Engineering State Codes** and set its value to a semicolon\-separated list of alert resolution states that route to TFS automatically. For example, to automatically create TFS work items for all new alerts \(state 0\) and alerts Assigned to Engineering \(state 248\), in the override value, enter **0;248**.  
  
    > [!NOTE]  
    > Even though each alert is created as new, you must still list other resolution states that need to route to TFS. This is necessary because an alert can be assigned to engineering in the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console before the synchronization workflow has created the work item in TFS.  
  
    In [!INCLUDE[sc2012sp1_short](../../om/manage/includes/sc2012sp1_short_md.md)], [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] has the predefined alert resolution states that are described in the following table.  
  
    |Alert resolution state|Resolution state ID|Description|  
    |--------------------------|-----------------------|---------------|  
    |New|0|New alert|  
    |Awaiting Evidence|247|A developer requested additional information from IT operations. With TFS synchronization turned on, this resolution state indicates that the developer has put the Operational Issue work item on hold while waiting for more information. Check the alert history for a Resolution Note from the developer.|  
    |Assigned to Engineering|248|The alert is being reviewed by developers. With TFS synchronization turned on, this resolution state initiates the creation of a new Operational Issue work item in TFS.|  
    |Acknowledged|249|A developer has received and accepted the Operational Issue work item for this alert. With TFS synchronization turned on, the Alert Owner field shows the current developer to whom the work item is assigned.|  
    |Scheduled|250|A fix is scheduled for the problem.|  
    |Resolved|254|A problem is resolved from a development perspective. With TFS synchronization turned on, this resolution state indicates that the associated Operational Issue work item is either resolved or closed. The alert might still be generated until the updated code is deployed to the operational environment.|  
    |Closed|255|The alert is closed.|  
  
    > [!NOTE]  
    > You can define your own alert resolution states in the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console Administration pane.  
  
5.  Save the settings to a management pack.  
  
