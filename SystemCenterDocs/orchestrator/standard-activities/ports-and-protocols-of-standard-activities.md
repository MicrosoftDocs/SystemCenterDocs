---
title: "Ports and Protocols of Standard Activities | Microsoft Docs"
ms.custom: na
ms.date: 1/2/2018
ms.prod: system-center
ms.reviewer: ""
ms.suite: ""
ms.technology: orchestrator
ms.tgt_pltfrm: ""
ms.topic: reference
author: bwren
ms.author: bwren
manager: cfreeman
---
# Ports and Protocols of Standard Activities
Orchestrator standard activities can communicate between the runbook servers where the runbook is deployed and any resource. If you have firewalls in your environment, when you use a standard activity, you must enable the ports between the runbook servers and resource as indicated in the following table.  
  
|Standard activity|Port on runbook server|Port on resource server|Notes|  
|-----------------------|----------------------------|-----------------------------|-----------|  
|[Query Database](query-database.md)||Any port the target database requires.||  
|[Write to Database](write-to-database.md)||Any port the target database requires.||  
|[Invoke Web Services](invoke-web-services.md)|HTTP or HTTPS|HTTP or HTTPS||  
|[Map Network Path](map-network-path.md)|||Activity uses Microsoft Windows file sharing.|  
|[Set SNMP Variable](set-snmp-variable.md)|SNMP|SNMP||  
|[Get SNMP Variable](get-snmp-variable.md)|SNMP|SNMP||  
|[Monitor SNMP Trap](monitor-snmp-trap.md)|SNMP|SNMP||  
|[Send SNMP Trap](send-snmp-trap.md)|SNMP|SNMP||  
|[Run Program](run-program.md)|||Activity uses Microsoft Windows file sharing and I/O pipes.|  
|[Send Email](send-email.md)|SMTP|SMTP||  
|[Monitor Internet Application](monitor-internet-application.md)|HTTP/SMTP/POP3/FTP/DNS|HTTP/SMTP/POP3/FTP/DNS||  
|[Get Internet Application Status](get-internet-application-status.md)|HTTP/SMTP/POP3/FTP/DNS/Custom|HTTP/SMTP/POP3/FTP/DNS/Custom|Custom can be anything.|  
|[Send Syslog Message](send-syslog-message.md)|syslog|syslog||  
  
## Other resources for this product  
  
-   [Orchestrator overview](../learn-about-orchestrator.md)  
    
-   [Alphabetical List of Standard Activities](alphabetical-list-of-standard-activities.md)  
