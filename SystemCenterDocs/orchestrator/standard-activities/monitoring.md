---
title: "Monitoring | Microsoft Docs"
ms.custom: ""
ms.date: "05/13/2016"
ms.prod: system-center
ms.reviewer: ""
ms.suite: ""
ms.technology: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center 2012 SP1 - Orchestrator"
  - "System Center 2012 - Orchestrator"
  - "System Center 2012 R2 Orchestrator"
ms.assetid: f7d2a4f1-97cf-4dc7-bf68-70c573b6fc08
caps.latest.revision: 7
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Monitoring

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support, we recommend you to [upgrade to Orchestrator 2019](https://docs.microsoft.com/system-center/orchestrator/?view=sc-orch-2019).

::: moniker-end

The following table provides a brief description of tasks you can accomplish when using each Monitoring activity.  

|Tasks|Monitoring Activities|  
|-----------|---------------------------|  
|Invoke a runbook when new events that match a filter appear in the Windows Event Log.|[Monitor Event Log](monitor-event-log.md)|  
|Invoke a runbook when a service has been started or stopped.|[Monitor Service](monitor-service.md)|  
|Check the status of a service on any computer.|[Get Service Status](get-service-status.md)|  
|Invoke a runbook when a process has been started or stopped.|[Monitor Process](monitor-process.md)|  
|Check the status of a running process on any computer.|[Get Process Status](get-process-status.md)|  
|Send a ping to a remote computer or IP address and wait for a response.|[Monitor Computer/IP](monitor-computer-ip.md)|  
|Send a ping to a remote computer or IP address and wait for a response.|[Get Computer/IP Status](get-computer-ip-status.md)|  
|Invoke a runbook when the disk space on a computer passes a critical threshold.|[Monitor Disk Space](monitor-disk-space.md)|  
|Retrieve the current amount of available disk space.|[Get Disk Space Status](get-disk-space-status.md)|  
|Invoke a runbook when an internet application server becomes available or unavailable.|[Monitor Internet Application](monitor-internet-application.md)|  
|Check the availability of a Web, Email (POP3 or SMTP), FTP, DNS, or custom server.|[Get Internet Application Status](get-internet-application-status.md)|  
|Invoke a runbook when a Windows Management Instrumentation (WMI) event is received as a result of the WMI event query you specified.|[Monitor WMI](monitor-wmi.md)|
