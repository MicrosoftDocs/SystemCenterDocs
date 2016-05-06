---
title: Data Sources
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 81c5ec95-966d-440e-a431-398d7b8be96e
---
# Data Sources
Monitors and rules in [!INCLUDE[om12short](../Token/om12short_md.md)] each start with a *data source* which defines where it will get the data to evaluate or collect. The first decision to make when you are defining a rule or monitor is the data source that it will use. The most straightforward method to answer this question is to determine where the information is that you want to collect or that indicates the condition you want to detect.

For example, an application may create an event in the Windows Event Log when a particular error occurs. You could create a rule that watches for this particular event and generates an alert when it detects one. If detection of the event is not possible through an event, a log, or a performance counter, then you may need to run a script on a periodic basis to retrieve the required information.

The same set of data sources is available for both monitors and rules as shown in the table below.

[Event Monitors and Rules](../Topic/Event-Monitors-and-Rules.md)

|Data Source|Description|
|---------------|---------------|
|[Windows Events](../Topic/Windows-Events.md)|Events in the Windows event log matching specified criteria.|
|[Text Logs](../Topic/Text-Logs.md)|Text log file that has a single line per entry.|
|[WMI Events](../Topic/WMI-Events.md)|Events created by Windows Management Instrumentation \(WMI\).|
|[SNMP Events](../Topic/SNMP-Events.md)|Traps sent from an SNMP device.|
|[Syslog Events](../Topic/Syslog-Events.md)|Events from Unix systems and other devices.|

[Performance Monitors and Rules](../Topic/Performance-Monitors-and-Rules.md)

|Data Source|Description|
|---------------|---------------|
|[Windows Performance Collection Rules](../Topic/Windows-Performance-Collection-Rules.md)|Monitor a threshold or collect a performance value from Windows.|
|[WMI Performance](../Topic/WMI-Performance.md)|Monitor a threshold or collect a performance value from a WMI query.|

[Script Monitors and Rules](../Topic/Script-Monitors-and-Rules.md)

|Data Source|Description|
|---------------|---------------|
|[Script Monitors](../Topic/Script-Monitors.md)|Monitor a value from a script that runs on a schedule.|
|[Script Collection Rules](../Topic/Script-Collection-Rules.md)|Collect events or performance data from a script that runs on a schedule.|

