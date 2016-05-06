---
title: Audit Collection Services Performance Counters
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 319bb987-1132-41e8-a5df-2dd65ae5ba7c
---
# Audit Collection Services Performance Counters
In [!INCLUDE[om12long](Token/om12long_md.md)], the Audit Collection Services \(ACS\) collector service includes two performance objects that have a total of 16 counters: the Collector object and the Collector Client object. The Collector object has 14 counters, and the Collector Client object has two counters. The counters in the Collector object record performance statistics from the perspective of the ACS collector. The Collector Client counters record performance statistics from the perspective of a single ACS forwarder.

Performance objects and counters are viewable in System Monitor, which is a part of Performance Console available in Windows Server products. For more information about monitoring performance and System Monitor, see [System Monitor Overview](http://go.microsoft.com/fwlink/?LinkId=74157).

## Collector Object
The following table describes each counter in the Collector performance object. If the counter describes information that is added to a specific table in the ACS database, that table is defined in the counter description.

Connected Clients
The number of ACS forwarders currently connected to the ACS collector.

Database Queue % Full
The ratio of the number of events currently in the ACS database loader queue divided by the highest number of requests that the database loader queue has had. This ratio is expressed as a percentage.

Database Queue Length
The number of events currently in the database loader queue.

DB Loader Events Inserts\/sec
The average number of records added, per second, to the dtEvent table in the ACS database, which contains event record entries.

DB Loader Principal Inserts\/sec
The average number of records added, per second, to the dtPrincipal table in the ACS database, which contains information about the user and computer accounts that have access to the ACS components.

DB Loader String Inserts\/sec
The average number of records added, per second, to the dtString table in the ACS database.

DB Principal Cache Hit %
The percentage of all handling requests that are serviced by the principal cache instead of the dtPrincipal table in the ACS database.

DB Request Queue Length
The number of requests from the ACS collector currently waiting to be serviced by the ACS database. These requests are used during forwarder handshake and during database maintenance. They are not part of normal event handling.

DB String Cache Hit %
The percentage of all handling requests that are serviced by the string cache, thereby avoiding a lookup in the dtString table in the ACS database.

Event time in collector in milliseconds
The amount of time, in milliseconds, between event arrival at the ACS collector and insertion into the ACS database queues.

Incoming Events\/sec
The total number of events arriving, per second, at the collector from all connected ACS forwarders.

Interface Audit Insertions\/sec
The number of event records, per second, sent by the collector to Windows Management Instrumentation \(WMI\) for forwarding to an application outside of ACS.

Interface Queue Length
The average number of requests waiting on WMI resources.

Registered Queries
The total number of subscription requests that WMI has received for ACS events since the ACS Collector service was last started.

## Collector Client Object
The Collector Client performance object displays statistics about events that occur on a specified ACS forwarder. The ACS Collector Client performance object is installed on the ACS collector. If multiple ACS forwarders are connected to the ACS collector, multiple instances of the counter are displayed. In large environments with more than 100 ACS forwarders connected to an ACS collector, the Collector Client performance object, by default, displays the statistics of the ACS forwarders with the highest asset values. ACS forwarders that have the most audit events are assigned higher asset values to ensure their connections are prioritized over ACS forwarders with fewer events.

> [!NOTE]
> Asset values are assigned automatically by the ACS collector. You can change the assigned asset values using AdtAdmin.exe and the *\\UpdForwarder* parameter. For more information about the AdtAdmin.exe tool, see [Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](Audit-Collection-Services-Administration--AdtAdmin.exe-.md).

The Collector Client performance object has two counters. The following table describes each of these counters.

Average time between event generation
The average amount of time, in milliseconds, from the creation of an event to the time the event arrives at the ACS collector.

Incoming Audits\/sec
The total number of events sent to the ACS collector from the ACS forwarder.

## See Also
[Collecting Security Events Using Audit Collection Services in Operations Manager](Collecting-Security-Events-Using-Audit-Collection-Services-in-Operations-Manager.md)
[How to Configure Certficates for ACS Collector and Forwarder](How-to-Configure-Certficates-for-ACS-Collector-and-Forwarder.md)
[Audit Collection Services Capacity Planning](Audit-Collection-Services-Capacity-Planning.md)
[Audit Collection Services Security](Audit-Collection-Services-Security.md)
[How to Enable Audit Collection Services &#40;ACS&#41; Forwarders](How-to-Enable-Audit-Collection-Services--ACS--Forwarders.md)
[How to Enable Event Logging and ACS Rules on Solaris and AIX Computers](How-to-Enable-Event-Logging-and-ACS-Rules-on-Solaris-and-AIX-Computers.md)
[How to Filter ACS Events for UNIX and Linux Computers](How-to-Filter-ACS-Events-for-UNIX-and-Linux-Computers.md)
[Monitoring Audit Collection Services Performance](Monitoring-Audit-Collection-Services-Performance.md)
[How to Remove Audit Collection Services &#40;ACS&#41;](How-to-Remove-Audit-Collection-Services--ACS-.md)
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](Audit-Collection-Services-Administration--AdtAdmin.exe-.md)


