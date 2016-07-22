---
title: How to Configure Integration with IntelliTrace Historical Profiling in System Center 2012 SP1
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 93797b7b-44c1-442e-b055-1ab4c55dce9e
author:mgoedtel
manager:cfreemanwa
---
# How to Configure Integration with IntelliTrace Historical Profiling in System Center 2012 SP1
[!INCLUDE[sc2012sp1notetopic](../../om/manage/includes/sc2012sp1notetopic_md.md)]  
  
In [!INCLUDE[sc2012sp1_short](../../om/manage/includes/sc2012sp1_short_md.md)], [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] includes the IntelliTrace Profiling Management Pack. This management pack lets you capture historical snapshots \(traces\) directly from the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, and to automatically generate IntelliTrace snapshots from .NET Application Performance Monitoring \(APM\) exception events. These snapshots can help developers investigate problems by giving them visibility to application execution history without the developers needing access to the servers where the applications ran. Developers can use Microsoft Visual Studio&nbsp;2012 Ultimate to open the collected snapshots. For information about IntelliTrace for developers, see [Debug Your App by Recording Code Execution with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=275118)  
  
IntelliTrace Profiling Management Pack automatically deploys the necessary infrastructure, which is called the IntelliTrace Collector, to the designated servers. The collected snapshots are uploaded to a network file share and attached to [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] alerts. Snapshots are uploaded to the management server using the same secure [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] channel that agents use to communicate with the management servers. You can configure Team Foundation Server \(TFS\) synchronization so that the IntelliTrace snapshots will be automatically added or linked to TFS work items. For more information, see [How to Configure Integration with TFS in System Center 2012 SP1](../../om/manage/How-to-Configure-Integration-with-TFS-in-System-Center-2012-SP1.md).  
  
> [!CAUTION]  
> IntelliTrace snapshots contain application runtime data that might include personal and sensitive information. Review your company's privacy policies before you enable this feature.  
  
### To configure integration with IntelliTrace Historical Profiling  
  
1.  Import and configure the Alert Attachment Management Pack. This management pack links the collected IntelliTrace snapshots to [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] alerts. For more information, see [How to Configure File Attachments for Operations Manager Alerts in System Center 2012 SP1](../../om/manage/How-to-Configure-File-Attachments-for-Operations-Manager-Alerts-in-System-Center-2012-SP1.md).  
  
2.  If you want to synchronize IntelliTrace snapshots with TFS work items, import and configure the TFS Work Item Synchronization Management Pack. When snapshots are synchronized with work items, developers can receive IntelliTrace snapshots with TFS work items in Visual Studio. Additionally, developers can set work item state to **Awaiting Evidence** and use TFS to submit requests to capture IntelliTrace snapshots. For more information, see [How to Configure Integration with TFS in System Center 2012 SP1](../../om/manage/How-to-Configure-Integration-with-TFS-in-System-Center-2012-SP1.md).  
  
    > [!NOTE]  
    > You can use IntelliTrace snapshots without TFS integration. If you do so, the IntelliTrace snapshots are not attached to work items, but they are uploaded to the Alert Attachment network file share instead.  
  
3.  In the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, click the **Administration** button, click **Management Packs**, and then, in the **Tasks** pane, click **Import Management Packs**. In the Import Management Packs Wizard, click **Add**, and then click **Add from disk**. Import the following management packs from the ManagementPacks folder on the [!INCLUDE[sc2012sp1_short](../../om/manage/includes/sc2012sp1_short_md.md)][!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] installation media:  
  
    -   IntelliTrace Collector Deployment \(Microsoft.SystemCenter.IntelliTraceCollectorInstallation.mpb\)  
  
    -   IntelliTrace Profiling \(Microsoft.SystemCenter.IntelliTraceProfiling.mpb\)  
  
    Click **Install**, and then click **Close**.  
  
    > [!IMPORTANT]  
    > The IntelliTrace tasks are not available until you restart the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console.  
  
