---
title: How to add an existing server to a Scale-Out File Server in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c272a03-f15a-482e-b9e5-10ffd5dfccf8
---
# How to add an existing server to a Scale-Out File Server in VMM
Use these procedures to add  nodes to Scale\-out File Servers that [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] manages:

-   [Bring a node under management by VMM if you already used Failover Cluster Manager to add the node](../Topic/How-to-add-an-existing-server-to-a-host-cluster-in-VMM.md#BKMK_fcm)

-   [Use VMM to add an existing server to a Hyper-V host cluster or Scale-Out File Server cluster](../Topic/How-to-add-an-existing-server-to-a-host-cluster-in-VMM.md#BKMK_vmm)

If you want to add a bare\-metal computer as a new node, see [How to add a bare-metal computer to a Scale-Out File Server in VMM](../Topic/How-to-add-a-bare-metal-computer-to-a-Scale-Out-File-Server-in-VMM.md).

## <a name="BKMK_fcm"></a>To bring a node under [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management if you already used Failover Cluster Manager to add the node to the Scale\-Out File Server

1.  Open the **Fabric** workspace.

2.  Expand **Storage** > **File Servers** and then locate the Scale\-Out File Server in the results pane.

3.  Right\-click the file server, click **Properties**, and look for nodes labeled **Pending VMM agent deployment**. Click **Add**, specify the pending node, and then click **OK**.

## <a name="BKMK_vmm"></a>To use [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] to add an existing server to a Scale\-Out File Server

1.  As needed, review [Prerequisites: creating a Scale-Out File Server in VMM from existing servers](../Topic/Prerequisites--creating-a-Scale-Out-File-Server-in-VMM-from-existing-servers.md). A server to be added to the cluster must meet the same basic requirements as the servers that are in the cluster.

2.  Open the **Fabric** workspace.

3.  In the **Fabric** pane, expand **Storage** > **File Servers**, and in the **File Servers** pane, locate the Scale\-Out File Server cluster. Right\-click it and then click **Add File Server Nodes**.

4.  In the **Add Nodes Wizard**, fill in the pages as follows:

    |Page|Information to enter for a Scale\-Out File Server cluster|
    |--------|-------------------------------------------------------------|
    |**Resource Type**|-   Ensure that **Existing servers running a Windows Server operating system** is selected.<br />-   The **Skip cluster validation** option appears, unless this cluster uses Storage Spaces Direct. If the option appears and you do not require support for this cluster from Microsoft, you can skip validation.|
    |**Select Computers**|Type the fully qualified domain name \(FQDN\), NetBIOS name, or IP address of a server that you want to add to the cluster, and then click **Add**. Repeat this process to add more servers.|

5.  On the **Summary** page, confirm the settings and then click **Finish**.

    Depending on settings, the **Jobs** dialog box might appear, and you can verify that the job has a status of **Complete**.

6.  When the job completes, verify the cluster status. Expand **Storage** > **File Servers**, and then locate and click the cluster. In the **File Servers** pane, verify that the status of the cluster is **OK**.

    If you added a node to a cluster configured with Storage Spaces Direct, you also added one or more disks to the cluster. If the disks have not been added into your storage pools, see [How to create or modify a storage pool on a Scale-Out File Server in VMM](../Topic/How-to-create-or-modify-a-storage-pool-on-a-Scale-Out-File-Server-in-VMM.md).

## See Also
[Creating a Scale-Out File Server in VMM from existing Windows servers](../Topic/Creating-a-Scale-Out-File-Server-in-VMM-from-existing-Windows-servers.md)
[Managing Scale-Out File Servers with VMM](../Topic/Managing-Scale-Out-File-Servers-with-VMM.md)
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)
[Managing storage resources and capacity with VMM](../Topic/Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)

