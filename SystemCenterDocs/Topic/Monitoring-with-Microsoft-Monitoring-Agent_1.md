---
title: Monitoring with Microsoft Monitoring Agent_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 53c9b72e-1e1a-48d4-84bd-7cef39cb1391
---
# Monitoring with Microsoft Monitoring Agent_1
Microsoft Monitoring Agent is a new agent that replaces the [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] Agent and combines .NET Application Performance Monitoring \(APM\) in System Center with the full functionality of IntelliTrace Collector in the Microsoft Visual Studio development system for gathering full application\-profiling traces. Microsoft Monitoring Agent can collect traces on demand or can be left running to monitor applications and collect traces. You can limit the disk space that the agent uses to store collected data. When the amount of data reaches the limit, the agent begins to overwrite the oldest data and store the latest data in its place.

You can use Microsoft Monitoring Agent together with [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] or as a stand\-alone tool for monitoring web applications that were written on the Microsoft .NET Framework. In both cases, you can direct the agent to save application traces in an IntelliTrace log format that can be opened in Microsoft Visual Studio Ultimate. The log contains detailed information about application failures and performance issues.

You can use Windows PowerShell commands to start and stop monitoring and collect IntelliTrace logs from web applications that are running on Internet Information Services \(IIS\). To open IntelliTrace logs that are generated from APM exceptions and APM performance events, you can use Visual Studio. For information about supported versions of IIS and Visual Studio, see [Microsoft Monitoring Agent Requirements and Compatibility](../Topic/Microsoft-Monitoring-Agent-Requirements-and-Compatibility.md).

## Monitoring with Microsoft Monitoring Agent Topics

-   [Microsoft Monitoring Agent Requirements and Compatibility](../Topic/Microsoft-Monitoring-Agent-Requirements-and-Compatibility.md)

-   [What's New and Support for Microsoft Monitoring Agent](assetId:///79ab2cd1-a598-4f3b-a3cb-afcdb2e1eaab)

-   [Installing Microsoft Monitoring Agent](../Topic/Installing-Microsoft-Monitoring-Agent.md)

-   [Monitoring Web Applications with Microsoft Monitoring Agent](../Topic/Monitoring-Web-Applications-with-Microsoft-Monitoring-Agent.md)

-   [Comparing Monitoring Approaches for .NET Applications](../Topic/Comparing-Monitoring-Approaches-for-.NET-Applications.md)

