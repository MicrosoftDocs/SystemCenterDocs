---
title: Monitoring Networks by Using Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe56f0f3-0f28-4b0c-8adf-9982a710540a
---
# Monitoring Networks by Using Operations Manager
[!INCLUDE[om12long](./Token/om12long_md.md)] can monitor physical network routers and switches, including the interfaces and ports on those devices, and the virtual local area networks \(VLANs\) and Hot Standby Router Protocol \(HSRP\) groups that they participate in, as well as firewalls and load balancers. Increased visibility into your network infrastructure can help you identify failures in critical services and applications that were caused by the network. For example, you observe an alert informing you that a critical server is unavailable. If you have configured network monitoring, you would also observe an alert informing you that a port is offline. When you view the computer vicinity diagram for the server, you see that the unavailable computer is connected to the offline port. Thus, you can focus on troubleshooting the root cause for the unavailable computers.

[!INCLUDE[om12short](./Token/om12short_md.md)] can show you how your network is connected to the computers you are monitoring through the [Network Vicinity View](https://technet.microsoft.com/en-us/library/1a28a022-698a-4bb9-8611-7e2fa799b372) dashboard. Using Network Vicinity View, you can see how your topology is laid out, as well as the health of each network device, computer, and the connection between each.

[!INCLUDE[om12short](./Token/om12short_md.md)] can discover and monitor network devices that use the Simple Network Management Protocol \(SNMP\) v1, v2c, and v3. For a complete list of supported devices, see [Network Devices Supported for Discovery by Operations Manager](./Network-Devices-Supported-for-Discovery-by-Operations-Manager.md).

## <a name="bkmk_networkdevicemonitoringcapabilitiesandscope"></a>Network Device Monitoring Capabilities and Scope
[!INCLUDE[om12short](./Token/om12short_md.md)] provides the following monitoring for discovered network devices:

-   Connection health \- Based on looking at both ends of a connection

-   VLAN health \- Based on health state of switches in VLAN

-   HSRP group health \- Based on health state of individual HSRP end points

-   Port\/Interface

    -   Up\/down \(operational & administrative status\)

    -   Volumes of inbound\/outbound traffic \(includes abort, broadcast, carrier sense, collision, CRC rates, discard, error, FCS error, frame, giants, runts, ignored, MAC transmit\/receive error, queue rates\)

    -   % Utilization

    -   Drop and broadcast rates

    > [!NOTE]
    > Ports that are connected to a computer are not monitored; only ports that connect to other network devices are monitored. You can monitor a port that is connected to a computer that is not agent\-managed in the same management group by adding the port to the Critical Network Adapters Group.

-   Processor \- % Utilization \(for some certified devices\)

-   Memory \- including high utilization, high buffer utilization, excessive fragmentation, and buffer allocation failures \(for some certified devices\)

    -   In\-depth memory counters \(Cisco devices only\)

    -   Free memory

> [!NOTE]
> Some of the monitoring capabilities are disabled by default. For more information, see [Tuning Network Monitoring](./Tuning-Network-Monitoring.md).

Operations Manager supports monitoring of the following number of network devices:

-   2000 network devices \(approximately 25,000 monitored ports\) managed by two resource pools

-   1000 network devices \(approximately 12,500 monitored ports\) managed by a resource pool that has three or more management servers

-   500 network devices \(approximately 6,250 monitored ports\) managed by a resource pool that has two or more gateway servers

## Required Management Packs
Network discovery and monitoring requires the following management packs, which are installed with Operations Manager:

-   Microsoft.Windows.Server.NetworkDiscovery

-   Microsoft.Windows.Client.NetworkDiscovery

There are additional management packs that are required to relate network devices to each other and to the agent computers they are connected to. Network monitoring requires discovery of the network adapter for each agent computer, which is performed by the management pack for the agent computer’s operating system. Verify that the management packs from the following list are installed for each of the operating systems in your environment.

-   [Windows Server 2003 Operating System](http://go.microsoft.com/fwlink/p/?LinkId=219547)

-   [Windows Server 2008 Operating System](http://go.microsoft.com/fwlink/p/?LinkId=219547)

-   [Windows 7 Client Operating Systems](http://go.microsoft.com/fwlink/p/?LinkId=219548)

-   [Windows Vista Client Operating Systems](http://go.microsoft.com/fwlink/p/?LinkId=219548)

## <a name="bkmk_hownetworkdevicediscoveryworks"></a>How Network Device Discovery Works
Network device discovery is performed by discovery rules that you create. For instructions on creating a discovery rule, see [How to Discover Network Devices in Operations Manager](./How-to-Discover-Network-Devices-in-Operations-Manager.md) and [Network Device Discovery Settings](./Network-Device-Discovery-Settings.md).

When you create a discovery rule, you designate a management server or gateway server to run the rule. Each management server or gateway server can run only one discovery rule. You may need to strategically place management servers on different network segments so that they can access the network devices that they are discovering.

Discovery rules run on a schedule that you can specify, and you can also run a rule on demand. Each time the discovery rule runs, it attempts to find new devices within its definition or changes to devices that were previously discovered. A discovery rule can perform *explicit discovery* or *recursive discovery*.

-   *Explicit discovery* – An explicit discovery rule will only attempt to discover those devices that you explicitly specify in the wizard by IP address or FQDN. It will only monitor those devices that it can successfully access. The rule will attempt to access the device by using ICMP, SNMP, or both depending on the configuration of the rule.

-   *Recursive discovery* – A recursive discovery rule will attempt to discover those devices that you explicitly specify in the wizard by IP address, as well as other network devices that are connected to the specified SNMP v1 or v2 device and that the specified SNMP v1 or v2 device knows about through the device’s Address Routing Protocol \(ARP\) table, its IP address table, or the topology Management Information Block \(MIB\).

    If you use recursive discovery, you can elect to discover all the other network devices that the specified SNMP v1 or v2 device knows about or only network devices that are connected to the specified SNMP v1 or v2 device that are in a specified IP address range. You can also filter recursive discovery by using such properties as the device type, name, and object identifier \(OID\).

    > [!NOTE]
    > Operations Manager can identify connected devices in a recursive discovery that use an IPv6 address; however, the initial device that is discovered must use an IPv4 address.

A discovery rule can perform only explicit or recursive discovery, but cannot perform a combination of discovery types. You can change the discovery type of a rule after the rule is created. If you know all of the network devices that you want discovered, you should use explicit discovery. Recursive discovery can discover devices that you have no business need to monitor and as a result, can increase the administrative workload of monitoring your network.

A discovery rule can discover any combination of SNMP v1, v2, and v3 devices. SNMP v3 devices can only be discovered by explicit discovery or by being specified in a recursive discovery rule. If you specify an SNMP v3 device in a recursive discovery rule, the SNMP v3 device will be discovered but devices connected to it will not be discovered. If you specify an SNMP v1 or v2 device in a recursive discovery rule, only SNMP v1 and v2 devices connected to it will be included in the recursive discovery.

SNMP trap rules are not supported for SNMP v3 devices.

> [!NOTE]
> Windows computers running SNMP are filtered out of discovery results if:
> 
> -   The device type is “Host” and the vendor is “Microsoft”
> -   The sysDescription field contains “Microsoft”
> -   The sysOid starts with .1.3.6.1.4.1.311.1.1.3.1
> -   The sysOid contains 1.3.6.1.4.1.199.1.1.3.11

In the discovery rule configuration, you specify whether Operations Manager will use ICMP, SNMP, or both to communicate with the network device. The network device must support the protocol that you specify. When the discovery rule runs, [!INCLUDE[om12short](./Token/om12short_md.md)] attempts to contact the network devices that you specify, using the protocol or protocols that you specified. If you specify that a device uses both ICMP and SNMP, [!INCLUDE[om12short](./Token/om12short_md.md)] must be able to contact the device by using both methods or discovery will fail. If you specify ICMP as the only protocol to use, discovery is limited to the specified device and monitoring is limited to whether the device is online or offline.

Credentials are also needed to communicate with the device. You associate each discovery rule with Run As accounts that supply the community string \(for SNMP v1 and v2 devices\) or access credentials \(SNMP v3\) to [!INCLUDE[om12short](./Token/om12short_md.md)]. For more information, see [Run As Accounts for Network Monitoring in Operations Manager](./Run-As-Accounts-for-Network-Monitoring-in-Operations-Manager.md).

After [!INCLUDE[om12short](./Token/om12short_md.md)] successfully accesses a specified network device, if you selected recursive discovery, it attempts to discover other network devices that the specified device knows about through the device’s ARP table, its IP address table, or the topology MIB files.

Network device discovery consists of the following phases, which are displayed in the status of the discovery task:

1.  **Probing**

    During the probing phase, [!INCLUDE[om12short](./Token/om12short_md.md)] attempts to contact device using the specified protocol, as follows:

    -   ICMP only: ping the device

    -   ICMP and SNMP: contact the device using both protocols

    -   SNMP only: uses the SNMP GET message

2.  **Processing**

    After probing is complete, [!INCLUDE[om12short](./Token/om12short_md.md)] processes all of the components of the device, such as ports and interfaces, memory, processors, VLAN membership, and HSRP groups.

3.  **Post Processing**

    [!INCLUDE[om12short](./Token/om12short_md.md)] correlates network device ports to the servers that the ports are connected to, inserts items into the operational database, and associates Run As accounts.

After discovery is complete, the management server resource pool that you specify in the discovery rule begins monitoring the discovered network devices. For more information on monitoring network devices, see [Viewing Network Devices and Data in Operations Manager](./Viewing-Network-Devices-and-Data-in-Operations-Manager.md) and [Reports for Network Monitoring in Operations Manager](./Reports-for-Network-Monitoring-in-Operations-Manager.md).

## See Also
[How to Discover Network Devices in Operations Manager](./How-to-Discover-Network-Devices-in-Operations-Manager.md)
[Network Device Discovery Settings](./Network-Device-Discovery-Settings.md)
[Run As Accounts for Network Monitoring in Operations Manager](./Run-As-Accounts-for-Network-Monitoring-in-Operations-Manager.md)
[How to Delete or Restore a Network Device in Operations Manager](./How-to-Delete-or-Restore-a-Network-Device-in-Operations-Manager.md)
[Viewing Network Devices and Data in Operations Manager](./Viewing-Network-Devices-and-Data-in-Operations-Manager.md)
[Security for Servers Performing Network Discovery](./Security-for-Servers-Performing-Network-Discovery.md)
[Network Devices Supported for Discovery by Operations Manager](./Network-Devices-Supported-for-Discovery-by-Operations-Manager.md)
[Reports for Network Monitoring in Operations Manager](./Reports-for-Network-Monitoring-in-Operations-Manager.md)
[Tuning Network Monitoring](./Tuning-Network-Monitoring.md)


