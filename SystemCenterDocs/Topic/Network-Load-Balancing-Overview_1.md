---
title: Network Load Balancing Overview_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5fae303-e627-4345-b54c-ba0d6d6e1746
---
# Network Load Balancing Overview_1
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This topic provides an overview of the Network Load Balancing (NLB) feature. By managing two or more servers as a single virtual cluster, NLB enhances the availability and scalability of Internet server applications such as those used on web, FTP, firewall, proxy, virtual private network (VPN), and other mission-critical servers. This topic describes the NLB feature and provides links to additional guidance about creating, configuring, and managing NLB clusters. </para>
  </introduction>
  <section address="BKMK_OVER">
    <title>Feature description</title>
    <content>
      <para>The NLB feature distributes traffic across several servers by using the TCP/IP networking protocol. By combining two or more computers that are running applications into a single virtual cluster, NLB provides reliability and performance for web servers and other mission-critical servers.</para>
      <para>The servers in an NLB cluster are called <newTerm>hosts</newTerm>, and each host runs a separate copy of the server applications. NLB distributes incoming client requests across the hosts in the cluster. You can configure the load that is to be handled by each host. You can also add hosts dynamically to the cluster to handle increased load. NLB can also direct all traffic to a designated single host, which is called the <newTerm>default host</newTerm>.</para>
      <para>NLB allows all of the computers in the cluster to be addressed by the same set of IP addresses, and it maintains a set of unique, dedicated IP addresses for each host. For load-balanced applications, when a host fails or goes offline, the load is automatically redistributed among the computers that are still operating. When it is ready, the offline computer can transparently rejoin the cluster and regain its share of the workload, which allows the other computers in the cluster to handle less traffic. </para>
    </content>
  </section>
  <section address="BKMK_APP">
    <title>Practical applications</title>
    <content>
      <para>NLB is useful for ensuring that stateless applications, such as web servers running Internet Information Services (IIS), are available with minimal downtime, and that they are scalable (by adding additional servers as the load increases). The following sections describe how NLB supports high availability, scalability, and manageability of the clustered servers that run these applications.</para>
    </content>
    <sections>
      <section>
        <title>High availability</title>
        <content>
          <para>A high availability system reliably provides an acceptable level of service with minimal downtime. To provide high availability, NLB includes built-in features that can automatically:</para>
          <list class="bullet">
            <listItem>
              <para>Detect a cluster host that fails or goes offline, and then recover.</para>
            </listItem>
            <listItem>
              <para>Balance the network load when hosts are added or removed.</para>
            </listItem>
            <listItem>
              <para>Recover and redistribute the workload within ten seconds.</para>
            </listItem>
          </list>
        </content>
      </section>
      <section>
        <title>Scalability</title>
        <content>
          <para>Scalability is the measure of how well a computer, service, or application can grow to meet increasing performance demands. For NLB clusters, scalability is the ability to incrementally add one or more systems to an existing cluster when the overall load of the cluster exceeds its capabilities. To support scalability, you can do the following with NLB:</para>
          <list class="bullet">
            <listItem>
              <para>Balance load requests across the NLB cluster for individual TCP/IP services.</para>
            </listItem>
            <listItem>
              <para>Support up to 32 computers in a single cluster.</para>
            </listItem>
            <listItem>
              <para>Balance multiple server load requests (from the same client or from several clients) across multiple hosts in the cluster.</para>
            </listItem>
            <listItem>
              <para>Add hosts to the NLB cluster as the load increases, without causing the cluster to fail.</para>
            </listItem>
            <listItem>
              <para>Remove hosts from the cluster when the load decreases.</para>
            </listItem>
            <listItem>
              <para>Enable high performance and low overhead through a fully pipelined implementation. Pipelining allows requests to be sent to the NLB cluster without waiting for a response to a previous request.</para>
            </listItem>
          </list>
        </content>
      </section>
      <section>
        <title>Manageability</title>
        <content>
          <para>To support manageability, you can do the following with NLB:</para>
          <list class="bullet">
            <listItem>
              <para>Manage and configure multiple NLB clusters and the cluster hosts from a single computer by using NLB Manager or the NLB <token>wps_2</token> cmdlets. </para>
            </listItem>
            <listItem>
              <para>Specify the load balancing behavior for a single IP port or group of ports by using port management rules. </para>
            </listItem>
            <listItem>
              <para>Define different port rules for each website. If you use the same set of load-balanced servers for multiple applications or websites, port rules are based on the destination virtual IP address (using virtual clusters).</para>
            </listItem>
            <listItem>
              <para>Direct all client requests to a single host by using optional, single-host rules. NLB routes client requests to a particular host that is running specific applications. </para>
            </listItem>
            <listItem>
              <para>Block undesired network access to certain IP ports. </para>
            </listItem>
            <listItem>
              <para>Enable Internet Group Management Protocol (IGMP) support on the cluster hosts to control switch port flooding (where incoming network packets are sent to all ports on the switch) when operating in multicast mode.</para>
            </listItem>
            <listItem>
              <para>Start, stop, and control NLB actions remotely by using Windows PowerShell commands or scripts.</para>
            </listItem>
            <listItem>
              <para>View the Windows Event Log to check NLB events. NLB logs all actions and cluster changes in the event log.</para>
            </listItem>
          </list>
        </content>
      </section>
    </sections>
  </section>
  <section>
    <title>Important functionality</title>
    <content>
      <alert class="note">
        <para> NLB functionality is the same as in <token>win8_server_2</token> and <token>nextref_server_7</token>. </para>
      </alert>
      <para>NLB is installed as a standard Windows networking driver component. Its operations are transparent to the TCP/IP networking stack. The following figure shows the relationship between NLB and other software components in a typical configuration:</para>
      <mediaLink>
        <image xlink:href="52bae903-4a12-482b-a3c2-1ead4dcf0cab" />
      </mediaLink>
      <para> </para>
      <para>The NLB features include the following:</para>
      <list class="bullet">
        <listItem>
          <para>Requires no hardware changes to run.</para>
        </listItem>
        <listItem>
          <para>Provides Network Load Balancing Tools to configure and manage multiple clusters and all of the hosts from a single remote or local computer.</para>
        </listItem>
        <listItem>
          <para>Enables clients to access the cluster by using a single, logical Internet name and virtual IP address, which is known as the cluster IP address (it retains individual names for each computer). NLB allows multiple virtual IP addresses for multihomed servers.</para>
          <alert class="note">
            <para>NLB does not require servers to be multihomed to have multiple virtual IP addresses in the case of virtual clusters.</para>
          </alert>
        </listItem>
        <listItem>
          <para>Enables NLB to be bound to multiple network adapters, which enables you to configure multiple independent clusters on each host. Support for multiple network adapters differs from virtual clusters in that virtual clusters allow you to configure multiple clusters on a single network adapter.</para>
        </listItem>
        <listItem>
          <para>Requires no modifications to server applications so that they can run in an NLB cluster.</para>
        </listItem>
        <listItem>
          <para>Can be configured to automatically add a host to the cluster if that cluster host fails and is subsequently brought back online. The added host can start handling new server requests from clients.</para>
        </listItem>
        <listItem>
          <para>Enables you to take computers offline for preventive maintenance without disturbing the cluster operations on the other hosts.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_HARD">
    <title>Hardware requirements </title>
    <content>
      <para>To run an NLB cluster, the following are hardware requirements:</para>
      <list class="bullet">
        <listItem>
          <para>All hosts in the cluster must reside on the same subnet.</para>
        </listItem>
        <listItem>
          <para>There is no restriction on the number of network adapters on each host, and different hosts can have a different number of adapters.</para>
        </listItem>
        <listItem>
          <para>Within each cluster, all network adapters must be either multicast or unicast. NLB does not support a mixed environment of multicast and unicast within a single cluster.</para>
        </listItem>
        <listItem>
          <para>If you use the unicast mode, the network adapter that is used to handle client-to-cluster traffic must support changing its media access control (MAC) address.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_SOFT">
    <title>Software requirements </title>
    <content>
      <para>To run an NLB cluster, the following are software requirements:</para>
      <list class="bullet">
        <listItem>
          <para>Only TCP/IP can be used on the adapter for which NLB is enabled on each host. Do not add any other protocols (for example, IPX) to this adapter.</para>
        </listItem>
        <listItem>
          <para>The IP addresses of the servers in the cluster must be static.</para>
        </listItem>
      </list>
      <alert class="note">
        <para>NLB does not support Dynamic Host Configuration Protocol (DHCP). NLB disables DHCP on each interface that it configures.</para>
      </alert>
    </content>
  </section>
  <section address="BKMK_INSTALL">
    <title>Server Manager information</title>
    <content>
      <para>In Server Manager, use the Add Roles and Features Wizard to add the Network Load Balancing feature. Optionally you can install the Network Load Balancing Tools to manage a local or remote NLB cluster. The tools include Network Load Balancing Manager and the NLB <token>wps_2</token> cmdlets. For more information about installing features, see <externalLink><linkText>Install or Uninstall Roles, Role Services, or Features</linkText><linkUri>http://go.microsoft.com/fwlink/p/?LinkID=239563</linkUri></externalLink>.</para>
      <para>To open Network Load Balancing Manager in Server Manager, click <ui>Tools</ui>, and then click <ui>Network Load Balancing Manager</ui>.</para>
    </content>
  </section>
  <section address="BKMK_LINKS">
    <title>See also</title>
    <content>
      <para>The following table provides links to additional information about the NLB feature that is available on the web. </para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>Content type</para>
            </TD>
            <TD>
              <para>References</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>
                <embeddedLabel>Deployment</embeddedLabel>
              </para>
            </TD>
            <TD>
              <para>
                <externalLink>
                  <linkText>Network Load Balancing Deployment Guide</linkText>
                  <linkUri>http://technet.microsoft.com/library/cc754833(WS.10).aspx</linkUri>
                </externalLink>
              </para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <embeddedLabel>Operations</embeddedLabel>
              </para>
            </TD>
            <TD>
              <para>
                <externalLink>
                  <linkText>Managing Network Load Balancing Clusters</linkText>
                  <linkUri>http://technet.microsoft.com/library/cc753954(WS.10).aspx</linkUri>
                </externalLink> | <externalLink><linkText>Setting Network Load Balancing Parameters</linkText><linkUri>http://technet.microsoft.com/library/cc731619(WS.10).aspx</linkUri></externalLink> | <externalLink><linkText>Controlling Hosts on Network Load Balancing Clusters</linkText><linkUri>http://technet.microsoft.com/library/cc770870(WS.10).aspx</linkUri></externalLink></para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <embeddedLabel>Troubleshooting</embeddedLabel>
              </para>
            </TD>
            <TD>
              <para>
                <externalLink>
                  <linkText>Troubleshooting Network Load Balancing Clusters</linkText>
                  <linkUri>http://technet.microsoft.com/library/cc732592(WS.10).aspx</linkUri>
                </externalLink> | <externalLink><linkText>NLB Cluster Events and Errors</linkText><linkUri>http://technet.microsoft.com/library/cc731678(WS.10).aspx</linkUri></externalLink></para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <embeddedLabel>Tools and settings</embeddedLabel>
              </para>
            </TD>
            <TD>
              <para>
                <externalLink>
                  <linkText>Network Load Balancing Windows PowerShell cmdlets</linkText>
                  <linkUri>http://technet.microsoft.com/library/hh801274.aspx</linkUri>
                </externalLink>
              </para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <embeddedLabel>Community resources</embeddedLabel>
              </para>
            </TD>
            <TD>
              <para>
                <externalLink>
                  <linkText>High Availability (Clustering) Forum</linkText>
                  <linkUri>http://go.microsoft.com/fwlink/p/?LinkId=230641</linkUri>
                </externalLink> | <externalLink><linkText>Failover Clustering and Network Load Balancing Team Blog</linkText><linkUri>http://blogs.msdn.com/b/clustering/</linkUri></externalLink></para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <embeddedLabel>Related technologies</embeddedLabel>
              </para>
            </TD>
            <TD>
              <para>
                <externalLink>
                  <linkText>Web Server (IIS)</linkText>
                  <linkUri>http://technet.microsoft.com/windowsserver/dd448617</linkUri>
                </externalLink> | <legacyLink xlink:href="912908f6-4c97-43d3-a442-7e11b62dda8a">NIC Teaming Overview</legacyLink></para>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>