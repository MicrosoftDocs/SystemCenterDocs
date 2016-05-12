---
title: Event Monitors and Rules
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab45f9ef-bdb4-4590-a5c6-5a1a3d70ce9e
---
# Event Monitors and Rules
Event monitors and rules rely on the application they are monitoring to create an event of some kind in response to a problem or other interesting occurrence. The monitor or rule continuously watches the data source for an event matching specific criteria and immediately takes an appropriate response. The basic logic and configuration of event rules and monitors are similar except for the initial configuration of the data source that they are retrieving the event from.

## Types of Event Monitors and Rules
The table below lists the kinds of events that can be used for monitors and rules in an [!INCLUDE[om12short](Token/om12short_md.md)] management pack. Each is discussed in more detail in their own topic.

-   [Windows Events](Windows-Events.md)

    Events in a Windows event log.

-   [Text Logs](Text-Logs.md)

    Text log file that has a single line per entry. The log can be a simple text log where each line is considered a single entry or a delimited text log where a single character is used to separate different fields of data.

-   [WMI Events](WMI-Events.md)

    Events created by Windows Management Instrumentation \(WMI\).

-   [Syslog Events](Syslog-Events.md)

    Events from Unix systems and other devices that send syslog messages.

-   [SNMP Events](SNMP-Events.md)

    SNMP traps that are sent to an agent or SNMP probes that are periodic requests for information from a device.

-   [UNIX-Linux Shell Command Alerts](UNIX-Linux-Shell-Command-Alerts.md)

    Events that are detected through the execution of an UNIX\/Linux command, script, or one\-line sequence of multiple commands \(using pipeline operators\).


