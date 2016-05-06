---
title: Monitor SNMP Trap
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ca394727-e584-4422-9ce2-5760f29e93d2
---
# Monitor SNMP Trap
The Monitor SNMP Trap activity waits for an event to occur either in the Microsoft SNMP Trap Service, or on a port that you specify. Using filters, you can invoke your runbooks according to the device that raised the event or the enterprise, generic, or specific identifiers of the SNMP trap. Use the Monitor SNMP Trap activity to monitor a network device for critical errors, automatically create a trouble ticket, and perform level 1 diagnostics on the device.

## Configuring the Monitor SNMP Trap Activity
Before you configure the Monitor SNMP Trap activity, you need to determine the following:

-   Version of SNMP that you are using

-   Source host IP address

-   Enterprise identifier of the device

-   Generic or specific identifier of the device that you are monitoring

Use the following information to configure the Monitor SNMP Trap activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Microsoft SNMP Trap Service \(SNMPv1, SNMPv2c\)**|Select this option to use the Microsoft SNMP Trap Service. This service is only compatible with SNMP versions SNMPv1 and SNMPv2c.|
|**No dependency \(SNMPv1, SNMPv2c, SNMPv3\)**|Select this option to monitor SNMP traps using a port rather than the Microsoft SNMP Trap Service.|
|**Port**|If you select the **No dependency** option, type the communication port number that will be monitored for SNMP traps. If you select port **162**, the Microsoft SNMP Trap Service must be disabled because it uses the same port when it runs.|
|**Source host**|Select to specify the IP address of the device where the event originates.|
|**Enterprise identifier**|Select to specify the enterprise identifier of the event raised by the device.|
|**Generic identifier**|Select to specify the generic identifier of the SNMP trap. There are six options available:<br /><br />**coldStart\(0\)**: Select to filter for a cold start of the network device. This option has a numerical value of 0.<br /><br />**warmStart\(1\)**:Select to filter for a warm start of the network device. This option has a numerical value of 1.<br /><br />**linkDown\(2\)**: Select to filter for a severed connection to the network device. This option has a numerical value of 2.<br /><br />**linkUp\(3\)**: Select to filter for a re\-established connection to the network device. This option has a numerical value of 3.<br /><br />**authenticationFailure\(4\)**: Select to filter for a failed SNMP authentications to the network device. This option has a numerical value of 4.<br /><br />**egpNeighborLoss\(5\)**: Select to filter for a lost connection to an EGP neighbor. This option has a numerical value of 5.<br /><br />**enterpriseSpecific\(6\)**: Select to filter based on an enterprise specific ID. This option has a numerical value of 6. You must specify this option to filter based on a Specific identifier.|
|**Specific identifier**|Select to specify an enterprise specific identifier for the SNMP trap. This setting becomes active when you select the **enterpriseSpecific\(6\)** option in the **Generic identifier** box.|

### Published Data
The following table lists published data items.

|Item|Description|
|--------|---------------|
|Source IP address|The IP address of the device where the trap originated.|
|Enterprise Id|The enterprise ID of the trap.|
|Generic Id|The generic ID of the trap.|
|Specific Id|The specific ID of the trap. The value of the specific identifier is published when using the **enterpriseSpecific\(6\)** option of the **Generic identifier** box. Otherwise, a value of 0 \(zero\) is published.|
|Trap port|The port where the trap was received.|
|Varbind count|The number of variable bindings received.|
|SNMP Version|The SNMP version specified for this trap.|


