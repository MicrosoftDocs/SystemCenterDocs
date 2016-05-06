---
title: Advanced Options and Updating Run Profiles for CAU
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a62dc1ea-f89e-4132-a550-c1c362517e86
---
# Advanced Options and Updating Run Profiles for CAU
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This topic describes Updating Run options that can be configured for a CAU Updating Run. These advanced options can be configured when you use either the CAU UI or the CAU <token>wps_2</token> cmdlets to apply updates or to configure self-updating options. </para>
    <para>Most configuration settings can be saved as an XML file called an Updating Run Profile and reused for later Updating Runs. The default values for the Updating Run options that are provided by CAU can also be used in many cluster environments.</para>
    <para>For information about additional options that you can specify for each Updating Run and about Updating Run Profiles, see the following sections later in this topic:</para>
    <list class="bullet">
      <listItem>
        <para>
          <link xlink:href="#BKMK_runtime">Options that you specify when you request an Updating Run</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="#BKMK_profile">Use Updating Run Profiles</link>
        </para>
      </listItem>
    </list>
  </introduction>
  <section>
    <title>Options that can be set in an Updating Run Profile</title>
    <content>
      <para>The following table lists options that you can set in a CAU Updating Run Profile. </para>
      <alert class="important">
        <para>To set the <ui>PreUpdateScript</ui> or <ui>PostUpdateScript</ui> option, ensure that <token>wps_2</token> 4.0 and .NET Framework 4.5 are installed and that <token>wps_2</token> remoting is enabled on each node in the cluster. For more information, see <legacyLink xlink:href="c4c50fef-cfa1-4844-8921-deeb7653d8ba#BKMK_NODE_CONFIG">Configure nodes for remote management</legacyLink> in <legacyLink xlink:href="c4c50fef-cfa1-4844-8921-deeb7653d8ba">Requirements and Best Practices for Cluster-Aware Updating [WS8]</legacyLink>.</para>
      </alert>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD colspan="1">
              <para>Option</para>
            </TD>
            <TD>
              <para>Default value</para>
            </TD>
            <TD colspan="1">
              <para>Details</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>
                <ui>StopAfter</ui>
              </para>
            </TD>
            <TD>
              <para>Unlimited time</para>
            </TD>
            <TD>
              <para>Time in minutes after which the Updating Run will be stopped if it has not completed.</para>
              <alert class="note">
                <para>If you specify a pre-update or a post-update <token>wps_2</token> script, the entire process of running scripts and performing updates must be complete within the <ui>StopAfter</ui> time limit.</para>
              </alert>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <ui>WarnAfter</ui>
              </para>
            </TD>
            <TD>
              <para>By default, no warning appears</para>
            </TD>
            <TD>
              <para>Time in minutes after which a warning will appear if the Updating Run (including a pre-update script and a post-update script, if they are configured) has not completed. </para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>
                <ui>MaxRetriesPerNode</ui>
              </para>
            </TD>
            <TD>
              <para>3</para>
            </TD>
            <TD colspan="1">
              <para>Maximum number of times that the update process (including a pre-update script and a post-update script, if they are configured) will be retried per node. The maximum is 64.</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>
                <ui>MaxFailedNodes</ui>
              </para>
            </TD>
            <TD>
              <para>For most clusters, an integer that is approximately one-third of the number of cluster nodes</para>
            </TD>
            <TD colspan="1">
              <para>Maximum number of nodes on which updating can fail, either because the nodes fail or the Cluster service stops running. If one more node fails, the Updating Run is stopped.</para>
              <para>The valid range of values is 0 to 1 less than the number of cluster nodes. </para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <ui>RequireAllNodesOnline</ui>
              </para>
            </TD>
            <TD>
              <para>None</para>
            </TD>
            <TD>
              <para>Specifies that all nodes must be online and reachable before updating begins.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <ui>RebootTimeoutMinutes</ui>
              </para>
            </TD>
            <TD>
              <para>15</para>
            </TD>
            <TD>
              <para>Time in minutes that CAU will allow for restarting a node (if a restart is necessary) and starting all auto-start services. If the restart process does not complete within this time, the Updating Run on that node is marked as failed.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <ui>PreUpdateScript</ui>
              </para>
            </TD>
            <TD>
              <para>None</para>
            </TD>
            <TD>
              <para>The path and file name for a <token>wps_2</token> script to run on each node before updating begins, and before the node is put into maintenance mode. The file name extension must be <system>.ps1</system>, and the total length of the path plus file name must not exceed 260 characters. As a best practice, the script should be located on a disk in cluster storage, or at a highly available network file share, to ensure that it is always accessible to all of the cluster nodes. If the script is located on a network file share, ensure that you configure the file share for Read permission for the Everyone group, and restrict write access to prevent tampering with the files by unauthorized users.</para>
              <para>If you specify a pre-update script, be sure that settings such as the time limits (for example, <ui>StopAfter</ui>) are configured to allow the script to run successfully. These limits span the entire process of running scripts and installing updates, not just the process of installing updates.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <ui>PostUpdateScript</ui>
              </para>
            </TD>
            <TD>
              <para>None</para>
            </TD>
            <TD>
              <para>The path and file name for a <token>wps_2</token> script to run after updating completes (after the node leaves maintenance mode). The file name extension must be <system>.ps1</system> and the total length of the path plus file name must not exceed 260 characters. As a best practice, the script should be located on a disk in cluster storage, or at a highly available network file share, to ensure that it is always accessible to all of the cluster nodes. If the script is located on a network file share, ensure that you configure the file share for Read permission for the Everyone group, and restrict write access to prevent tampering with the files by unauthorized users.</para>
              <para>If you specify a post-update script, be sure that settings such as the time limits (for example, <ui>StopAfter</ui>) are configured to allow the script to run successfully. These limits span the entire process of running scripts and installing updates, not just the process of installing updates.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <ui>ConfigurationName</ui>
              </para>
            </TD>
            <TD>
              <para>This setting only has an effect if you run scripts.</para>
              <para>If you specify a pre-update script or a post-update script, but you do not specify a <ui>ConfigurationName</ui>, the default session configuration for <token>wps_2</token> (Microsoft.PowerShell) is used.</para>
            </TD>
            <TD>
              <para>Specifies the <token>wps_2</token> session configuration that defines the session in which scripts (specified by <ui>PreUpdateScript</ui> and <ui>PostUpdateScript</ui>) are run, and can limit the commands that can be run.</para>
              <para />
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <ui>CauPluginName</ui>
              </para>
            </TD>
            <TD>
              <para>
                <system>Microsoft.WindowsUpdatePlugin</system> </para>
            </TD>
            <TD>
              <para>Plug-in that you configure Cluster-Aware Updating to use to preview updates or perform an Updating Run. For more information, see <legacyLink xlink:href="847b571b-12b3-473c-953f-75a5a1f51333">How CAU Plug-ins Work [WS8]</legacyLink>.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <ui>CauPluginArguments</ui>
              </para>
            </TD>
            <TD>
              <para>None</para>
            </TD>
            <TD>
              <para>A set of <placeholder>name=value</placeholder> pairs (arguments) for the updating plug-in to use, for example:</para>
              <para>
                <system>Domain=Domain.local</system>
              </para>
              <para>These <placeholder>name=value</placeholder> pairs must be meaningful to the plug-in that you specify in <ui>CauPluginName</ui>.</para>
              <para>To specify an argument using the CAU UI, type the <placeholder>name</placeholder>, press the Tab key, and then type the corresponding <placeholder>value</placeholder>. Press the Tab key again to provide the next argument. Each <placeholder>name</placeholder> and <placeholder>value</placeholder> are automatically separated with an equal (=) sign. Multiple pairs are automatically separated with semicolons.</para>
              <para>For the default <system>Microsoft.WindowsUpdatePlugin</system> plug-in, no arguments are needed. However, you can specify an optional argument, for example to specify a standard Windows Update Agent query string to filter the set of updates that are applied by the plug-in. For a <placeholder>name</placeholder>, use <system>QueryString</system>, and for a <placeholder>value</placeholder>, enclose the full query in quotation marks. </para>
              <para>For more information, see <legacyLink xlink:href="847b571b-12b3-473c-953f-75a5a1f51333">How CAU Plug-ins Work [WS8]</legacyLink>.</para>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
  </section>
  <section address="BKMK_runtime">
    <title>Options that you specify when you request an Updating Run</title>
    <content>
      <para>The following table lists options (other than those in an Updating Run Profile) that you can specify when you request an Updating Run. For information about options that you can set in an Updating Run Profile, see the preceding table.</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD colspan="1">
              <para>Option</para>
            </TD>
            <TD>
              <para>Default value</para>
            </TD>
            <TD colspan="1">
              <para>Details</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>
                <ui>ClusterName</ui>
              </para>
            </TD>
            <TD>
              <para>None</para>
              <alert class="note">
                <para>This option must be set only when the CAU UI is not run on a failover cluster node, or you want to reference a failover cluster different from where the CAU UI is run.</para>
              </alert>
</TD>
            <TD>
              <para>NetBIOS name of the cluster on which to perform the Updating Run. </para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <ui>Credential</ui>
              </para>
            </TD>
            <TD>
              <para>Current account credentials</para>
            </TD>
            <TD>
              <para>Administrative credentials for the target cluster on which the Updating Run will be performed. You may already have the necessary credentials if you start the CAU UI (or open a <token>wps_2</token> session, if you are using the CAU <token>wps_2</token> cmdlets) from an account that has administrator rights and permissions on the cluster.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <ui>NodeOrder</ui>
              </para>
            </TD>
            <TD>
              <para>By default, CAU starts with the node that owns the smallest number of clustered roles, then progresses to the node that has the second smallest number, and so on.</para>
            </TD>
            <TD>
              <para>Names of the cluster nodes in the order that they should be updated (if possible). </para>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
  </section>
  <section address="BKMK_profile">
    <title>Use Updating Run Profiles</title>
    <content>
      <para>Each Updating Run can be associated with a specific Updating Run Profile. The default Updating Run Profile is stored in the %windir%\cluster folder. If you are using the CAU UI in remote-updating mode, you can specify an Updating Run Profile at the time that you apply updates, or you can use the default Updating Run profile. If you are using CAU in self-updating mode, you can import the settings from a specified Updating Run Profile when you configure the self-updating options. In both cases, you can override the displayed values for the Updating Run options according to your needs. If you want, you can save the Updating Run options as an Updating Run Profile with the same file name or a different file name. The next time that you apply updates or configure self-updating options, CAU automatically selects the Updating Run Profile that was previously selected.</para>
      <para>An existing Updating Run Profile can also be modified, or a new Updating Run Profile can be created, by selecting <ui>Create or modify Updating Run Profile</ui> in the CAU UI. </para>
      <para>
        <mediaLinkInline>
          <image xlink:href="eda3e676-68d6-4a56-90af-dd29179cfd9b" />
        </mediaLinkInline>
        <embeddedLabel>
          <token>wps_proc_title</token>
        </embeddedLabel>
      </para>
      <para>You can import the settings from an Updating Run Profile when you run the <system>Invoke-CauRun</system>, <system>Add-CauClusterRole</system>, or <system>Set-CauClusterRole</system> cmdlet.</para>
      <para>The following example performs a scan and a full Updating Run on the cluster named <placeholder>CONTOSO-FC1</placeholder>, using the Updating Run options that are specified in <placeholder>C:\Windows\Cluster\DefaultParameters.xml</placeholder>. Default values are used for the remaining cmdlet parameters. </para>
      <code language="powershell">$MyRunProfile = Import-Clixml C:\Windows\Cluster\DefaultParameters.xml
Invoke-CauRun –ClusterName CONTOSO-FC1 @MyRunProfile </code>
      <para>By using an Updating Run Profile, you can update a failover cluster in a repeatable fashion with consistent settings for exception management, time bounds, and other operational parameters. Because these settings are typically specific to a class of failover clusters—such as “All Microsoft SQL Server clusters”, or “My business-critical clusters”—you might want to name each Updating Run Profile according to the class of Failover Clusters it will be used with. In addition, you might want to manage the Updating Run Profile on a file share that is accessible to all of the failover clusters of a specific class in your IT organization.</para>
      <alert class="note">
        <list class="bullet">
          <listItem>
            <para>An Updating Run Profile does not store cluster-specific information such as administrative credentials. If you are using CAU in self-updating mode, the Updating Run Profile also does not store the self-updating schedule information. This makes it possible to share an Updating Run Profile across all failover clusters in a specified class.</para>
          </listItem>
          <listItem>
            <para>If you configure self-updating options using an Updating Run Profile and later modify the profile with different values for the Updating Run options, the self-updating configuration does not change automatically. To apply the new Updating Run settings, you must configure the self-updating options again.</para>
          </listItem>
        </list>
      </alert>
    </content>
  </section>
  <section>
    <title>See also</title>
    <content>
      <list class="bullet">
        <listItem>
          <para>
            <legacyLink xlink:href="a8e6dfbb-9d98-4130-86ac-9f6f00241e02">Cluster-Aware Updating Overview [WS8overview]</legacyLink>
          </para>
        </listItem>
        <listItem>
          <para>
            <legacyLink xlink:href="16e9bb53-ae89-4d69-9a6b-fb8201bbf189">Cluster-Aware Updating Cmdlets in Windows PowerShell [cmdlet stub]</legacyLink>
          </para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>