---
title: How to add an existing server to a host cluster in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ea976dc-f64c-4a78-858f-f18e33eb3acf
---
# How to add an existing server to a host cluster in VMM
Use these procedures to add  nodes to host clusters that Virtual Machine Manager \(VMM\) manages:

-   [Bring a node under management by VMM if you already used Failover Cluster Manager to add the node](How-to-add-an-existing-server-to-a-host-cluster-in-VMM.md#BKMK_fcm)

-   [Use VMM to add an existing server to a Hyper-V host cluster or Scale-Out File Server cluster](How-to-add-an-existing-server-to-a-host-cluster-in-VMM.md#BKMK_vmm)

If you want to add a bare\-metal computer as a new node, see [How to add a bare-metal computer to a host cluster in VMM](How-to-add-a-bare-metal-computer-to-a-host-cluster-in-VMM.md).

## <a name="BKMK_fcm"></a>To bring a node under VMM management if you already used Failover Cluster Manager to add the node to the cluster

1.  Open the **Fabric** workspace.

2.  Expand **Servers** > **All Hosts**, and then locate and expand the host cluster.

3.  Right\-click the host with a status of **Pending**, and then click **Add to Host Cluster**.

## <a name="BKMK_vmm"></a>To use VMM to add an existing server to a Hyper\-V host cluster

1.  As needed, review [Prerequisites: creating a host cluster in VMM from existing Windows servers](Prerequisites--creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md). A server to be added to the cluster must meet the same basic requirements as the servers that are in the cluster.

    > [!NOTE]
    > You can add a Windows Server Technical Preview node to a Windows Server 2012 R2 cluster. The cluster continues to function as a Windows Server 2012 R2 cluster, in mixed mode. For more information, see the [Server Operating Systems](https://technet.microsoft.com/library/dn997307.aspx) requirements.

    For Hyper\-V host clusters, the hosts you want to add must already be under management by VMM. For more information, see the topics listed in [Adding Windows servers as Hyper-V hosts or host clusters in VMM](Adding-Windows-servers-as-Hyper-V-hosts-or-host-clusters-in-VMM.md).

2.  Open the **Fabric** workspace.

3.  In the **Fabric** pane, expand **Servers** > **All Hosts**, and locate the host cluster. Right\-click it and then click **Add Cluster Node**.

4.  In the **Add Nodes Wizard**, fill in the pages as follows:

    |Page|Information to enter for a host cluster|
    |--------|-------------------------------------------|
    |**Resource Type**|-   Click **Browse** and then select or create the Run As account that will be used to add nodes to the cluster. Then click **OK**.<br />    The account that you use must have administrative permissions on the hosts that will become cluster nodes, and must belong to the same domain as the existing host cluster.<br />-   Ensure that **Existing servers running a Windows Server operating system** is selected.<br />-   If you do not require support from Microsoft for this cluster, you can select **Skip cluster validation**.|
    |**Select Hosts**|From the list of available hosts, select the hosts to add to the cluster. You can select multiple hosts by using the CTRL key, or a range by using SHIFT.<br /><br />If the list of hosts is not what you expect, cancel the wizard, and view the host group that the cluster is in. Ensure that the hosts you want to add are also in that host group, and that they are in a functioning state.|

5.  On the **Summary** page, confirm the settings and then click **Finish**.

    Depending on settings, the **Jobs** dialog box might appear, and you can verify that the job has a status of **Complete**.

6.  When the job completes, verify the cluster status. Expand **Servers** > **All Hosts**, and then locate and click the host cluster. In the **Hosts** pane, in the **Host Status** column, verify that the nodes are **OK**.

    > [!NOTE]
    > To view detailed status information for a host cluster, including a link to the cluster validation test report, right\-click the cluster, click **Properties**, and then click the **Status** tab.
    > 
    > For a host cluster, you can perform cluster validation at any time by right\-clicking the host cluster and then clicking **Validate Cluster**. Cluster validation begins immediately.

## See Also
[Creating a host cluster in VMM from existing Windows servers](Creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md)
[Deploying Hyper-V hosts or host clusters from bare metal with VMM](Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)
[Managing Hyper-V hosts and host clusters with VMM](Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


