---
title: How to create a Scale-Out File Server in VMM using existing servers
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab69213b-ffdd-4dec-bb06-a98860eac788
---
# How to create a Scale-Out File Server in VMM using existing servers
You can use [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)] to  create a Scale\-Out File Server from existing Windows servers. .

> [!NOTE]
> Before beginning this procedure, review [Prerequisites: creating a Scale-Out File Server in VMM from existing servers](Prerequisites--creating-a-Scale-Out-File-Server-in-VMM-from-existing-servers.md)

### To create a Scale\-Out File Server using existing Windows servers

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, click **Servers**.

3.  On the **Home** tab, in the **Create** group, click **Create** > **File Server Cluster**.

4.  Fill in the wizard pages as follows:

    |Page|Information to enter|
    |--------|------------------------|
    |**General Configuration**|<ul><li>Specify a **Cluster name**, a **Scale\-Out File Server name**, and **Cluster IP addresses** \(if needed\).</li><li>If the existing servers are running [!INCLUDE[winthreshold_server_2](../../Token/winthreshold_server_2_md.md)], choose a **Storage configuration**:<br /><br /><ul><li>**Shared storage**.</li><li>**Storage attached directly to each cluster node \(Storage Spaces Direct\)**.<br />                                        For information about this configuration, see [Storage Spaces Direct in Windows Server Technical Preview](https://technet.microsoft.com/library/mt126109.aspx).</li></ul></li></ul>|
    |**Resource Type**|-   Ensure that **Existing servers running a Windows Server operating system** is selected.<br />-   Click **Browse** and then select or create the Run As account that will be used to create the cluster. Then click **OK**.<br />    The account that you use must have administrative permissions on the servers that will become cluster nodes, and must belong to the same domain as those servers. Also, the account requires **Create Computer objects** permission in the container that is used for Computer accounts in the domain. For more information, see the account prerequisites listed in[Create a Failover Cluster](http://technet.microsoft.com/library/dn505754.aspx#BKMK_ClusPrereq).<br />-   The **Skip cluster validation** option appears, if **Shared storage** was selected on the previous page of the wizard. If you do not require support from Microsoft for this cluster, you can skip cluster validation. **Note:**     You cannot skip cluster validation for a cluster using Storage Spaces Direct.|
    |**Select Computers**|Type the fully qualified domain name \(FQDN\), NetBIOS name, or IP address of a server that you want to add to the cluster, and then click **Add**. Repeat this process to add more servers.|

5.  On the **Summary** page, confirm the settings, and then click **Finish** to create the cluster and to bring it under [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] management.

    Depending on settings, the **Jobs** dialog box might appear. Make sure that all steps in the job have a status of **Completed**, and then close the dialog box.

6.  To confirm that the cluster was added, follow these steps:

    1.  Open the **Fabric** workspace.

    2.  In the **Fabric** pane, expand **Storage**, and then expand **File Servers**.

    3.  Verify that the name of the new Scale\-Out File Server cluster appears in the File Servers pane, and that its status is **OK**.

After the wizard closes, you can review the properties by right\-clicking the Scale\-Out File Server and then clicking **Properties**. For information about additional configuration steps you can take with the Scale\-Out File Server, see:

-   [Overview: configuring storage using Scale-Out File Servers in VMM](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md)

-   [How to set a disk witness for a Scale-Out File Server quorum in VMM](How-to-set-a-disk-witness-for-a-Scale-Out-File-Server-quorum-in-VMM.md)

## See Also
[Deploying Hyper-V hosts or host clusters from bare metal with VMM](Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)
[Configuring storage using Scale-Out File Servers in VMM](Configuring-storage-using-Scale-Out-File-Servers-in-VMM.md)
[How to add an existing Scale-Out File Server to storage in VMM](How-to-add-an-existing-Scale-Out-File-Server-to-storage-in-VMM.md)
[Creating a Scale-Out File Server in VMM from existing Windows servers](Creating-a-Scale-Out-File-Server-in-VMM-from-existing-Windows-servers.md)
[Managing Scale-Out File Servers with VMM](Managing-Scale-Out-File-Servers-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


