---
title: Failover Clustering Overview
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a9d9ac62-f6d5-4c93-9738-d95fbf7a9b84
---
# Failover Clustering Overview
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction address="BKMK_INTRO">
    <para>This topic provides an overview of the Failover Clustering feature. Failover clusters provide high availability and scalability to many server workloads. These include server applications such as Microsoft Exchange Server, Hyper-V, Microsoft SQL Server, and file servers. The server applications can run on physical servers or virtual machines. This topic describes the Failover Clustering feature and provides links to additional guidance about creating, configuring, and managing failover clusters that can scale to 64 physical nodes and to 8,000 virtual machines.</para>
  </introduction>
  <section address="BKMK_OVER">
    <title>Feature description</title>
    <content>
      <para>A failover cluster is a group of independent computers that work together to increase the availability and scalability of clustered roles. The clustered servers (called nodes) are connected by physical cables and by software. If one or more of the cluster nodes fail, other nodes begin to provide service (a process known as failover). In addition, the clustered roles are proactively monitored to verify that they are working correctly. If they are not working, they are restarted or moved to another node. Failover clusters also provide Cluster Shared Volumes (CSV) functionality that provides a consistent, distributed namespace that clustered roles can use to access shared storage from all nodes. With the Failover Clustering feature, users experience a minimum of disruptions in service.</para>
      <para>Failover clusters are managed by using the Failover Cluster Manager snap-in and the Failover Clustering <token>wps_Token> cmdlets. File shares on file server clusters can additionally be managed by using the tools in File and Storage Services. </para>
    </content>
  </section>
  <section address="BKMK_APP" expanded="true">
    <title>Practical applications</title>
    <content>
      <list class="bullet">
        <listItem>
          <para>Highly available or continuously available file share storage for applications such as Microsoft SQL Server and Hyper-V virtual machines</para>
        </listItem>
        <listItem>
          <para>Highly available clustered roles that run on physical servers or on virtual machines that are installed on servers running Hyper-V </para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_NEW" expanded="true">
    <title>New and changed functionality</title>
    <content>
      <para>New and changed functionality in Failover Clustering supports increased scalability, easier management, faster failover, and more flexible architectures for failover clusters.</para>
      <para>For information about what is new, see <externalLink><linkText>What's New in Failover Clustering in Windows Server 2012 R2</linkText><linkUri>http://technet.microsoft.com/library/dn265972.aspx</linkUri></externalLink> and <externalLink><linkText>What's New in Failover Clustering in Windows Server 2012</linkText><linkUri>http://technet.microsoft.com/library/hh831414.aspx</linkUri></externalLink>.</para>
    </content>
  </section>
  <section address="BKMK_HARD" expanded="true">
    <title>Hardware requirements </title>
    <content>
      <para>A failover cluster solution must meet the following hardware requirements:</para>
      <list class="bullet">
        <listItem>
          <para>Hardware components in the failover cluster solution must meet the qualifications for the Certified for <token>winblue_server_Token> or <token>win8_server_Token> logo.</para>
        </listItem>
        <listItem>
          <para>Storage must be attached to the nodes in the cluster, if the solution is using shared storage.</para>
        </listItem>
        <listItem>
          <para>Device controllers or appropriate adapters for the storage can be Serial Attached SCSI (SAS), Fibre Channel, Fibre Channel over Ethernet (FcoE), or iSCSI.</para>
        </listItem>
        <listItem>
          <para>The complete cluster configuration (servers, network, and storage) must pass all tests in the Validate a Configuration Wizard.</para>
        </listItem>
      </list>
      <alert class="note">
        <para>In the network infrastructure that connects your cluster nodes, avoid having single points of failure.</para>
      </alert>
      <para>For more information about hardware compatibility, see the <externalLink><linkText>Windows Server Catalog</linkText><linkUri>http://go.microsoft.com/fwlink/p/?linkid=139145</linkUri></externalLink>.</para>
      <para>For more information about the correct configuration of the servers, network, and storage for a failover cluster, see the following topics:</para>
      <list class="bullet">
        <listItem>
          <para>
            <externalLink>
              <linkText>Failover Clustering Hardware Requirements and Storage Options</linkText>
              <linkUri>http://technet.microsoft.com/library/jj612869.aspx</linkUri>
            </externalLink>
          </para>
        </listItem>
        <listItem>
          <para>
            <externalLink>
              <linkText>Validating Hardware for a Failover Cluster</linkText>
              <linkUri>http://technet.microsoft.com/library/jj134244.aspx</linkUri>
            </externalLink>
          </para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_SOFT" expanded="true">
    <title>Software requirements </title>
    <content>
      <para>You must follow the hardware manufacturers' recommendations for firmware updates and software updates. Usually, this means that the latest firmware and software updates have been applied. Occasionally, a manufacturer might recommend specific updates other than the latest updates.</para>
    </content>
  </section>
  <section address="BKMK_LINKS" expanded="true">
    <title>See also</title>
    <content>
      <para>For more information about the Failover Clustering feature, see the following topics:</para>
      <list class="bullet">
        <listItem>
          <para>
            <externalLink>
              <linkText>Failover Clustering node in the TechNet Library</linkText>
              <linkUri>http://technet.microsoft.com/library/hh831579.aspx</linkUri>
            </externalLink>
          </para>
        </listItem>
        <listItem>
          <para>
            <externalLink>
              <linkText>High Availability (Clustering) Forum</linkText>
              <linkUri>http://go.microsoft.com/fwlink/p/?LinkId=230641</linkUri>
            </externalLink>
          </para>
        </listItem>
        <listItem>
          <para>
            <externalLink>
              <linkText>Failover Clustering and Network Load Balancing Team Blog</linkText>
              <linkUri>http://blogs.msdn.com/b/clustering/</linkUri>
            </externalLink>
          </para>
        </listItem>
        <listItem>
          <para>
            <externalLink>
              <linkText>Failover Clustering Cmdlets in Windows PowerShell</linkText>
              <linkUri>http://go.microsoft.com/fwlink/p/?LinkId=233200</linkUri>
            </externalLink>
          </para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>

