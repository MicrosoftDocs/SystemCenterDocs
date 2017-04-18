---
title: Monitoring Networks by Using Operations Manager
description: This article provides an overview of how you can monitor network devices with Operations Manager 2016.
author: mgoedtel
ms.author: magoedte
manager: cfreeman
ms.date: 01/26/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: fe56f0f3-0f28-4b0c-8adf-9982a710540a
---

# Monitoring networks by using Operations Manager

>Applies To: System Center 2016 - Operations Manager

System Center 2016 - Operations Manager can monitor physical network routers and switches, including the interfaces and ports on those devices, and the virtual local area networks (VLANs) and Hot Standby Router Protocol (HSRP) groups that they participate in, as well as firewalls and load balancers. Increased visibility into your network infrastructure can help you identify failures in critical services and applications that were caused by the network. For example, you observe an alert informing you that a critical server is unavailable. If you have configured network monitoring, you would also observe an alert informing you that a port is offline. When you view the computer vicinity diagram for the server, you see that the unavailable computer is connected to the offline port. Thus, you can focus on troubleshooting the root cause for the unavailable computers.  
  
Operations Manager can show you how your network is connected to the computers you are monitoring through the [Network Vicinity View](../om/manage/../om/manage/viewing-network-devices-and-data-in-operations-manager.md#network-vicinity-dashboard) dashboard. Using Network Vicinity View, you can see how your topology is laid out, as well as the health of each network device, computer, and the connection between each.  
  
Operations Manager can discover and monitor network devices that use the Simple Network Management Protocol (SNMP v1, v2c, and v3. For a complete list of supported devices, see  [Network Devices with Extended Monitoring Capability spreadsheet](http://go.microsoft.com/fwlink/p/?LinkID=231254). The devices worksheet includes processor and memory columns for each device to indicate whether Operations Manager can provide extended monitoring for either or both aspects for each device.  

With System Center 2016 - Operations Manager, a Network Monitoring Management Pack generation tool is included to help you create a custom management pack to add extended monitoring support for new network devices, without the need of Microsoft device certification.  In addition to that, this tool enables you to add monitoring of additional device components such as fan, temperature sensor, voltage sensor and power supply. You can download the tool and user guide from the [Microsoft Download Center](http://download.microsoft.com/download/D/8/C/D8C9D294-2434-4E6F-89BF-76BB6BC15921/NetMonMPGeneratorTool.docx). 
  
## Network device monitoring capabilities and scope  

Operations Manager provides the following monitoring for discovered network devices:  
  
-   Connection health - Based on looking at both ends of a connection  
  
-   VLAN health - Based on health state of switches in VLAN  
  
-   HSRP group health - Based on health state of individual HSRP end points  
  
-   Port/Interface  
  
    -   Up/down (operational & administrative status)  
  
    -   Volumes of inbound/outbound traffic (includes abort, broadcast, carrier sense, collision, CRC rates, discard, error, FCS error, frame, giants, runts, ignored, MAC transmit/receive error, queue rates)  
  
    -   % Utilization  
  
    -   Drop and broadcast rates  
  
    > [!NOTE]  
    > Ports that are connected to a computer are not monitored; only ports that connect to other network devices are monitored. You can monitor a port that is connected to a computer that is not agent-managed in the same management group by adding the port to the Critical Network Adapters Group.  
  
-   Processor - % Utilization (for some certified devices)  
  
-   Memory - including high utilization, high buffer utilization, excessive fragmentation, and buffer allocation failures (for some certified devices)  
  
    -   In-depth memory counters (Cisco devices only)  
  
    -   Free memory  
  
> [!NOTE]  
> Some of the monitoring capabilities are disabled by default. For more information, see [How to configure monitoring of network devices](../om/manage/how-to-configure-monitoring-of-network-devices.md).  
  
Operations Manager supports monitoring of the following number of network devices:  
  
-   2000 network devices (approximately 25,000 monitored ports) managed by two resource pools  
  
-   1000 network devices (approximately 12,500 monitored ports) managed by a resource pool that has three or more management servers  
  
-   500 network devices (approximately 6,250 monitored ports) managed by a resource pool that has two or more gateway servers  
  
## Required management packs  

Network discovery and monitoring requires the following management packs, which are installed with Operations Manager:  
  
-   Microsoft.Windows.Server.NetworkDiscovery  
  
-   Microsoft.Windows.Client.NetworkDiscovery  
  
There are additional management packs that are required to relate network devices to each other and to the agent computers they are connected to. Network monitoring requires discovery of the network adapter for each agent computer, which is performed by the management pack for the agent computer's operating system. Verify that the management packs from the following list are installed for each of the operating systems in your environment.  
  
-   [Windows Server 2003, 2008, 2008 R2, 2012, and 2012 R2 Operating System](http://go.microsoft.com/fwlink/p/?LinkId=219547)  
  
-   [Windows Client 2000/XP/Vista/Windows 7 Operating Systems](http://go.microsoft.com/fwlink/p/?LinkId=219548)  

-   [Windows 8 and 8.1 Client Operating System](https://www.microsoft.com/download/details.aspx?id=38434) 
  
-   [Windows 10 Client Operating System](https://www.microsoft.com/download/details.aspx?id=51189)  


## How Network device discovery works  

Network device discovery is performed by discovery rules that you create. For instructions on creating a discovery rule, see [How to discover network devices in Operations Manager](../om/manage/how-to-discover-network-devices-in-operations-manager.md) and [How to configure network device discovery settings](../om/manage/how-to-configure-network-device-discovery-settings.md).  
  
When you create a discovery rule, you designate a management server or gateway server to run the rule. Each management server or gateway server can run only one discovery rule. You may need to strategically place management servers on different network segments so that they can access the network devices that they are discovering.  
  
Discovery rules run on a schedule that you can specify, and you can also run a rule on demand. Each time the discovery rule runs, it attempts to find new devices within its definition or changes to devices that were previously discovered. A discovery rule can perform *explicit discovery* or *recursive discovery*.  
  
-   *Explicit discovery* - An explicit discovery rule will only attempt to discover those devices that you explicitly specify in the wizard by IP address or FQDN. It will only monitor those devices that it can successfully access. The rule will attempt to access the device by using ICMP, SNMP, or both depending on the configuration of the rule.  
  
-   *Recursive discovery* - A recursive discovery rule will attempt to discover those devices that you explicitly specify in the wizard by IP address, as well as other network devices that are connected to the specified SNMP v1 or v2 device and that the specified SNMP v1 or v2 device knows about through the device's Address Routing Protocol (ARP) table, its IP address table, or the topology Management Information Block (MIB).  
  
    If you use recursive discovery, you can elect to discover all the other network devices that the specified SNMP v1 or v2 device knows about or only network devices that are connected to the specified SNMP v1 or v2 device that are in a specified IP address range. You can also filter recursive discovery by using such properties as the device type, name, and object identifier (OID).  
  
    > [!NOTE]  
    > Operations Manager can identify connected devices in a recursive discovery that use an IPv6 address; however, the initial device that is discovered must use an IPv4 address.  
  
A discovery rule can perform only explicit or recursive discovery, but cannot perform a combination of discovery types. You can change the discovery type of a rule after the rule is created. If you know all of the network devices that you want discovered, you should use explicit discovery. Recursive discovery can discover devices that you have no business need to monitor and as a result, can increase the administrative workload of monitoring your network.  
  
A discovery rule can discover any combination of SNMP v1, v2, and v3 devices. SNMP v3 devices can only be discovered by explicit discovery or by being specified in a recursive discovery rule. If you specify an SNMP v3 device in a recursive discovery rule, the SNMP v3 device will be discovered but devices connected to it will not be discovered. If you specify an SNMP v1 or v2 device in a recursive discovery rule, only SNMP v1 and v2 devices connected to it will be included in the recursive discovery.  
  
SNMP trap rules are not supported for SNMP v3 devices.  
  
> [!NOTE]  
> Windows computers running SNMP are filtered out of discovery results if:  
>   
> -   The device type is "Host" and the vendor is "Microsoft"  
> -   The sysDescription field contains "Microsoft"  
> -   The sysOid starts with .1.3.6.1.4.1.311.1.1.3.1  
> -   The sysOid contains 1.3.6.1.4.1.199.1.1.3.11  
  
In the discovery rule configuration, you specify whether Operations Manager will use ICMP, SNMP, or both to communicate with the network device. The network device must support the protocol that you specify. When the discovery rule runs, Operations Manager attempts to contact the network devices that you specify, using the protocol or protocols that you specified. If you specify that a device uses both ICMP and SNMP, Operations Manager must be able to contact the device by using both methods or discovery will fail. If you specify ICMP as the only protocol to use, discovery is limited to the specified device and monitoring is limited to whether the device is online or offline.  
  
Credentials are also needed to communicate with the device. You associate each discovery rule with Run As accounts that supply the community string (for SNMP v1 and v2 devices) or access credentials (SNMP v3) to Operations Manager. For more information, see [Run As Accounts for Network Monitoring in Operations Manager](../om/manage/run-as-accounts-for-network-monitoring-in-operations-manager.md).  
  
After Operations Manager successfully accesses a specified network device, if you selected recursive discovery, it attempts to discover other network devices that the specified device knows about through the device's ARP table, its IP address table, or the topology MIB files.  
  
Network device discovery consists of the following phases, which are displayed in the status of the discovery task:  
  
1.  **Probing**  
  
    During the probing phase, Operations Manager attempts to contact device using the specified protocol, as follows:  
  
    -   ICMP only: ping the device  
  
    -   ICMP and SNMP: contact the device using both protocols  
  
    -   SNMP only: uses the SNMP GET message  
  
2.  **Processing**  
  
    After probing is complete, Operations Manager processes all of the components of the device, such as ports and interfaces, memory, processors, VLAN membership, and HSRP groups.  
  
3.  **Post Processing**  
  
    Operations Manager correlates network device ports to the servers that the ports are connected to, inserts items into the operational database, and associates Run As accounts.  
  
After discovery is complete, the management server resource pool that you specify in the discovery rule begins monitoring the discovered network devices. For more information on monitoring network devices, see [Viewing Network Devices and Data in Operations Manager]../om/manage/viewing-network-devices-and-data-in-operations-manager.md) and [Reports for Network Monitoring in Operations Manager](../om/manage/reports-for-network-monitoring-in-operations-manager.md).  
  
## Next steps

- Review [Configuring a Firewall for Operations Manager](plan-security-config-firewall.md) to understand the firewall ports and direction the communication flows in preparing your environment for network device monitoring with Operations Manager.  

- Learn [How to discover network devices in Operations Manager](../om/manage/how-to-discover-network-devices-in-operations-manager.md).  

- Review [Run As accounts for network monitoring in Operations Manager](../om/manage/run-as-accounts-for-network-monitoring-in-operations-manager.md) to understand how to configure the Run As accounts before configuring the Run As accounts or network device discovery rules.  

- To view information about the network devices you are monitoring, see [Viewing Network Devices and Data in Operations Manager](../om/manage/viewing-network-devices-and-data-in-operations-manager.md).  
  