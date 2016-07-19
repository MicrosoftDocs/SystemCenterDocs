---
title: How to Configure Integration with IntelliTrace Historical Profiling in System Center 2012 R2
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ee19be3f-cf58-458e-a92d-ce9edbfe573a
author:mgoedtel
manager:cfreemanwa
---
# How to Configure Integration with IntelliTrace Historical Profiling in System Center 2012 R2
[!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)] includes the IntelliTrace Profiling Management Pack. This management pack lets you capture historical snapshots \(traces\) directly from the [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] console, and to automatically generate IntelliTrace snapshots from .NET Application Performance Monitoring \(APM\) events. These snapshots can help developers investigate problems by giving them visibility to application execution history without the developers needing access to the servers where the applications ran. Developers can use Microsoft Visual Studio 2012 Ultimate or Microsoft Visual Studio 2013 Preview to open the collected snapshots. For information about IntelliTrace for developers, see [Debug Your App by Recording Code Execution with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=275118)  
  
IntelliTrace Profiling Management Pack in [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)] uses a built\-in feature of Microsoft Monitoring Agent \(MMA\) for collecting application historical snapshots \(traces\). The collected snapshots are uploaded to a network file share and attached to [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] alerts. Snapshots are uploaded to the management server using the same secure [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] channel that agents use to communicate with the management servers. You can configure Team Foundation Server \(TFS\) synchronization so that the IntelliTrace snapshots will be automatically added or linked to TFS work items. For more information, see [How to Configure Integration with TFS in System Center 2012 R2](../../om/manage/How-to-Configure-Integration-with-TFS-in-System-Center-2012-R2.md).  
  
> [!IMPORTANT]  
> In [!INCLUDE[sc2012sp1_short](../../om/manage/includes/sc2012sp1_short_md.md)][!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] IntelliTrace Collector was deployed to the monitored servers as a separate package by the IntelliTrace Collector Management Pack. If your [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] environment was upgraded from [!INCLUDE[sc2012sp1_short](../../om/manage/includes/sc2012sp1_short_md.md)] to [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] and you imported [!INCLUDE[sc2012sp1_short](../../om/manage/includes/sc2012sp1_short_md.md)] versions of the IntelliTrace management packs, to continue to collect IntelliTrace information, you must remove the IntelliTrace Collector Deployment Management Pack and update Alert Attachment Management Pack and IntelliTrace Profiling Management Pack with the versions included in [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)]. Additionally, you must upgrade the [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] agent to Microsoft Monitoring Agent on each monitored server where you want to collect historical snapshots or automatically generate IntelliTrace snapshots from APM events.  
  
> [!CAUTION]  
> IntelliTrace snapshots contain application runtime data that might include personal and sensitive information. Review your company’s privacy policies before you enable this feature.  
  
### To configure integration with IntelliTrace Historical Profiling  
  
1.  Import and configure the Alert Attachment Management Pack. This management pack links the collected IntelliTrace snapshots to [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] alerts. For more information, see [How to Configure File Attachments for Operations Manager Alerts in System Center 2012 R2](../../om/manage/How-to-Configure-File-Attachments-for-Operations-Manager-Alerts-in-System-Center-2012-R2.md).  
  
2.  If you want to synchronize IntelliTrace snapshots with TFS work items, import and configure the TFS Work Item Synchronization Management Pack. When snapshots are synchronized with work items, developers can receive IntelliTrace snapshots with TFS work items in Visual Studio. Additionally, developers can set work item state to **Awaiting Evidence** and use TFS to submit requests to capture IntelliTrace snapshots. For more information, see [How to Configure Integration with TFS in System Center 2012 R2](../../om/manage/How-to-Configure-Integration-with-TFS-in-System-Center-2012-R2.md).  
  
    > [!NOTE]  
    > You can use IntelliTrace snapshots without TFS integration. If you do so, the IntelliTrace snapshots are not attached to work items, but they are uploaded to the Alert Attachment network file share instead.  
  
3.  In the [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] console, click the **Administration** button, click **Management Packs**, and then, in the **Tasks** pane, click **Import Management Packs**. In the Import Management Packs Wizard, click **Add**, and then click **Add from disk**. Import IntelliTrace Profiling \(Microsoft.SystemCenter.IntelliTraceProfiling.mpb\) from the ManagementPacks folder on the [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)] installation media.  
  
    Click **Install**, and then click **Close**.  
  
    > [!IMPORTANT]  
    > The IntelliTrace tasks are not available until you restart the [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] console.  
  
