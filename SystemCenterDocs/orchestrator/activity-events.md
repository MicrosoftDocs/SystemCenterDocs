---
title: Activity Events
description: This topic describes how to capture events triggered by activities in a runbook for monitoring success or performance issues.
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 51302055-3f9c-43a2-943d-d63769b9ed2b
ms.date: 04/10/2025
author: jyothisuri
ms.author: jsuri
---

# Capture activity events to monitor runbooks

Each activity in an Orchestrator runbook has the ability to send an event whenever it fails to run or is taking too long to run. These events are presented on the **Events** tab of the Runbook Designer or can be configured to be delivered to a receiver as an SNMP trap. Runbook activity events are only sent for those activities that you specifically configure to do so.  

## Configure an activity to send events  

To configure an activity to send events, follow these steps:

1. Open the runbook in the **Runbook Designer**.  

2. Double-click the activity to view its properties.  

3. Select the **Run Behavior** tab.  

4. Enter the number of seconds to send an event when the activity runs too long.  

5. Check the **Report if the activity fails to run** box to send an event when the activity fails.  

6. Select **Finish** to save the activity.  

## Receive Events from SNMP

In addition to viewing the events on the **Events** tab in the Runbook Designer, you can send them to an SNMP trap destination. This lets you monitor the health of the Orchestrator environment by using other tools designed to provide proactive alerting. The only requirement for such a tool is that it can receive SNMP traps. You can use the **Orchestrator Event Delivery Configuration Utility** to add and configure SNMP trap destinations for Runbook events.  

### Add an SNMP Trap Destination

To add an SNMP trap destination, run the `oedc` command one time for each destination that you want to add by using the following syntax:  

```bat
oedc /snmp /add /ip <Targeted IP Address> /port <Targeted Port> /version <version> /community <community>  
```

For example, use the following procedure to send traps by using SNMP version 1 to an SNMP receiver at IP address 10.1.1.10 on port 162 and a community called public.  

### Add an SNMP trap destination

To add an SNMP trap destination, follow these steps:

1. Open a command prompt with administrative credentials.  

::: moniker range="<=sc-orch-2019"
2.  Navigate to `C:\Program Files (x86)\Microsoft System Center\Orchestrator\Management Server`.  
::: moniker-end

::: moniker range=">=sc-orch-2022"
2.  Navigate to `C:\Program Files\Microsoft System Center\Orchestrator\Management Server`.  
::: moniker-end

3. Enter the following command: `oedc /snmp /add /ip 10.1.1.10 /port 162 /version SNMP1 /community public`  

4. Restart the Orchestrator Runbook Service and the Orchestrator Runbook Server Monitor service.  

### Remove All SNMP Trap Destinations

You can't remove individual SNMP trap destinations. Instead, you must remove all destinations, and then add back any that you want. To remove all SNMP trap destination, run the `oedc` command with the following syntax:  

**oedc /snmp /clear**  

To remove all SNMP trap destinations, follow these steps:

1. Open a command prompt with administrative credentials.  

::: moniker range="<=sc-orch-2019"
2.  Navigate to `C:\Program Files (x86)\Microsoft System Center\Orchestrator\Management Server`.  
::: moniker-end

::: moniker range=">=sc-orch-2022"
2.  Navigate to `C:\Program Files\Microsoft System Center\Orchestrator\Management Server`.  
::: moniker-end

3. Enter the following command: **oedc /snmp /clear**  

4. Restart the Orchestrator Runbook Service and the Orchestrator Runbook Server Monitor service.  

### Receive SNMP Traps

After you've configured an SNMP trap destination for Orchestrator event notifications, you can receive them by using any tool that reads SNMP traps, or you can use the **Monitor SNMP Trap** activity in a runbook to read the information. The content of SNMP traps is limited to the first 1000 characters if the content exceeds that length.  

The variable bindings are listed in the following table:  

|Trap Enterprise ID|1.3.6.1.4.1.4217.100.100|  
|---|---|    
|Generic ID|\(6\)|  
|Specific ID|\(1\)|  
|Orchestrator Event Information IDs|Orchestrator Event Type - 1<br /><br />Orchestrator Event Summary - 2<br /><br />Orchestrator Event Details - 3|  
|Example|Orchestrator Event Type - 1.3.6.1.4.1.4217.100.100.1<br /><br />Orchestrator Event Summary - 1.3.6.1.4.1.4217.100.100.2<br /><br />Orchestrator Event Details - 1.3.6.1.4.1.4217.100.100.3|  

## Next steps  

- Look up the data that is captured when activities fire at [Orchestrator Logs](orchestrator-logs.md).  
- Read more about SNMP traps at [SNMP Traps in Windows Server](https://blogs.technet.microsoft.com/networking/2009/06/25/snmp-traps-in-windows-server/).
