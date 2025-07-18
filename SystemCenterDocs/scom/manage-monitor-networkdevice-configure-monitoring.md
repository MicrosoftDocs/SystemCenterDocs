---
title: Configure Monitoring of Network Devices
description: This article describes how to configure Operations Manager to sample specific performance metrics and alert for certain issues detected on network devices.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.custom: UpdateFrequency3
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
ms.assetid: 59ac2317-06dc-4f83-b074-47a1bd4b98ac
---

# Configure monitoring of network devices


System Center Operations Manager includes the following management packs specific to network device discovery and monitoring:

- Network Management - Core Monitoring

    This management pack contains monitoring logic for network devices.

- Windows Client Network Discovery

    This management pack contains discovery rules to set the properties of discovered network adapters connected to computers running client operating systems.

- Windows Server Network Discovery

    This management pack contains discovery rules to set the properties of discovered network adapters connected to computers running server operating systems.

- Network Discovery Internal

    This management pack contains definitions and rules for discovering network devices.

- Network Management Library

    This management pack contains definitions for core network device management.

- Network Management Reports

    This management pack contains reports for network management.

- Network Management Templates

    This management pack contains templates for authoring network management workflows.

## Tune network rules

The following rules are disabled by default. Using overrides, enable these rules only for the specific device types in your environment. To view these rules grouped by type, in the **Authoring** workspace, scope **Management Pack Objects** to the network monitoring management packs listed in the previous section, and select **Rules**.

|Rule|Description|Types|
|----|-------|---------|
|**Internal Network Management Discovery Trap Rediscovery**|Internal rule to initiate rediscovery via trap requests|-   Bridge<br>-   Call Server<br>-   Card (Multilayer Switch Feature)<br>-   Firewall<br>-   Host<br>-   Hub<br>-   Load Balancer<br>-   Media Gateway<br>-   Network Device<br>-   Node<br>-   Probe<br>-   Relay Device<br>-   Route Switch Feature Card<br>-   Route Switch Module<br>-   Router<br>-   Switch<br>-   Terminal Server|
|**Output Packet Error Percentage**|Collects the percentage of output packet errors|-   Interface (if-mib dot3)<br>-   Interface (if-mib ethernet)<br>-   Interface (if-mib netcor)<br>-   Interface (if-mib router)<br>-   Interface (netcor cisco ethernet)<br>-   Interface (netcor if-mib cisco ethernet)<br>-   Interface (netcor if-mib cisco)<br>-   Interface (netcor if-mib MIB2)<br>-   Interface (netcor MIB2)<br>-   Interface (netcor router)<br>-   Network adapter (dot3)<br>-   Network adapter (if-mib cisco)<br>-   Network adapter (if-mib performance)<br>-   Network adapter (if-mib)<br>-   Network adapter (MIB2)<br>-   Network adapter (netcor cisco)<br>-   Network adapter (netcor ethernet)<br>-   Network adapter (netcor if-mib)<br>-   Network adapter (netcor performance)<br>-   Network adapter (netcor)<br>-   Port (MIB2 Dot3 ethernet)<br>-   Port (netcor if-mib dot3)|
|**Input Broadcast Packets Percentage**|Collects the percentage of input broadcast packets.|-   Interface (if-mib dot3)<br>-   Interface (if-mib ethernet)<br>-   Interface (if-mib netcor)<br>-   Interface (if-mib router)<br>-   Interface (netcor cisco ethernet)<br>-   Interface (netcor if-mib cisco ethernet)<br>-   Interface (netcor if-mib cisco)<br>-   Interface (netcor if-mib MIB2)<br>-   Interface (netcor MIB2)<br>-   Interface (netcor router)<br>-   Network adapter (if-mib cisco)<br>-   Network adapter (if-mib performance)<br>-   Network adapter (if-mib)<br>-   Network adapter (netcor if-mib)<br>-   Network adapter (netcor performance)<br>-   Port (MIB2 Dot3 ethernet)<br>-   Port (netcor if-mib dot3)|
|**Input Packet Error Percentage**|Collects the percentage of input packet errors|-*   Interface (if-mib dot3)<br>-   Interface (if-mib ethernet)<br>-   Interface (if-mib netcor)<br>-   Interface (if-mib router)<br>-   Interface (netcor cisco ethernet)<br>-   Interface (netcor if-mib cisco ethernet)<br>-   Interface (netcor if-mib cisco)<br>-   Interface (netcor if-mib MIB2)<br>-   Interface (netcor MIB2)<br>-   Interface (netcor router)<br>-   Network adapter (dot3)<br>-   Network adapter (if-mib cisco)<br>-   Network adapter (if-mib performance)<br>-   Network adapter (if-mib)<br>-   Network adapter (MIB2)<br>-   Network adapter (netcor cisco)<br>-   Network adapter (netcor ethernet)<br>-   Network adapter (netcor if-mib)<br>-   Network adapter (netcor performance)<br>-   Network adapter (netcor)<br>-   Port (MIB2 Dot3 ethernet)<br>-   Port (netcor if-mib dot3)|
|**Collision Percentage**|Collects the rate of Ethernet packet collisions|-   Interface (if-mib dot3)<br>-   Interface (if-mib ethernet)<br>-   Interface (netcor cisco ethernet)<br>-   Interface (netcor if-mib cisco ethernet)<br>-   Interface (netcor if-mib cisco ethernet)<br>-   Network adapter (dot3)<br>-   Network adapter (netcor ethernet)<br>-   Port (MIB2 Dot3 ethernet)<br>-   Port (netcor if-mib dot3)|
|**Outbound Multicast Packets per Second**|Collects outbound multicast packets per second|-   Interface (if-mib dot3)<br>-   Interface (if-mib ethernet)<br>-   Interface (if-mib netcor)<br>-   Interface (if-mib router)<br>-   Network adapter (if-mib base)<br>-   Network adapter (if-mib cisco)<br>-   Network adapter (if-mib performance)<br>-   Network adapter (if-mib)|
|**Inbound Unicast Packets per Second**|Collects inbound unicast packets per second|-   Interface (if-mib dot3)<br>-   Interface (if-mib ethernet)<br>-   Interface (if-mib netcor)<br>-   Interface (if-mib router)<br>-   Interface (netcor cisco ethernet)<br>-   Interface (netcor if-mib cisco ethernet)<br>-   Interface (netcor if-mib cisco)<br>-   Interface (netcor if-mib MIB2)<br>-   Interface (netcor MIB2)<br>-   Interface (netcor router)<br>-   Network adapter (dot3)<br>-   Network adapter (if-mib base)<br>-   Network adapter (if-mib cisco)<br>-   Network adapter (if-mib performance)<br>-   Network adapter (if-mib)<br>-   Network adapter (MIB2)<br>-   Network adapter (netcor base)<br>-   Network adapter (netcor cisco)<br>-   Network adapter (netcor ethernet)<br>-   Network adapter (netcor if-mib)<br>-   Network adapter (netcor performance)<br>-   Network adapter (netcor)<br>-   Port (MIB2 Dot3 ethernet)<br>-   Port (netcor if-mib dot3)|
|**Outbound Broadcast Packets per Second**|Collects outbound broadcast packets per second|-   Interface (if-mib dot3)<br>-   Interface (if-mib ethernet)<br>-   Interface (if-mib netcor)<br>-   Interface (if-mib router)<br>-   Network adapter (if-mib base)<br>-   Network adapter (if-mib cisco)<br>-   Network adapter (if-mib performance)<br>-   Network adapter (if-mib)|
|**Outbound Unicast Packets per Second**|Collects outbound unicast packets per second|-   Interface (if-mib dot3)<br>-   Interface (if-mib ethernet)<br>-   Interface (if-mib netcor)<br>-   Interface (if-mib router)<br>-   Interface (netcor cisco ethernet)<br>-   Interface (netcor if-mib cisco ethernet)<br>-   Interface (netcor if-mib cisco)<br>-   Interface (netcor if-mib MIB2)<br>-   Interface (netcor MIB2)<br>-   Interface (netcor router)<br>-   Network adapter (dot3)<br>-   Network adapter (if-mib base)<br>-   Network adapter (if-mib cisco)<br>-   Network adapter (if-mib performance)<br>-   Network adapter (if-mib)<br>-   Network adapter (MIB2)<br>-   Network adapter (netcor base)<br>-   Network adapter (netcor cisco)<br>-   Network adapter (netcor ethernet)<br>-   Network adapter (netcor if-mib)<br>-   Network adapter (netcor performance)<br>-   Network adapter (netcor)<br>-   Port (MIB2 Dot3 ethernet)<br>-   Port (netcor if-mib dot3)|
|**Input Packet Discard Rate**|Collects the percentage of discarded input packets|-   Interface (if-mib dot3)<br>-   Interface (if-mib ethernet)<br>-   Interface (if-mib netcor)<br>-   Interface (if-mib router)<br>-   Interface (netcor cisco ethernet)<br>-   Interface (netcor if-mib cisco ethernet)<br>-   Interface (netcor if-mib cisco)<br>-   Interface (netcor if-mib MIB2)<br>-   Interface (netcor MIB2)<br>-   Interface (netcor router)<br>-   Network adapter (dot3)<br>-   Network adapter (if-mib base)<br>-   Network adapter (if-mib cisco)<br>-   Network adapter (if-mib performance)<br>-   Network adapter (if-mib)<br>-   Network adapter (MIB2)<br>-   Network adapter (netcor base)<br>-   Network adapter (netcor cisco)<br>-   Network adapter (netcor ethernet)<br>-   Network adapter (netcor if-mib)<br>-   Network adapter (netcor performance)<br>-   Network adapter (netcor)<br>-   Port (MIB2 Dot3 ethernet)<br>-   Port (netcor if-mib dot3)|
|**Outbound Bits per Second**|Collects outbound bits per second|-   Interface (if-mib dot3)<br>-   Interface (if-mib ethernet)<br>-   Interface (if-mib netcor)<br>-   Interface (if-mib router)<br>-   Interface (netcor cisco ethernet)<br>-   Interface (netcor if-mib cisco ethernet)<br>-   Interface (netcor if-mib cisco)<br>-   Interface (netcor if-mib MIB2)<br>-   Interface (netcor MIB2)<br>-   Interface (netcor router)<br>-   Network adapter (dot3)<br>-   Network adapter (if-mib base)<br>-   Network adapter (if-mib cisco)<br>-   Network adapter (if-mib performance)<br>-   Network adapter (if-mib)<br>-   Network adapter (MIB2)<br>-   Network adapter (netcor base)<br>-   Network adapter (netcor cisco)<br>-   Network adapter (netcor ethernet)<br>-   Network adapter (netcor if-mib)<br>-   Network adapter (netcor performance)<br>-   Network adapter (netcor)<br>-   Port (MIB2 Dot3 ethernet)<br>-   Port (netcor if-mib dot3)|
|**Inbound Broadcast Packets per Second**|Collects inbound broadcast packets per second|-   Interface (if-mib dot3)<br>-   Interface (if-mib ethernet)<br>-   Interface (if-mib netcor)<br>-   Interface (if-mib router)<br>-   Network adapter (if-mib base)<br>-   Network adapter (if-mib cisco)<br>-   Network adapter (if-mib performance)<br>-   Network adapter (if-mib)|
|**Inbound Bits per Second**|Collects inbound bits per second|-   Interface (if-mib dot3)<br>-   Interface (if-mib ethernet)<br>-   Interface (netcor cisco ethernet)<br>-   Interface (netcor if-mib cisco ethernet)<br>-   Interface (if-mib netcor)<br>-   Interface (if-mib router)<br>-   Interface (netcor if-mib cisco)<br>-   Interface (netcor if-mib MIB2)<br>-   Interface (netcor MIB2)<br>-   Interface (netcor router)<br>-   Network adapter (dot3)<br>-   Network adapter (if-mib base)<br>-   Network adapter (if-mib cisco)<br>-   Network adapter (if-mib performance)<br>-   Network adapter (if-mib)<br>-   Network adapter (MIB2)<br>-   Network adapter (netcor base)<br>-   Network adapter (netcor cisco)<br>-   Network adapter (netcor ethernet)<br>-   Network adapter (netcor if-mib)<br>-   Network adapter (netcor performance)<br>-   Network adapter (netcor)<br>-   Port (MIB2 Dot3 ethernet)<br>-   Port (netcor if-mib dot3)|
|**Inbound Multicast Packets per Second**|Collects inbound multicast packets per second|-   Interface (if-mib dot3)<br>-   Interface (if-mib ethernet)<br>-   Interface (if-mib netcor)<br>-   Interface (if-mib router)<br>-   Network adapter (if-mib base)<br>-   Network adapter (if-mib cisco)<br>-   Network adapter (if-mib performance)<br>-   Network adapter (if-mib)|
|**Interface Utilization**|Collects the utilization of the interface|-   Interface (if-mib dot3)<br>-   Interface (if-mib ethernet)<br>-   Interface (if-mib netcor)<br>-   Interface (if-mib router)<br>-   Interface (netcor cisco ethernet)<br>-   Interface (netcor if-mib cisco ethernet)<br>-   Interface (netcor if-mib cisco)<br>-   Interface (netcor if-mib MIB2)<br>-   Interface (netcor MIB2)<br>-   Interface (netcor router)<br>-   Network adapter (dot3)<br>-   Network adapter (if-mib base)<br>-   Network adapter (if-mib cisco)<br>-   Network adapter (if-mib performance)<br>-   Network adapter (if-mib)<br>-   Network adapter (MIB2)<br>-   Network adapter (netcor base)<br>-   Network adapter (netcor cisco)<br>-   Network adapter (netcor ethernet)<br>-   Network adapter (netcor if-mib)<br>-   Network adapter (netcor performance)<br>-   Network adapter (netcor)<br>-   Port (MIB2 Dot3 ethernet)<br>-   Port (netcor if-mib dot3)|
|**Output Packet Discard Rate**|Collects the percentage of discarded output packets|-   Interface (if-mib dot3)<br>-   Interface (if-mib ethernet)<br>-   Interface (if-mib netcor)<br>-   Interface (if-mib router)<br>-   Interface (netcor cisco ethernet)<br>-   Interface (netcor if-mib cisco ethernet)<br>-   Interface (netcor if-mib cisco)<br>-   Interface (netcor if-mib MIB2)<br>-   Interface (netcor MIB2)<br>-   Interface (netcor router)<br>-   Network adapter (dot3)<br>-   Network adapter (if-mib base)<br>-   Network adapter (if-mib cisco)<br>-   Network adapter (if-mib performance)<br>-   Network adapter (if-mib)<br>-   Network adapter (MIB2)<br>-   Network adapter (netcor base)<br>-   Network adapter (netcor cisco)<br>-   Network adapter (netcor ethernet)<br>-   Network adapter (netcor if-mib)<br>-   Network adapter (netcor performance)<br>-   Network adapter (netcor)<br>-   Port (MIB2 Dot3 ethernet)<br>-   Port (netcor if-mib dot3)|
|**Inbound Queue Packets Dropped Per Second**|Collects the number of packets dropped per second due to the input queue being full.|Interface (Cisco Router)|
|**Inbound Giant Packets per Second**|Collects giant inbound packets per second.|Interface (Cisco Router)|
|**Inbound Packets with CRC Error per Second**|Collects the number of inbound packets per second with CRC errors.|Interface (Cisco Router)|
|**Inbound Packets Aborted per Second**|Collects the number of inbound packets aborted per second.|Interface (Cisco Router)|
|**Inbound Misaligned Packets per Second**|Collects the number of inbound misaligned packets per second.|Interface (Cisco Router)|
|**Output Queue Packets Dropped per Second**|Collects the number of packets dropped per second due to the output queue being full.|Interface (Cisco Router)|
|**Inbound Runts per Second**|Collects the number of inbound packets smaller than permitted by the physical media.|Interface (Cisco Router)|
|**Inbound Packets Ignored per Second**|Collects inbound packets ignored per second.|Interface (Cisco Router)|
|**Output Packet Queue Drop Percentage**|Collects the number of output packets discarded because of output queue overflow.|-   Interface (if-mib ethernet)<br>-   Interface (if-mib router)<br>-   Interface (netcor cisco ethernet)<br>-   Interface (netcor if-mib cisco ethernet)<br>-   Interface (netcor if-mib cisco)<br>-   Interface (netcor router)<br>-   Network adapter (if-mib cisco)<br>-   Network adapter (netcor cisco)<br>-   Network adapter (netcor ethernet)|
|**Input Packet Queue Drop Percentage**|Collects the number of input packets discarded because of input queue overflow.|-   Interface (if-mib ethernet)<br>-   Interface (if-mib router)<br>-   Interface (netcor cisco ethernet)<br>-   Interface (netcor if-mib cisco ethernet)<br>-   Interface (netcor if-mib cisco)<br>-   Interface (netcor router)<br>-   Network adapter (if-mib cisco)<br>-   Network adapter (netcor cisco)<br>-   Network adapter (netcor ethernet)|
|**Outbound Non-Unicast Packets per Second**|Collects outbound non-unicast packets per second.|-   Interface (netcor cisco ethernet)<br>-   Interface (netcor if-mib cisco ethernet)<br>-   Interface (netcor if-mib cisco)<br>-   Interface (netcor if-mib MIB2)<br>-   Interface (netcor MIB2)<br>-   Interface (netcor router)<br>-   Network adapter (dot3)<br>-   Network adapter (MIB2)<br>-   Network adapter (netcor base)<br>-   Network adapter (netcor cisco)<br>-   Network adapter (netcor ethernet)<br>-   Network adapter (netcor if-mib)<br>-   Network adapter (netcor performance)<br>-   Network adapter (netcor)<br>-   Port (MIB2 Dot3 ethernet)<br>-   Port (netcor if-mib dot3)|
|**Inbound Non-Unicast Packets per Second**|Collects inbound non-unicast packets per second.|-   Interface (netcor cisco ethernet)<br>-   Interface (netcor if-mib cisco ethernet)<br>-   Interface (netcor if-mib cisco)<br>-   Interface (netcor if-mib MIB2)<br>-   Interface (netcor MIB2)<br>-   Interface (netcor router)<br>-   Network adapter (dot3)<br>-   Network adapter (MIB2)<br>-   Network adapter (netcor base)<br>-   Network adapter (netcor cisco)<br>-   Network adapter (netcor ethernet)<br>-   Network adapter (netcor if-mib)<br>-   Network adapter (netcor performance)<br>-   Network adapter (netcor)<br>-   Port (MIB2 Dot3 ethernet)<br>-   Port (netcor if-mib dot3)|
|**Port Alignment Errors Rate**|Determines the change in the SNMP dot3StatsAlignmentErrorsRate value for the dot3_Ethernet_Performance_Port since the last polling.|Port (Dot3 ethernet)|
|**Port Carrier Sense Errors Rate**|Determines the change in the SNMP dot3StatsCarrierSenseErrorsRate value for the dot3_Ethernet_Performance_Port since the last polling.|Port (Dot3 ethernet)|
|**Port FCS Errors Rate**|Determines the change in the SNMP dot3StatsFCSErrorsRate value for the dot3_Ethernet_Performance_Port since the last polling.|Port (Dot3 ethernet)|
|**Port Frame Too Longs Rate**|Determines the change in the SNMP dot3StatsFrameTooLongsRate value for the dot3_Ethernet_Performance_Port since the last polling.|Port (Dot3 ethernet)|
|**Port Internal Mac Receive Errors Rate**|Determines the change in the SNMP dot3StatsInternalMacReceiveErrorsRate value for the dot3_Ethernet_Performance_Port since the last polling.|Port (Dot3 ethernet)|
|**Port Internal Mac Transmit Errors Rate**|Determines the change in the SNMP dot3StatsInternalMacTransmitErrorsRate value for the dot3_Ethernet_Performance_Port since the last polling.|Port (Dot3 ethernet)|

## Tune alerts for network monitoring

The following monitors that generate alerts are disabled by default. Using overrides, enable these monitors if you want to receive alerts for the issue.

|Monitor|Description|Targets|
|-----------|---------------|-----------|
|**Interface Is Flapping**|Monitors whether the interface link is switching<br> frequently between up and down based on SNMP traps received.|-   BPX Port (Cisco)<br>-   Interface<br>-   Network Adapter<br>-   Port<br>-   Token Ring Port<br>-   VR Interface|
|**Interface Status**|Aggregate monitor that rolls up interface health states<br> for Operational Status and Administrative Status monitors.|-   BPX Port (Cisco)<br>-   Interface<br>-   Network Adapter<br>-   Port<br>-   Token Ring Port<br>-   VR Interface|
|**High Discard Percentage**|Aggregate monitor that rolls up discard percentage health monitors.|-   BPX Port (Cisco)<br>-   Interface<br>-   Network Adapter<br>-   Port<br>-   Token Ring Port<br>-   VR Interface|
|**High Error Percentage**|Aggregate monitor that rolls up error percentage<br> health monitors.|-  BPX Port (Cisco)<br>-   Interface<br>-   Network Adapter<br>-   Port<br>-   Token Ring Port<br>-   VR Interface|
|**High Queue Drop Percentage**|Aggregate monitor that rolls up queue drop<br> percentage health monitors|-   BPX Port (Cisco)<br>-   Interface<br>-   Network Adapter<br>-   Port<br>-   Token Ring Port<br>-   VR Interface|
|**ICMP (Ping) Monitor**|Monitors the response of network devices to ping.|ICMP IP|
|**ICMPv6 (Ping) Monitor**|Monitors the response of network devices to an IPv6 ping.|ICMPv6 IPv6|
|**Collision Rate (Dot3 Ethernet)**|Monitors the packet collision rate on this device|-   Interface<br>-   Network Adapter|
|**High Input Broadcast Rate (if MIB Dot3 Ethernet Port)**|Monitors the level of input broadcast packets on this device|-   Interface<br>-   Network Adapter|

## Next steps

- To understand how to stop monitoring a network device, see [How to Delete or Restore a Network Device in Operations Manager](manage-monitor-networkdevice-delete-restore.md).

- To view information about the network devices you're monitoring, see [Viewing Network Devices and Data in Operations Manager](manage-monitor-networkdevice-viewing-data.md).  
