---
title: Activity Events
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 51302055-3f9c-43a2-943d-d63769b9ed2b
ms.author: cfreeman
ms.date: 10/12/2016
author: cfreemanwa
manager: cfreeman
---

# Activity Events

> Applies To: System Center 2016 - Orchestrator

Each activity in an Orchestrator runbook has the ability to send an event whenever it fails to run or is taking too long to run. These events are presented on the **Events** tab of the Runbook Designer or can be configured to be delivered to a receiver as an SNMP trap. Runbook activity events are only sent for those activities that you specifically configure to do so.  

### To configure an activity to send events  

1.  Open the runbook in the **Runbook Designer**.  

2.  Double\-click the activity to view its properties.  

3.  Click the **Run Behavior** tab.  

4.  Type a number of seconds to send an event when the activity runs too long.  

5.  Check the **Report if the activity fails to run** box to send an event when the activity fails.  

6.  Click **Finish** to save the activity.  

## Receiving Events from SNMP  
In addition to viewing the events on the **Events** tab in the Runbook Designer, you can send them to an SNMP trap destination. This lets you monitor the health of the Orchestrator environment by using other tools designed to provide proactive alerting. The only requirement for such a tool is that it can receive SNMP traps. You can use the **Orchestrator Event Delivery Configuration Utility** to add and configure SNMP trap destinations for Runbook events.  

### Add an SNMP Trap Destination  
To add an SNMP trap destination, run the **oedc** command one time for each destination that you want to add by using the following syntax:  

**oedc \/snmp \/add \/ip***<Targeted IP Address>***\/port***<Targeted Port>***\/version***<version>***\/community<community>**  

For example, use the following procedure to send traps by using SNMP version 1 to an SNMP receiver at IP address 10.1.1.10 on port 162 and a community called public.  

##### To add an SNMP trap destination  

1.  Open a command prompt with administrative credentials.  

2.  Navigate to *System Drive*:\\Program Files \(x86\)\\Microsoft System Center 2016\\Orchestrator\\Management Server.  

3.  Type the following command: **oedc \/snmp \/add \/ip 10.1.1.10 \/port 162 \/version SNMP1 \/community public**  

4.  Restart the Orchestrator Runbook Service and the Orchestrator Runbook Server Monitor service.  

### Remove All SNMP Trap Destinations  
You cannot remove individual SNMP trap destinations. Instead, you must remove all destinations, and then add back any that you want. To remove all SNMP trap destination, run the **oedc** command with the following syntax:  

**oedc \/snmp \/clear**  

##### To remove all SNMP trap destinations  

1.  Open a command prompt with administrative credentials.  

2.  Navigate to *System Drive*:\\Program Files \(x86\)\\Microsoft System Center 2016\\Orchestrator\\Management Server.  

3.  Type the following command: **oedc \/snmp \/clear**  

4.  Restart the Orchestrator Runbook Service and the Orchestrator Runbook Server Monitor service.  

### Receiving SNMP Traps  
After you have configured an SNMP trap destination for Orchestrator event notifications, you can receive them by using any tool that reads SNMP traps, or you can use the **Monitor SNMP Trap** activity in a runbook to read the information. The content of SNMP traps is limited to the first 1000 characters if the content exceeds that length.  

The variable bindings are listed in the following table.  

|||  
|---|---|  
|Trap Enterprise ID|1.3.6.1.4.1.4217.100.100|  
|Generic ID|\(6\)|  
|Specific ID|\(1\)|  
|Orchestrator Event Information IDs|Orchestrator Event Type - 1<br /><br />Orchestrator Event Summary - 2<br /><br />Orchestrator Event Details - 3|  
|Example|Orchestrator Event Type - 1.3.6.1.4.1.4217.100.100.1<br /><br />Orchestrator Event Summary - 1.3.6.1.4.1.4217.100.100.2<br /><br />Orchestrator Event Details - 1.3.6.1.4.1.4217.100.100.3|  

## See Also  

[Orchestrator Logs](../get-started/orchestrator-logs.md)  
