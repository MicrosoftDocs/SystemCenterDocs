---
title: "Ports and Protocols of Standard Activities | Microsoft Docs"
ms.custom: ""
ms.date: "2016-05-13"
ms.prod: "system-center-2012"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "orchestrator"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "System Center 2012 SP1 - Orchestrator"
  - "System Center 2012 - Orchestrator"
  - "System Center 2012 R2 Orchestrator"
ms.assetid: 306056fe-02cc-44e9-8cd2-9df390660915
caps.latest.revision: 2
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Ports and Protocols of Standard Activities
[!INCLUDE[orchshort](../../../SystemCenterDocs/orchestrator/standard-activities/includes/orchshort-md.md)] standard activities can communicate between the runbook servers where the runbook is deployed and any resource. If you have firewalls in your environment, when you use a standard activity, you must enable the ports between the runbook servers and resource as indicated in the following table.  
  
|Standard activity|Port on runbook server|Port on resource server|Notes|  
|-----------------------|----------------------------|-----------------------------|-----------|  
|[Query Database](../../../SystemCenterDocs/orchestrator/standard-activities/query-database.md)||Any port the target database requires.||  
|[Write to Database](../../../SystemCenterDocs/orchestrator/standard-activities/write-to-database.md)||Any port the target database requires.||  
|[Invoke Web Services](../../../SystemCenterDocs/orchestrator/standard-activities/invoke-web-services.md)|HTTP or HTTPS|HTTP or HTTPS||  
|[Map Network Path](../../../SystemCenterDocs/orchestrator/standard-activities/map-network-path.md)|||Activity uses Microsoft Windows file sharing.|  
|[Set SNMP Variable](../../../SystemCenterDocs/orchestrator/standard-activities/set-snmp-variable.md)|SNMP|SNMP||  
|[Get SNMP Variable](../../../SystemCenterDocs/orchestrator/standard-activities/get-snmp-variable.md)|SNMP|SNMP||  
|[Monitor SNMP Trap](../../../SystemCenterDocs/orchestrator/standard-activities/monitor-snmp-trap.md)|SNMP|SNMP||  
|[Send SNMP Trap](../../../SystemCenterDocs/orchestrator/standard-activities/send-snmp-trap.md)|SNMP|SNMP||  
|[Run Program](../../../SystemCenterDocs/orchestrator/standard-activities/run-program.md)|||Activity uses Microsoft Windows file sharing and I/O pipes.|  
|[Send Email](../../../SystemCenterDocs/orchestrator/standard-activities/send-email.md)|SMTP|SMTP||  
|[Monitor Internet Application](../../../SystemCenterDocs/orchestrator/standard-activities/monitor-internet-application.md)|HTTP/SMTP/POP3/FTP/DNS|HTTP/SMTP/POP3/FTP/DNS||  
|[Get Internet Application Status](../../../SystemCenterDocs/orchestrator/standard-activities/get-internet-application-status.md)|HTTP/SMTP/POP3/FTP/DNS/Custom|HTTP/SMTP/POP3/FTP/DNS/Custom|Custom can be anything.|  
|[Send Syslog Message](../../../SystemCenterDocs/orchestrator/standard-activities/send-syslog-message.md)|syslog|syslog||  
  
## Other resources for this product  
  
-   TechNet Library main page for [Orchestrator](../Topic/Orchestrator1.md)  
  
-   [Runbook Activity Reference for System Center 2012 - Orchestrator](../Topic/Runbook%20Activity%20Reference%20for%20System%20Center%202012%20-%20Orchestrator.md)  
  
-   [Alphabetical List of Standard Activities](../../../SystemCenterDocs/orchestrator/standard-activities/alphabetical-list-of-standard-activities.md)  
  
## See Also  
 [TCP Port Requirements](../Topic/TCP%20Port%20Requirements.md)