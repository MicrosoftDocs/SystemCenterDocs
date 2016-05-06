---
title: Integrating Operations Manager with Development Processes in System Center 2012 SP1
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8883365d-aec3-4cd4-a40a-46316488e2b7
---
# Integrating Operations Manager with Development Processes in System Center 2012 SP1
Streamlining the communications between development and information technology \(IT\) operations teams \(often called DevOps\) can help you decrease the time it takes for application maintenance and delivery into production, where your application delivers value to customers. To speed interactions between these teams, it is essential to quickly detect and fix problems that might need assistance from the engineering team.

The topics in this section can help you integrate [!INCLUDE[om12long](../Token/om12long_md.md)] with development tools, such as Team Foundation Server \(TFS\) and Visual Studio. This integration enables deep troubleshooting and provides greater efficiency between development and IT operations teams.

## Integrating Operations Manager with Development Processes \(DevOps\) Topics

-   [How to Configure Integration with TFS in System Center 2012 SP1](../Topic/How-to-Configure-Integration-with-TFS-in-System-Center-2012-SP1.md)

    You can synchronize [!INCLUDE[om12long](../Token/om12long_md.md)] alerts and TFS work items. When synchronization is enabled, IT operations can assign alerts to the engineering team.

-   [How to Configure File Attachments for Operations Manager Alerts in System Center 2012 SP1](../Topic/How-to-Configure-File-Attachments-for-Operations-Manager-Alerts-in-System-Center-2012-SP1.md)

    You will need to configure file attachments for [!INCLUDE[om12short](../Token/om12short_md.md)] alerts. Proper configuration enables integration with TFS, IntelliTrace Historical Profiling, sharing Application Performance Monitoring events with developers, Global Service Monitor web tests, and any other scenarios that require files to be associated with [!INCLUDE[om12short](../Token/om12short_md.md)] alerts.

-   [How to Synchronize Alerts with TFS in System Center 2012 SP1](../Topic/How-to-Synchronize-Alerts-with-TFS-in-System-Center-2012-SP1.md)

    TFS lets you configure engineering process templates. [!INCLUDE[om12short](../Token/om12short_md.md)] integration with TFS introduces a new "Operational Issue" work item type definition that can be embedded into any of your organization’s engineering processes.

-   [How to Configure Integration with IntelliTrace Historical Profiling in System Center 2012 SP1](../Topic/How-to-Configure-Integration-with-IntelliTrace-Historical-Profiling-in-System-Center-2012-SP1.md)

    You can help developers to debug applications by collecting IntelliTrace snapshots directly from [!INCLUDE[om12short](../Token/om12short_md.md)]. When TFS and [!INCLUDE[om12short](../Token/om12short_md.md)] are integrated, these snapshots can be automatically attached to TFS work items.

-   [How to Collect IntelliTrace Historical Profiling Traces from System Center 2012 SP1](../Topic/How-to-Collect-IntelliTrace-Historical-Profiling-Traces-from-System-Center-2012-SP1.md)

    After configuring integration with IntelliTrace, you can collect and share IntelliTrace snapshots with developers.

-   [Monitoring Integration between Operations Manager and TFS in System Center 2012 SP1](../Topic/Monitoring-Integration-between-Operations-Manager-and-TFS-in-System-Center-2012-SP1.md)

    Depending on your environment, you can import TFS monitoring and management packs that give you real\-time visibility into the health of the TFS developer environment.

-   [Integrating Operations Manager with Non-English Versions of Team Foundation Server &#40;TFS&#41; or a Customized Process Model in TFS](../Topic/Integrating-Operations-Manager-with-Non-English-Versions-of-Team-Foundation-Server--TFS--or-a-Customized-Process-Model-in-TFS.md)

    When you need to synchronize Operations Manager alerts and TFS work items, and your development team is using a non\-English process template in TFS \(included in non\-English versions of TFS\), you must configure Operations Manager so that it can synchronize alerts with TFS work items.

