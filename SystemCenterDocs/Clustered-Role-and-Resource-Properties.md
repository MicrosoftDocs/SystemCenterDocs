---
title: Clustered Role and Resource Properties
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 113b5967-f7a4-4038-b583-a9c343dbffd7
---
# Clustered Role and Resource Properties
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This topic describes the user interface (UI) choices that are available on the following tabs in Failover Cluster Manager:</para>
    <list class="bullet">
      <listItem>
        <para>
          <link xlink:href="#BKMK_General">&lt;ClusteredRole&gt; Properties: General Tab</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="#BKMK_Policies">&lt;Resource&gt; Properties: Policies Tab</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="#BKMK_AdvancedPolicies">&lt;Resource&gt; Properties: Advanced Policies Tab</link>
        </para>
      </listItem>
    </list>
  </introduction>
  <section address="BKMK_General">
    <title>&lt;ClusteredRole&gt; Properties: General Tab</title>
    <content>
      <para>The following table describes the UI choices that are available on the <ui>Policies</ui> tab for a clustered role.</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD colspan="1">
              <para>Item</para>
            </TD>
            <TD colspan="1">
              <para>Details</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD colspan="1">
              <para>
                <ui>Preferred Owners</ui>
              </para>
            </TD>
            <TD colspan="1">
              <para>Select nodes from the list, and then use the buttons to list them in order.</para>
              <para>If you want this clustered role to be moved to a particular node whenever that node is available:</para>
              <list class="bullet">
                <listItem>
                  <para>Select the check box for a node and use the buttons to place it at the top of the list.</para>
                </listItem>
                <listItem>
                  <para>On the <ui>Failover</ui> tab, ensure that failback is allowed for this clustered role.</para>
                </listItem>
              </list>
              <para>Even if you clear the check box for a node in the <ui>Preferred Owners</ui> list, the clustered role could fail over to that node for the following reasons:</para>
              <list class="bullet">
                <listItem>
                  <para>You have not specified any preferred owners.</para>
                </listItem>
                <listItem>
                  <para>No node that is a preferred owner is currently online.</para>
                </listItem>
              </list>
              <para>To ensure that a clustered role never fails over to a particular node: </para>
              <list class="ordered">
                <listItem>
                  <para>Select an individual resource in the clustered role. </para>
                </listItem>
                <listItem>
                  <para>Open the <ui>Properties</ui> sheet for that resource. </para>
                </listItem>
                <listItem>
                  <para>Select the <ui>Advanced Policies</ui> tab. </para>
                </listItem>
                <listItem>
                  <para>Configure <ui>Possible Owners</ui>.</para>
                </listItem>
              </list>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
  </section>
  <section address="BKMK_Policies">
    <title>&lt;Resource&gt; Properties: Policies Tab</title>
    <content>
      <para>The following table describes the UI choices that are available on the <ui>Policies</ui> tab for a cluster resource.</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD colspan="1">
              <para>Item</para>
            </TD>
            <TD colspan="1">
              <para>Details</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD colspan="1">
              <para>
                <ui>Period for restarts (mm:ss)</ui>
              </para>
            </TD>
            <TD colspan="1">
              <para>Specify the length of the period (minutes and seconds) during which the Cluster service counts the number of times that a resource has been restarted. </para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>
                <ui>Maximum restarts in the specified period</ui>
              </para>
            </TD>
            <TD colspan="1">
              <para>Specify the number of times that you want the Cluster service to try to restart the resource during the period you specify. If the resource cannot be started after this number of attempts in the specified period, the Cluster service will take actions as specified by other fields on this tab.</para>
              <para>For example, if you specify <ui>3</ui> for <ui>Maximum restarts in the specified period</ui> and <ui>15:00</ui> for the period, the Cluster service attempts to restart the resource three times in a given 15 minute period. If the resource still does not run, instead of trying to restart it a fourth time, the Cluster service will take the actions that you specified in the other fields on this tab.</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>
                <ui>If restart is unsuccessful, fail over all resources in this role</ui>
              </para>
            </TD>
            <TD colspan="1">
              <para>Controls how the Cluster service responds if the maximum number of restarts that you specified fail:</para>
              <list class="bullet">
                <listItem>
                  <para>Select this check box if you want the Cluster service to fail over the clustered role to another node.</para>
                </listItem>
                <listItem>
                  <para>Clear this check box if you want the Cluster service to leave this clustered role running on this node (even if this resource is in a failed state).</para>
                </listItem>
              </list>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>
                <ui>If all the restart attempts fail, begin restarting again after the specified period (hh:mm)</ui>
              </para>
            </TD>
            <TD colspan="1">
              <para>Select this check box if you want the Cluster service to go into an extended waiting period after it attempts the maximum number of restarts on the resource. This extended waiting period is measured in hours and minutes. After the waiting period, the Cluster service will begin another series of restarts. This is true regardless of which node owns the clustered role at that time.</para>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
  </section>
  <section address="BKMK_AdvancedPolicies">
    <title>&lt;Resource&gt; Properties: Advanced Policies Tab</title>
    <content>
      <para>The following table describes the UI choices that are available on the <ui>Advanced Policies</ui> tab for a cluster resource.</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD colspan="1">
              <para>Item</para>
            </TD>
            <TD colspan="1">
              <para>Details</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD colspan="1">
              <para>
                <ui>Possible Owners</ui>
              </para>
            </TD>
            <TD colspan="1">
              <para>Clear the check box for a node only if you want to prevent this resource (and the clustered role that contains this resource) from failing over to that node. Otherwise, leave the boxes selected for all nodes.</para>
              <alert class="note">
                <para>If you select a check box for only one node, this resource (and the clustered role that contains this resource) cannot fail over.</para>
              </alert>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>
                <ui>Basic resource health check interval</ui>
              </para>
            </TD>
            <TD colspan="1">
              <para>Specify how often you want the cluster to perform a basic check to see whether the resource appears to be online. We recommend that you select the <ui>Use standard time period for the resource type</ui> option unless you have a reason to change the interval.</para>
              <alert class="note">
                <para>This health check is also known as the Looks Alive poll.</para>
              </alert>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>
                <ui>Thorough resource health check interval</ui>
              </para>
            </TD>
            <TD colspan="1">
              <para>Specify how often you want the cluster to perform a more thorough check, which looks for indications that the resource is online and functioning properly. We recommend that you select the <ui>Use standard time period for the resource type</ui> option unless you have a reason to change the interval.</para>
              <alert class="note">
                <para>This health check is also known as the Is Alive poll.</para>
              </alert>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>