---
title: How to Synchronize Alerts with TFS in System Center 2012 SP1
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b52cd429-aed0-4c42-8f5d-31063665890c
author:mgoedtel
manager:cfreemanwa
---
# How to Synchronize Alerts with TFS in System Center 2012 SP1
[!INCLUDE[sc2012sp1notetopic](../../om/manage/includes/sc2012sp1notetopic_md.md)]  
  
In [!INCLUDE[sc2012sp1_short](../../om/manage/includes/sc2012sp1_short_md.md)], you can synchronize [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] alerts and Team Foundation Server \(TFS\) work items. When synchronization is enabled, IT operations can then assign alerts to the engineering team. Assigning an alert to engineering creates a new work item in TFS. The workflow will track and synchronize any changes that are made to TFS work items and any associated Operations Manager alerts. In order to synchronize alerts with TFS, you must first configure alert synchronization. For more information, see [How to Configure Integration with TFS in System Center 2012 SP1](../../om/manage/How-to-Configure-Integration-with-TFS-in-System-Center-2012-SP1.md).  
  
### To assign alerts to engineering  
  
1.  In the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, you can view all application problems that have been collected. To view alerts in [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)], in the navigation pane, click **Monitoring**, and then click **Active Alerts**.  
  
2.  To assign an alert to engineering, right\-click the alert, select **Set Resolution State**, and select **Assigned to Engineering**. This action creates a TFS work item and adds the TFS work item ID to the alert.  
  
3.  The system synchronizes all changes to the alert inside [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] and all changes to the work item in TFS.  
  
    > [!TIP]  
    > Any comments that you add to an [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] alert on the alert **History** tab are automatically added to the corresponding TFS work items. You can use this function to provide additional information to engineering.  
  
### To review alerts that are awaiting evidence from engineering  
  
1.  In the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, you can view all application problems that have been collected. To view alerts in [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)], in the navigation pane, click **Monitoring**, expand **Team Foundation Server Synchronization**, expand **Alerts**, and then click **Awaiting Evidence**.  
  
### To review and close alerts that have been resolved by engineering  
  
1.  In the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, you can view all application problems that have been collected. To view alerts in [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)], in the navigation pane, click **Monitoring**, expand **Team Foundation Server Synchronization**, expand **Alerts**, and then click **Resolved**.  
  
2.  When you want to close the resolved alerts, you can right\-click an alert, select **Set Resolution State**, and then set the resolution state to **Closed**.  
  
