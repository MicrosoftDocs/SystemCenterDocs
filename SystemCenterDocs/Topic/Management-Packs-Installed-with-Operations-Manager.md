---
title: Management Packs Installed with Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13b9ecf3-5822-4f9d-97aa-b637e4fc68a3
---
# Management Packs Installed with Operations Manager
When you install Operations Manager, a component of System Center 2012, a number of management packs are installed as well. The following table describes the purposes of those management packs.

|Purpose|Associated management packs|
|-----------|-------------------------------|
|Core monitoring functionality|-   System Center Core Library<br />-   System Center Core Monitoring<br />-   System Center Core Monitoring Agent Management<br />-   System Center Internal Library<br />-   Microsoft System Center Operations Manager Library<br />-   Operations Manager Internal Library<br />-   Performance Library<br />-   Process Monitoring Library<br />-   Health Internal Library<br />-   Health Library<br />-   Default Management Pack<br />-   Baselining Tasks Library<br />-   System Center Operations Manager Infrastructure Monitoring<br />-   Instance Group Library<br />-   Process Monitoring Library<br />-   System Center Hardware Library<br />-   System Library<br />-   System Software Library<br />-   Windows Cluster Library<br />-   Windows Core Library<br />-   Windows Service Library<br />-   System Center Operations Manager Data Access Service Monitoring<br />-   System Center Rule Templates<br />-   System Center Task Templates<br />-   System Center UI Executed Tasks<br />-   System Center Workflow Foundation Library<br />-   System Virtualization Library<br />-   WS\-Management Library|
|Client monitoring, agentless exception monitoring \(AEM\), and Customer Experience Improvement Program \(CEIP\)|-   Client Monitoring Internal Library<br />-   Client Monitoring Library<br />-   Client Monitoring Overrides Management Pack<br />-   Client Monitoring Views Library|
|Application monitoring|-   Distributed Application Designer Library<br />-   Microsoft System Center Application Monitoring 360 Template Library<br />-   Operations Manager APM Infrastructure<br />-   Operations Manager APM Infrastructure Monitoring<br />-   Operations Manager APM Library<br />-   Operations Manager APM Library Resources \(enu\)<br />-   Operations Manager APM Reports Library<br />-   Operations Manager APM Wcf Library<br />-   Operations Manager APM Web<br />-   Operations Manager Application Monitoring Library<br />-   Web Application Availability Monitoring Library<br />-   Web Application Availability Monitoring Solutions Base Library<br />-   Web Application Availability Monitoring Solutions Library<br />-   Web Application Monitoring Library<br />-   System Application Log Library<br />-   Synthetic Transactions Library<br />-   Microsoft.SystemCenter.DataProviders.Library|
|Network monitoring|-   SNMP Library<br />-   Network Device Library<br />-   Network Discovery Internal<br />-   Network Management – Core Monitoring<br />-   Network Management Library<br />-   Network Management Reports<br />-   Network Management Templates|
|UNIX and Linux monitoring|-   UNIX\/Linux Core Library<br />-   UNIX\/Linux Core Console Library<br />-   UNIX View Library<br />-   UNIX Log File Template Library<br />-   Image Library \(UNIX\/Linux\)|
|Enabling views and consoles|-   Image Library \(System Center\)<br />-   Image Library \(System\)<br />-   Image Library \(UNIX\/Linux\)<br />-   Image Library \(Windows\)<br />-   Microsoft SystemCenter OperationsManager Summary Dashboard<br />-   Microsoft SystemCenter Visualization Network Dashboard<br />-   Microsoft System Center Visualization Network Library<br />-   Microsoft.SystemCenter.Visualization.Configuration.Library<br />-   Microsoft.SystemCenter.Visualization.Internal<br />-   Microsoft.SystemCenter.Visualization.Library<br />-   System Center Core Monitoring Views|
|Notifications|-   Notifications Internal Library<br />-   Notifications Library|
|Reporting|-   Data Warehouse Internal Library<br />-   Date Warehouse Library<br />-   Microsoft Data Warehouse Reports<br />-   Microsoft Generic Report Library<br />-   Microsoft ODR Report Library<br />-   Microsoft Service Level Report Library<br />-   Microsoft.SystemCenter.Reports.Deployment|
|Audit collection services \(ACS\)|-   Microsoft Audit Collection Services|

The following unsealed management packs are included in [!INCLUDE[om12short](../Token/om12short_md.md)]:

-   Client Monitoring Overrides Management Pack

-   Default Management Pack

-   Microsoft SystemCenter Virtualization Network Management Pack

-   Network Discovery Internal Management Pack

Do not save any settings, views, or overrides to these management packs. You should create your own local pack, which is an unsealed management pack in which to store your customizations. As a best practice, you should create a separate local pack for each sealed management pack you customize.

## See Also
[Creating a Management Pack for Overrides](../Topic/Creating-a-Management-Pack-for-Overrides.md)
[What Is in an Operations Manager Management Pack?](../Topic/What-Is-in-an-Operations-Manager-Management-Pack-.md)
[Management Pack Life Cycle](../Topic/Management-Pack-Life-Cycle.md)
[How to Import an Operations Manager Management Pack](../Topic/How-to-Import-an-Operations-Manager-Management-Pack.md)
[How to Remove an Operations Manager Management Pack](../Topic/How-to-Remove-an-Operations-Manager-Management-Pack.md)
[How to Export an Operations Manager Management Pack](../Topic/How-to-Export-an-Operations-Manager-Management-Pack.md)
[How to Add Knowledge to a Management Pack](../Topic/How-to-Add-Knowledge-to-a-Management-Pack.md)

