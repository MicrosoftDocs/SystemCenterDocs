---
title: How to assign file shares on a Scale-Out File Server to a Hyper-V host or cluster in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bf1a333d-0772-49c4-8cac-171bcfb79a72
---
# How to assign file shares on a Scale-Out File Server to a Hyper-V host or cluster in VMM
On a Scale\-Out File Server in [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)], after file shares have been created, assign them to a Hyper\-V host or host cluster. This configures the necessary permissions. For information about steps to take before and after assigning file shares to hosts and host clusters, see [Overview: configuring storage using Scale-Out File Servers in VMM](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md).

This topic contains two procedures:

-   [Assign shares on a Scale-Out File Server to a Hyper-V host cluster](How-to-assign-file-shares-on-a-Scale-Out-File-Server-to-a-Hyper-V-host-or-cluster-in-VMM.md#BKMK_cluster)

-   [Assign shares on a Scale-Out File Server to a stand-alone Hyper-V host](How-to-assign-file-shares-on-a-Scale-Out-File-Server-to-a-Hyper-V-host-or-cluster-in-VMM.md#BKMK_standalone)

## <a name="BKMK_cluster"></a>Assign file shares on a Scale\-Out File Server to a Hyper\-V host cluster
Use this procedure for working with a Hyper\-V host cluster.

#### To assign file shares on a Scale\-Out File Server to a Hyper\-V host cluster

1.  Confirm that the Scale\-Out File Server is in the same domain as the host cluster.

2.  Open the **Fabric** workspace.

3.  In the **Fabric** pane, expand **Servers** > **All Hosts**, and navigate to the host group that contains the Hyper\-V host cluster.

4.  In the **Hosts** pane, right\-click one of the cluster nodes \(not the cluster itself\), and then click **Properties**.

5.  In the *Host Name* **Properties** dialog box, click the **Host Access** tab.

6.  In the **Run As account** box, configure the account settings. Note the following:

    > [!NOTE]
    > By default, the Run As account that was used to add the host to [!INCLUDE[vmm12short](Token/vmm12short_md.md)] is listed. If you want to change the Run As account, click **Browse**, and then select an existing Run As account, or click **Create Run As Account** to create a new account. Do not use the same account that you used for the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] service account. You must use the same Run As account on all cluster nodes.

7.  Repeat steps 4 through 6 on each node of the host cluster.

8.  After you have verified the host management Run As account on each cluster node, in the **Fabric** pane, right\-click the host cluster \(not the cluster nodes\) and then click **Properties**.

9. In the *Cluster Name* **Properties** dialog box, click the **File Share Storage** tab.

10. In the **File Share Storage** pane, click **Add**.

11. In **File share path**, select the file share on the Scale\-Out File Server, and then click **OK**.

12. Click **OK** to apply the changes.

    > [!TIP]
    > To confirm that the cluster has access, open the **Jobs** workspace to view the job status. To view the access status, free space, and total capacity for the share, open the host cluster properties again, and then click the **File Share Storage** tab.

## <a name="BKMK_standalone"></a>Assign file shares on a Scale\-Out File Server to a stand\-alone Hyper\-V host
Use this procedure for working with a stand\-alone Hyper\-V host. If you are working with a cluster, see [Assign shares on a Scale-Out File Server to a Hyper-V host cluster](How-to-assign-file-shares-on-a-Scale-Out-File-Server-to-a-Hyper-V-host-or-cluster-in-VMM.md#BKMK_cluster), earlier in this topic.

#### To assign file shares on a Scale\-Out File Server to a stand\-alone Hyper\-V host

1.  Confirm that the Scale\-Out File Server is in the same domain as the Hyper\-V host.

2.  Open the **Fabric** workspace.

3.  In the **Fabric** pane, expand **Servers** > **All Hosts**, and navigate to the host group that contains the Hyper\-V host.

4.  In the **Hosts** pane, right\-click the host, and then click **Properties**.

5.  In the **Properties** dialog box, click the **Host Access** tab.

6.  In the **Run As account** box, configure the account settings. Note the following:

    -   By default, the Run As account that was used to add the host to [!INCLUDE[vmm12short](Token/vmm12short_md.md)] is listed. If you want to change the Run As account, click **Browse**, and then select an existing Run As account, or click **Create Run As Account** to create a new account. You cannot use the same account that you used for the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] service account.

    -   If you used a domain account for the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] service account, add the domain account to the local Administrators group on the file server.

    -   If you used the local system account for the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] service account, add the computer account for the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] management server to the local Administrators group on the file server. For example, for a [!INCLUDE[vmm12short](Token/vmm12short_md.md)] management server that is named **VMMServer01**, add the computer account **VMMServer01$**.

    -   Any host or host cluster that accesses the SMB 3.0 file share must have been added to [!INCLUDE[vmm12short](Token/vmm12short_md.md)] by using a Run As account. [!INCLUDE[vmm12short](Token/vmm12short_md.md)] automatically uses this Run As account to access the SMB 3.0 file share.

        > [!NOTE]
        > If you specified explicit user credentials when you added a host or host cluster, you can remove the host or cluster from [!INCLUDE[vmm12short](Token/vmm12short_md.md)], and then add it again by using a Run As account.

7.  In the *Host Name* **Properties** dialog box, click the **Storage** tab.

8.  On the toolbar, click **Add** > **Add File Share**.

9. In **File share path**, select the file share on the Scale\-Out File Server, and then click **OK**.

    > [!TIP]
    > To confirm that the host has access, open the **Jobs** workspace to view the job status. Or, open the host properties again, and then click the **Storage** tab. Under **File Shares**, click the SMB 3.0 file share. Verify that a green check mark appears next to **Access to file share**.

## See Also
[How to create a Run As account in VMM](How-to-create-a-Run-As-account-in-VMM.md)
[Overview: configuring storage using Scale-Out File Servers in VMM](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md)
[Configuring storage using Scale-Out File Servers in VMM](Configuring-storage-using-Scale-Out-File-Servers-in-VMM.md)


