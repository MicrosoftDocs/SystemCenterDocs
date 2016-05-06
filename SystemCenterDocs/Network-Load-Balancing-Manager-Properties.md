---
title: Network Load Balancing Manager Properties
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6863bc14-7c12-4c85-a3a5-c242b5e82f89
---
# Network Load Balancing Manager Properties
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>The following table describes the properties that are related to Network Load Balancing (NLB).</para>
  </introduction>
  <section>
    <title>Network Load Balancing properties</title>
    <content>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD colspan="1">
              <para>Tab</para>
            </TD>
            <TD colspan="1">
              <para>Description</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD colspan="1">
              <para>Cluster IP addresses </para>
            </TD>
            <TD colspan="1">
              <para>The <ui>IP address</ui> parameter specifies the cluster's primary IP address. IPv4 addresses use the standard Internet dotted notation (for example, w.x.y.z). IPv6 addresses use 16-byte addresses, typically expressed in colon-hexadecimal notation. Colon-hexadecimal notation uses eight 4-digit hexadecimal numbers, with colons separating the 16-bit blocks (the 4-digit numbers). </para>
              <para>To manage addresses more easily, IPv6 suppresses leading zeros and compresses a single contiguous all-zero 16-bit block, representing the contiguous block with two colons (::). This is known as double-colon compression. An example of an IPv6 address with leading zeros suppressed and double-colon compression is: </para>
              <para>FE80::2AA:FF:FE9A:4CA2</para>
              <para>The address is a virtual IP address, and it must be set identically for all hosts in the cluster. This IP address is used to address the cluster as a whole, and it should be the IP address that maps to the full Internet name that you specify for the cluster. </para>
              <para>If you want to add multiple IP addresses to the cluster, click <ui>Add</ui> to enter the additional IP addresses. If you are configuring a virtual private network (VPN) load-balancing cluster, you should not configure the dedicated IP address. On a VPN, only the cluster IP address should be present on each of the cluster hosts.</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Cluster parameters</para>
            </TD>
            <TD colspan="1">
              <list class="bullet">
                <listItem>
                  <para>The <ui>IP address</ui> parameter specifies the cluster's primary IP address in standard Internet dotted notation (for example, w.x.y.z). You can select a different IP address for the cluster by clicking the drop-down list.</para>
                </listItem>
                <listItem>
                  <para>The <ui>Subnet mask</ui> parameter denotes the subnet mask for the IP address that is specified. The mask is entered in standard Internet dotted notation (for example, 255.255.255.0). This is shown only when the cluster IP address is an IPv4 address.</para>
                </listItem>
                <listItem>
                  <para>The <ui>Full Internet name</ui> parameter specifies a full Internet name for the NLB cluster (for example, cluster.microsoft.com). This name is used for the cluster as a whole, and it should be the same for all hosts in the cluster. If you alias several names for the cluster, enter the primary (main) name here. This name should be resolvable to the cluster's primary IP address through your DNS server or <ui>Hosts</ui> file.</para>
                </listItem>
                <listItem>
                  <para>The <ui>Network address</ui> parameter specifies the media access control (MAC) address for the network adapter that is to be used for handling client-to-cluster traffic. If multicast support is disabled, the host reverts to unicast mode. NLB automatically instructs the driver that belongs to the cluster adapter to override the adapter's unique, built-in network address and to change its MAC address to the cluster's MAC address. This is the address used on all cluster hosts. You do not need to manually configure the network adapter to recognize this address. </para>
                  <para>If you have other NLB clusters on one local subnet, each cluster needs to use a different network address. When you select a different primary IP address for each cluster, NLB automatically ensures that the clusters use unique network addresses. Some network adapters might not allow the built-in network address to be modified. If you experience this issue, you must obtain and install a different network adapter that supports this functionality. </para>
                </listItem>
                <listItem>
                  <para>The <ui>Cluster operation mode</ui> parameters specify whether a multicast MAC address should be used for cluster operations. If multicast is enabled, NLB converts the cluster MAC address that belongs to the cluster adapter into a multicast address. It also ensures that the cluster's primary IP address resolves to this multicast address as part of the ARP protocol. The adapter can now use its original, built-in MAC address that was disabled in unicast mode. </para>
                  <para>In multicast mode, you can also enable Internet Group Management Protocol (IGMP) support, which limits switch flooding by limiting traffic to Network Load Balancing ports only. That is, enabling IGMP support ensures that traffic intended for an NLB cluster passes through only those ports that are serving the cluster hosts and not all switch ports. </para>
                  <para>If you select unicast support, NLB automatically instructs the driver that belongs to the cluster adapter to override the adapter's unique, built-in network address and to change its MAC address to the cluster's MAC address. This is the address used on all cluster hosts. You do not need to manually configure the network adapter to recognize this address. (Note that some network adapters do not support changing their MAC addresses. If you experience this issue, you must install a network adapter that does.)</para>
                </listItem>
              </list>
              <alert class="important">
                <para>NLB does not support a mixed environment of unicast and multicast within a single cluster. Within each cluster, all network adapters in that cluster must be either multicast or unicast. Otherwise, the cluster will not function properly. There is no restriction on the number of network adapters, and different hosts can have a different number of adapters.</para>
              </alert>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Port rules</para>
            </TD>
            <TD colspan="1">
              <para>The <ui>Port Rules</ui> tab shows only the summary of existing port rules. If you click <ui>Add</ui> or <ui>Edit</ui>, the following parameters will be available:</para>
              <list class="bullet">
                <listItem>
                  <para>The <ui>Cluster IP address</ui> parameter specifies the cluster IP address that the port rule should cover. If this parameter is left blank and <ui>All</ui> is selected, the port rule is a global port rule, and it will cover all cluster IP addresses associated with that particular NLB cluster. If a cluster IP address is specified, the port rule overrides any conflicting global port rule for that particular cluster IP address.</para>
                </listItem>
                <listItem>
                  <para>The <ui>Port range</ui> parameter specifies the TCP/UDP port range that a port rule should cover. The default port range is 0 to 65,535. Rules for a single port are encoded as a range having the same starting and ending port numbers.</para>
                </listItem>
                <listItem>
                  <para>The <ui>Protocols</ui> parameter lets you choose the specific TCP/IP protocol that a port rule should cover: TCP, UDP, or both. Only the network traffic for the specified protocol is affected by the rule. Traffic that is not affected by the port rule is handled by the default host.</para>
                </listItem>
                <listItem>
                  <para>For <ui>Filtering mode</ui>, configure the following parameters:</para>
                  <list class="bullet">
                    <listItem>
                      <para>The <ui>Multiple hosts</ui> parameter specifies that multiple hosts in the cluster will handle network traffic for the associated port rule. This filtering mode provides scaled performance and fault tolerance by distributing the network load among multiple hosts. You can specify that the load be equally distributed among the hosts or that each host will handle a specified load weight.</para>
                    </listItem>
                    <listItem>
                      <para>The <ui>Single host</ui> parameter specifies that network traffic for the associated port rule be handled by a single host in the cluster according to the specified handling priority. This filtering mode provides port specific fault tolerance for handling network traffic.</para>
                    </listItem>
                    <listItem>
                      <para>The <ui>Disable this port range</ui> parameter specifies that all network traffic for the associated port rule be blocked. In this case, the NLB driver filters all corresponding network packets or datagrams. This filtering mode lets you block network traffic that is addressed to a specific range of ports.</para>
                    </listItem>
                  </list>
                </listItem>
                <listItem>
                  <para>The <ui>Affinity</ui> parameter is applicable only for the <ui>Multiple hosts</ui> filtering mode.</para>
                  <list class="bullet">
                    <listItem>
                      <para>The <ui>None</ui> option specifies that multiple connections from the same client IP address can be handled by different cluster hosts (there is no client affinity). To allow Network Load Balancing to properly handle IP fragments, you should avoid using <ui>None</ui> when selecting <ui>UDP</ui> or <ui>Both</ui> for your protocol setting.</para>
                    </listItem>
                    <listItem>
                      <para>The <ui>Single</ui> option specifies that NLB should direct multiple requests from the same client IP address to the same cluster host. This is the default setting for <ui>affinity</ui>. You can optionally modify the NLB client affinity to direct all client requests from a TCP/IP Class C address range (instead of a single IP address) to a single cluster host by enabling the <ui>Network</ui> option instead of the <ui>Single</ui> option. This feature ensures that clients that use multiple proxy servers to access the cluster can have their TCP connections directed to the same cluster host. </para>
                    </listItem>
                    <listItem>
                      <para>The <ui>Network</ui> option specifies that NLB direct multiple requests from the same TCP/IP Class C address range to the same cluster host. Enabling <ui>Network</ui> affinity instead of <ui>Single</ui> affinity ensures that clients that use multiple proxy servers to access the cluster have their TCP connections directed to the same cluster host. </para>
                      <para>The use of multiple proxy servers at the client's site causes requests from a single client to appear to originate from different computers. Assuming that all of the client's proxy servers are located within the same address range, <ui>Network</ui> affinity ensures that client sessions are properly handled. If you do not need this capability, use <ui>Single</ui> affinity to maximize scaled performance.</para>
                    </listItem>
                  </list>
                  <para>As an extension to the <ui>Single</ui> and <ui>Network</ui> options, you can configure a time-out setting to preserve client affinity when the configuration of an NLB cluster is changed. This extension also allows clients to keep affinity to a cluster host even if there are no active, existing connections from the client to the host.</para>
                  <para>Enabling <ui>Single</ui> or <ui>Network</ui> affinity ensures that only one cluster host handles all connections that are part of the same client session. This is important if the server application that is running on the cluster host maintains a session state (such as server cookies) between connections.</para>
                  <para>This does not preserve a session state with back-end databases where many different transactions are occurring that involve many different computers. When the connection ends, the session state also ends.</para>
                  <para>Disabling <ui>affinity</ui> allows for improved load balancing because it allows multiple connections from the same client to be handled concurrently by different cluster hosts. To maximize scaled performance, disable the client affinity (by using the <ui>None</ui> option) when it is not needed. However, to allow NLB to properly handle IP fragments, you should avoid using <ui>None</ui> when selecting <ui>UDP</ui> or <ui>Both</ui> for your protocol setting.</para>
                </listItem>
              </list>
              <alert class="important">
                <para>When using NLB to load balance VPN traffic, you must configure the port rules that govern the ports handling the VPN traffic (TCP port 1723 for PPTP/GRE and UDP port 500 for IPSEC/L2TP) to use either <ui>Single</ui> or <ui>Network</ui> affinity.</para>
              </alert>
              <list class="bullet">
                <listItem>
                  <para>The <ui>Load weight</ui> parameter is applicable only for the <ui>Multiple hosts</ui> filtering mode. You can configure this parameter only when you open the port rules dialog box through <ui>Host Properties</ui>. (This parameter is not configurable when you open the port rules dialog box through <ui>Cluster Properties</ui>.) </para>
                  <para>When using the <ui>Multiple hosts</ui> filtering mode, this parameter specifies the relative amount of load-balanced network traffic that this host should handle for the associated port rule. Allowed values range from 0 (zero) to 100. To prevent a host from handling any network traffic, set the load weight to 0 (zero). The actual fraction of traffic handled by each host is computed as the local load weight divided by the sum of all load weights across the cluster.</para>
                  <para>You can specify different load weights for each host in the cluster by using the <ui>Load weight</ui> parameter. You can specify that all hosts distribute the network load equally by using the <ui>Equal load</ui> distribution parameter instead of the <ui>Load weight</ui> parameter.</para>
                </listItem>
                <listItem>
                  <para>The <ui>Handling priority</ui> parameter is applicable only for <ui>Single host</ui> filtering mode. You can configure this parameter only when you open the port rules dialog box through <ui>Host Properties</ui>. (This parameter is not available when you open the port rules dialog box through <ui>Cluster Properties</ui>.) </para>
                  <para>When <ui>Single host</ui> filtering mode is used, the <ui>Handling priority</ui> parameter specifies the local host's priority for handling the network traffic for the associated port rule. The host with the highest handling priority (lowest numerical value) for this rule among the current members of the cluster will handle all of the traffic for this rule. The allowed values range from 1, the highest priority, to the maximum number of hosts allowed (32). This value must be unique for all hosts in the cluster. Although this parameter is displayed in the <ui>Defined port rules</ui> list, you configure this parameter on the <ui>Host Parameters</ui> tab.</para>
                </listItem>
              </list>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Host parameters</para>
            </TD>
            <TD colspan="1">
              <list class="bullet">
                <listItem>
                  <para>The <ui>Priority (Unique host ID)</ui> parameter specifies a unique ID for each host. The host with the lowest numerical priority among the current members of the cluster handles all of the cluster's network traffic that is not covered by a port rule. You can override these priorities or provide load balancing for specific ranges of ports by specifying rules in the <ui>Port rules</ui> tab. </para>
                  <para>If a new host joins the cluster and its priority conflicts with another host in the cluster, the host is not accepted as part of the cluster. The rest of the cluster will continue to handle the traffic. A message describing the issue is written to the Windows event log. </para>
                </listItem>
                <listItem>
                  <para>The <ui>IP address</ui> parameter specifies this host's unique IP address, which is used for network traffic that is not associated with the cluster (for example, specifying Telnet access to a specific host within the cluster). It should be entered in standard Internet dotted notation (for example, w.x.y.z). This IP address is used to individually address each host in the cluster, and it should be unique for each host. The dedicated IP address should always be entered first in TCP/IP properties.</para>
                  <para>NLB references the dedicated IP address only when a single network adapter is used to handle both client-to-cluster traffic and other network traffic that must go specifically to the dedicated IP address. NLB ensures that all traffic to the dedicated IP address is unaffected by the NLB current configuration. This includes when this host is running as part of the cluster and when NLB is disabled due to parameter errors in the registry.</para>
                </listItem>
              </list>
              <alert class="important">
                <para>Typically, both the dedicated IP address and the cluster IP address must also be entered in the <ui>Internet Protocol (TCP/IP) Properties</ui> dialog box. Make sure that the addresses are the same in both places. However, if you are configuring a virtual private network (VPN) load-balancing cluster, you should not configure the dedicated IP address. On a VPN, only the cluster IP address should be present on each of the cluster hosts. The dedicated IP address must be a static IP address—it cannot be a DHCP address.</para>
              </alert>
              <list class="bullet">
                <listItem>
                  <para>The <ui>Subnet mask</ui> parameter denotes the subnet mask for the IP address specified. The mask is entered in standard Internet dotted notation (for example, 255.255.255.0).</para>
                </listItem>
                <listItem>
                  <para>The <ui>Initial host state</ui> parameter specifies whether NLB will start and whether the host will immediately join the cluster when the operating system is started. For example, you might want to start other services manually and in a specific order before starting NLB. Hosts can be commanded to join and leave the cluster dynamically by using the <system>Start</system> and <system>Stop</system> commands in NLB command-line control. If the <ui>Retain suspended state after computer starts</ui> check box is selected, when the host is shut down while in a suspended state, the host will remain suspended when Windows is started.</para>
                </listItem>
              </list>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
  </section>
  <section>
    <title>See also</title>
    <content>
      <list class="bullet">
        <listItem>
          <para>
            <legacyLink xlink:href="bad6f3ac-ab94-425c-8a51-883765dc7f97">Network Load Balancing Overview</legacyLink>
          </para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>