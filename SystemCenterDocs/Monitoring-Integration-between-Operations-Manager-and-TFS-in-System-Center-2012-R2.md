---
title: Monitoring Integration between Operations Manager and TFS in System Center 2012 R2
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 62830d85-e3a8-4943-a92f-848da71962f7
---
# Monitoring Integration between Operations Manager and TFS in System Center 2012 R2
Synchronization between [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] and Team Foundation Server \(TFS\) makes efficient communication possible between information technology \(IT\) operations and developers. A healthy TFS environment is essential for all development processes. Depending on your environment, you can import TFS monitoring and management packs that give you real\-time visibility into the health of the TFS developer environment.

The TFS Work Item Synchronization management pack synchronizes [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] alerts and TFS work items. Additionally, it monitors the synchronization infrastructure, and it generates alerts when synchronization fails. However, to monitor the complete TFS infrastructure, you need additional monitoring packs that alert you about a wide range of problems with TFS components. When you import the TFS Work Item Synchronization management pack, it is a best practice to also import and configure these monitoring packs. Together, they help you make sure that you are monitoring the complete health of the developer TFS environment.

## Management and Monitoring Packs to Use with TFS Integration
Use the management packs and monitoring packs in the following table for TFS integration.

|Management Pack|Description|Use with …|Where to get it|
|-------------------|---------------|--------------|-------------------|
|[Microsoft Visual Studio 2010 Team Foundation Server Monitoring Management Pack for Microsoft System Center](http://go.microsoft.com/fwlink/?LinkId=272647)|Monitors TFS infrastructure. Provides both proactive and reactive monitoring of Microsoft Team Foundation Server 2010. Monitors TFS components, such as application tier server instances, team project collections, build servers, and proxy servers.|-   Microsoft Team Foundation Server 2010<br />-   [!INCLUDE[om2007r2short](../Token/om2007r2short_md.md)]<br />-   [!INCLUDE[om12long](../Token/om12long_md.md)]<br />-   [!INCLUDE[om12short](../Token/om12short_md.md)] in [!INCLUDE[sc2012sp1_long](../Token/sc2012sp1_long_md.md)]|Microsoft Download Center|
|[Microsoft Visual Studio 2012 Team Foundation Server Monitoring Management Pack for Microsoft System Center](http://go.microsoft.com/fwlink/?LinkId=272663)|Monitors TFS infrastructure. Provides both proactive and reactive monitoring of Microsoft Team Foundation Server 2012. Monitors TFS components, such as application tier server instances, team project collections, build servers, and proxy servers.|-   Microsoft Team Foundation Server 2012<br />-   [!INCLUDE[om2007r2short](../Token/om2007r2short_md.md)]<br />-   [!INCLUDE[om12long](../Token/om12long_md.md)]<br />-   [!INCLUDE[om12short](../Token/om12short_md.md)] in [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)]<br />-   [!INCLUDE[omblue_1](../Token/omblue_1_md.md)]|Microsoft Download Center|
|[System Center Management Pack for Microsoft Visual Studio Team Foundation Server 2010 Work Item Synchronization](http://go.microsoft.com/fwlink/?LinkId=271476)|Provides synchronization with Microsoft Team Foundation Server 2010. Monitors its own synchronization infrastructure only. Use this if you are running [!INCLUDE[om12long](../Token/om12long_md.md)] without SP1.|-   Microsoft Team Foundation Server 2010<br />-   [!INCLUDE[om12long](../Token/om12long_md.md)]<br />-   [!INCLUDE[om12short](../Token/om12short_md.md)] in [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)]<br />-   [!INCLUDE[omblue_1](../Token/omblue_1_md.md)]|Microsoft Download Center|
|Team Foundation Server Work Item Synchronization Management Pack|Provides synchronization with Microsoft Team Foundation Server 2010 and Microsoft Team Foundation Server 2012. Monitors its own synchronization infrastructure only.|-   Microsoft Team Foundation Server 2010<br />-   Microsoft Team Foundation Server 2012<br />-   [!INCLUDE[om12short](../Token/om12short_md.md)] in [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)]<br />-   [!INCLUDE[omblue_1](../Token/omblue_1_md.md)]|-   [!INCLUDE[om12short](../Token/om12short_md.md)] in [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] media<br />-   [!INCLUDE[omblue_1](../Token/omblue_1_md.md)] media|

> [!NOTE]
> If your environment contains TFS 2010 and TFS 2012, you can use both monitoring packs together \(Microsoft Visual Studio 2010 Team Foundation Server Monitoring Management Pack for Microsoft System Center and Microsoft Visual Studio 2012 Team Foundation Server Monitoring Management Pack for Microsoft System Center\). Also, you can use these management packs without enabling synchronization between [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] alerts and TFS work items to get visibility into the health of the TFS environment.

## See Also
[How to Configure Integration with TFS in System Center 2012 R2](../Topic/How-to-Configure-Integration-with-TFS-in-System-Center-2012-R2.md)

