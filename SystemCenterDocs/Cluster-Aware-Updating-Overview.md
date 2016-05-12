---
title: Cluster-Aware Updating Overview
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 700cd500-c335-4138-9678-a6d28dfa8078
---
# Cluster-Aware Updating Overview
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction address="BKMK_INTRO">
    <para>This topic provides an overview of Cluster-Aware Updating (CAU), a feature that automates the software updating process on clustered servers while maintaining availability.</para>
  </introduction>
  <section address="BKMK_OVER">
    <title>Feature description</title>
    <content>
      <para>CAU is an automated feature that enables you to update clustered servers with little or no loss in availability during the update process. During an Updating Run, CAU transparently performs the following tasks:</para>
      <list class="bullet">
        <listItem>
          <para>Puts each node of the cluster into node maintenance mode</para>
        </listItem>
        <listItem>
          <para>Moves the clustered roles off the node</para>
        </listItem>
        <listItem>
          <para>Installs the updates and any dependent updates</para>
        </listItem>
        <listItem>
          <para>Performs a restart if necessary</para>
        </listItem>
        <listItem>
          <para>Brings the node out of maintenance mode</para>
        </listItem>
        <listItem>
          <para>Restores the clustered roles on the node</para>
        </listItem>
        <listItem>
          <para>Moves to update the next node</para>
        </listItem>
      </list>
      <para>For many clustered roles in the cluster, the automatic update process triggers a planned failover. This can cause a transient service interruption for connected clients. However, in the case of continuously available workloads, such as Hyper-V with live migration or file server with SMB Transparent Failover, CAU can coordinate cluster updates with no impact to the service availability.</para>
      <alert class="note">
        <para>The CAU feature is only compatible with <token>winblue_server_Token> and <token>win8_server_Token> failover clusters and the clustered roles that are supported on those versions.</para>
      </alert>
    </content>
  </section>
  <section address="BKMK_APP" expanded="true">
    <title>Practical applications</title>
    <content>
      <list class="bullet">
        <listItem>
          <para>CAU reduces service outages in clustered services, reduces the need for manual updating workarounds, and makes the end-to-end cluster updating process more reliable for the administrator. When the CAU feature is used in conjunction with continuously available cluster workloads, such as continuously available file servers (file server workload with SMB Transparent Failover) or Hyper-V, the cluster updates can be performed with zero impact to service availability for clients.</para>
        </listItem>
        <listItem>
          <para>CAU facilitates the adoption of consistent IT processes across the enterprise. Updating Run Profiles can be created for different classes of failover clusters and then managed centrally on a file share to ensure that CAU deployments throughout the IT organization apply updates consistently, even if the clusters are managed by different lines-of-business or administrators.</para>
        </listItem>
        <listItem>
          <para>CAU can schedule Updating Runs on regular daily, weekly, or monthly intervals to help coordinate cluster updates with other IT management processes. </para>
        </listItem>
        <listItem>
          <para>CAU provides an extensible architecture to update the cluster software inventory in a cluster-aware fashion. This can be used by publishers to coordinate the installation of software updates that are not published to Windows Update or Microsoft Update or that are not available from Microsoft, for example, updates for non-Microsoft device drivers.</para>
        </listItem>
        <listItem>
          <para>CAU self-updating mode enables a "cluster in a box" appliance (a set of clustered physical machines, typically packaged in one chassis) to update itself. Typically, such appliances are deployed in branch offices with minimal local IT support to manage the clusters. Self-updating mode offers great value in these deployment scenarios.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section expanded="true">
    <title>Important functionality</title>
    <content>
      <para>The following is a description of important CAU functionality:</para>
      <list class="bullet">
        <listItem>
          <para>A user interface (UI) and a set of <token>wps_Token> cmdlets that you can use to preview, apply, monitor, and report on the updates</para>
        </listItem>
        <listItem>
          <para>An end-to-end automation of the cluster-updating operation (an Updating Run), orchestrated by one or more Update Coordinator computers</para>
        </listItem>
        <listItem>
          <para>A default plug-in that integrates with the existing Windows Update Agent (WUA) and Windows Server Update Services (WSUS) infrastructure in <token>winblue_server_Token> or <token>win8_server_Token> to apply important Microsoft updates</para>
        </listItem>
        <listItem>
          <para>A second plug-in that can be used to apply Microsoft hotfixes, and that can be customized to apply non-Microsoft updates</para>
        </listItem>
        <listItem>
          <para>Updating Run Profiles that you configure with settings for Updating Run options, such as the maximum number of times that the update will be retried per node. Updating Run Profiles enable you to rapidly reuse the same settings across Updating Runs and easily share the update settings with other failover clusters.</para>
        </listItem>
        <listItem>
          <para>An extensible architecture that supports new plug-in development to coordinate other node-updating tools across the cluster, such as custom software installers, BIOS updating tools, and network adapter or host bus adapter (HBA) updating tools.</para>
        </listItem>
      </list>
      <para>CAU can coordinate the complete cluster updating operation in two modes:</para>
      <list class="bullet">
        <listItem>
          <para>
            <embeddedLabel>Self-updating mode</embeddedLabel>  For this mode, the CAU clustered role is configured as a workload on the failover cluster that is to be updated, and an associated update schedule is defined. The cluster updates itself at scheduled times by using a default or custom Updating Run profile. During the Updating Run, the CAU Update Coordinator process starts on the node that currently owns the CAU clustered role, and the process sequentially performs updates on each cluster node. To update the current cluster node, the CAU clustered role fails over to another cluster node, and a new Update Coordinator process on that node assumes control of the Updating Run. In self-updating mode, CAU can update the failover cluster by using a fully automated, end-to-end updating process. An administrator can also trigger updates on-demand in this mode, or simply use the remote-updating approach if desired. In self-updating mode, an administrator can get summary information about an Updating Run in progress by connecting to the cluster and running the <system>Get-CauRun</system> Windows PowerShell cmdlet.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Remote-updating mode</embeddedLabel>   For this mode, a remote computer, which is called an Update Coordinator, is configured with the CAU tools. The Update Coordinator is not a member of the cluster that is updated during the Updating Run. From the remote computer, the administrator triggers an on-demand Updating Run by using a default or custom Updating Run profile. Remote-updating mode is useful for monitoring real-time progress during the Updating Run, and for clusters that are running on Server Core installations.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_SOFT" expanded="true">
    <title>Hardware and software requirements</title>
    <content>
      <para>To use CAU in self-updating mode, the Failover Clustering Tools must be installed on each cluster node.</para>
      <para>To enable remote-updating mode for a <token>winblue_server_Token> failover cluster, you must install the Failover Clustering Tools from the RSAT on a local or a remote computer that is running <token>winblue_server_Token> or <token>winblue_client_Token> and that has network connectivity to the failover cluster.</para>
      <alert class="note">
        <list class="bullet">
          <listItem>
            <para>You must use the Failover Clustering Tools from the <token>winblue_server_Token> RSAT to remotely manage updates for a <token>winblue_server_Token> failover cluster. You can also use the <token>winblue_server_Token> RSAT to remotely manage updates on a <token>win8_server_Token> failover cluster.</para>
          </listItem>
          <listItem>
            <para>To use CAU only in remote-updating mode, installation of the Failover Clustering Tools on the cluster nodes is not required. However, certain CAU features will not be available. For more information, see <externalLink><linkText>Requirements and Best Practices for Cluster-Aware Updating</linkText><linkUri>http://go.microsoft.com/fwlink/p/?LinkId=234906</linkUri></externalLink>.</para>
          </listItem>
          <listItem>
            <para>Unless you are using CAU only in self-updating mode, the computer on which the CAU tools are installed and that coordinates the updates cannot be a member of the failover cluster.</para>
          </listItem>
        </list>
      </alert>
      <para>To enable self-updating mode, the CAU clustered role must also be added to the failover cluster. To do this by using the CAU UI, under <ui>Cluster Actions</ui>, use the <ui>Configure Self-Updating Options</ui> action. Alternatively, run the <externalLink><linkText>Add-CauClusterRole</linkText><linkUri>http://technet.microsoft.com/library/hh847235.aspx</linkUri></externalLink> <token>wps_Token> cmdlet.</para>
      <para>To uninstall CAU, uninstall the Failover Clustering feature or Failover Clustering Tools by using Server Manager, <token>wps_Token> cmdlets, or the DISM command-line tools.</para>
    </content>
    <sections>
      <section>
        <title>Additional requirements and best practices</title>
        <content>
          <para>To ensure that CAU can update the cluster nodes successfully, and for additional guidance for configuring your failover cluster environment to use CAU, you can run the CAU Best Practices Analyzer.</para>
          <para>For detailed requirements and best practices for using CAU, and information about running the CAU Best Practices Analyzer, see <externalLink><linkText>Requirements and Best Practices for Cluster-Aware Updating</linkText><linkUri>http://go.microsoft.com/fwlink/p/?LinkId=234906</linkUri></externalLink>.</para>
        </content>
      </section>
      <section expanded="true">
        <title>Starting CAU</title>
        <content>
          <procedure>
            <title>To start the CAU UI from Server Manager</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Start Server Manager.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Do one of the following:</para>
                  <list class="bullet">
                    <listItem>
                      <para>On the <ui>Tools</ui> menu, click <ui>Cluster-Aware Updating</ui>.</para>
                    </listItem>
                    <listItem>
                      <para>If one or more cluster nodes, or the cluster, is added to Server Manager, on the <ui>All Servers</ui> page, right-click the name of a node (or the name of the cluster), and then click <ui>Update Cluster</ui>.</para>
                    </listItem>
                  </list>
                </content>
              </step>
            </steps>
          </procedure>
        </content>
      </section>
    </sections>
  </section>
  <section address="BKMK_LINKS" expanded="true">
    <title>See also</title>
    <content>
      <para>The following links provide more information about using CAU.</para>
      <list class="bullet">
        <listItem>
          <para>
            <externalLink>
              <linkText>Requirements and Best Practices for Cluster-Aware Updating</linkText>
              <linkUri>http://go.microsoft.com/fwlink/p/?LinkId=234906</linkUri>
            </externalLink>
          </para>
        </listItem>
        <listItem>
          <para>
            <externalLink>
              <linkText>Cluster-Aware Updating: Frequently Asked Questions</linkText>
              <linkUri>http://technet.microsoft.com/library/hh831367.aspx</linkUri>
            </externalLink>
          </para>
        </listItem>
        <listItem>
          <para>
            <externalLink>
              <linkText>Advanced Options and Updating Run Profiles for CAU</linkText>
              <linkUri>http://go.microsoft.com/fwlink/p/?LinkId=234907</linkUri>
            </externalLink>
          </para>
        </listItem>
        <listItem>
          <para>
            <externalLink>
              <linkText>How CAU Plug-ins Work</linkText>
              <linkUri>http://go.microsoft.com/fwlink/p/?LinkId=235333</linkUri>
            </externalLink>
          </para>
        </listItem>
        <listItem>
          <para>
            <externalLink>
              <linkText>Cluster-Aware Updating Cmdlets in Windows PowerShell</linkText>
              <linkUri>http://go.microsoft.com/fwlink/p/?LinkId=237675</linkUri>
            </externalLink>
          </para>
        </listItem>
        <listItem>
          <para>
            <externalLink>
              <linkText>Cluster-Aware Updating Plug-in Reference</linkText>
              <linkUri>http://msdn.microsoft.com/library/hh418084.aspx</linkUri>
            </externalLink>
          </para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>

