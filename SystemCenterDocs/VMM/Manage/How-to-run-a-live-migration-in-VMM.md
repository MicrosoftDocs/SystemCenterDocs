---
title: How to run a live migration in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5027e2b-85f5-466d-a261-044280b2d27a
---
# How to run a live migration in VMM
[!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)] provides live migration support between stand\-alone Hyper\-V hosts, or cluster hosts that have the Live Migration feature enabled. This topic describes the following migration procedures:

-   [Live migration of a virtual machine between two stand-alone hosts](#BKMK_Standalone)—This procedure describes how to migrate a virtual machine from one stand\-alone Hyper\-V host to another stand\-alone Hyper\-V host. Note that the virtual machine configuration files and virtual hard disk must be located on a Server Message Block \(SMB\) 3.0 file share.

-   [Live migration of a virtual machine between hosts in two clusters](#BKMK_Cluster)—This procedure describes how to migrate a virtual machine from a host that runs in one cluster to a host that runs in a different cluster. Note that when you run a live migration between two clusters, the virtual machine temporarily loses its high availability status. Therefore, a host failure during the migration causes the virtual machine to become unavailable. For live migration between clusters, you should use SMB 3.0 file shares as the storage location. Because the storage does not have to be migrated, the time in which high availability status cannot be guaranteed is very short.

-   [Live migration of storage between two locations on a stand-alone host](#BKMK_Storage)—This procedure describes how to migrate storage only.

-   [Concurrent live migrations](#BKMK_Concurrent)—This procedure provides an overview of how to run multiple concurrent migrations and describes how to verify that concurrent migrations run as expected.

-   [Faster live migrations](#BKMK_Faster)—This procedure provides an overview of how to perform a faster live migration.

## <a name="BKMK_Standalone"></a>Live migration of a virtual machine between two stand\-alone hosts
Use the following procedure to perform a live migration between two stand\-alone hosts.

#### To perform live migration of a virtual machine between two stand\-alone hosts

1.  Open the **VMs and Services** workspace.

2.  In the **VMs and Services** pane, expand **All Hosts**. Locate, and then click the stand\-alone source host from which you want to migrate a virtual machine.

    For example, click the host **StandAlone1** in the host group **Stand\-Alone HG**.

3.  In the **VMs** pane, click the running virtual machine that you want to migrate. Start the machine if it is not running.

    For example, click the virtual machine **StandAloneVM1**.

4.  On the **Virtual Machine** tab, in the **Virtual Machine** group, click **Migrate Virtual Machine** to start the **Migrate Virtual Machine Wizard**.

5.  On the **Select Host** page, review the destination hosts and their associated transfer types.

    The **Live** transfer type appears if both hosts are configured to connect to the same SMB 3.0 file share.

6.  Click the destination host where the transfer type is **Live**, and then click **Next**.

    For example, click the host **StandAlone2**.

7.  On the **Summary** page, click **Move**.

8.  To track the job status, open the **Jobs** workspace.

9. To verify that the virtual machine was migrated, in the **VMs and Services** workspace, in the **VMs and Services** pane, locate, and then click the destination host. In the **VMs** pane, verify that the virtual machine is listed with a status of **Running**.

## <a name="BKMK_Cluster"></a>Live migration of a virtual machine between hosts in two clusters
Use the following procedure to perform a live migration between two cluster hosts.

#### To perform live migration of a virtual machine between hosts in two clusters

1.  Open the **VMs and Services** workspace.

2.  In the **VMs and Services** pane, expand **All Hosts**. Locate, and then click the cluster node from which you want to try the live migration of a highly available virtual machine.

    For example, click the cluster node **Cluster1Node1**.

3.  In the **VMs** pane, click the running virtual machine that you want to migrate. Start the machine if it is not running.

    For example, click the virtual machine **HAVM1**.

4.  On the **Virtual Machine** tab, in the **Virtual Machine** group, click **Migrate Virtual Machine** to start the **Migrate Virtual Machine Wizard**.

5.  On the **Select Host** page, review the destination hosts and their associated transfer types.

    The **Live** transfer type is available for any destination cluster nodes that are configured to connect to the same SMB 3.0 file share on which the virtual machine was originally created.

6.  Click a cluster node that is in a different host cluster, and then click **Next**.

    For example, click the cluster node **Cluster2Node1**.

7.  On the **Summary** page, click **Move**.

8.  To track the job status, open the **Jobs** workspace.

9. To verify that the virtual machine was migrated, in the **VMs and Services** workspace, in the **VMs and Services** pane, locate, and then click the destination host. In the **VMs** pane, verify that the virtual machine is listed with a status of **Running**.

## <a name="BKMK_Storage"></a>Live migration of storage between two locations on a stand\-alone host
Use the following procedure to perform a live migration between locations on stand\-alone hosts. You can move the entire virtual machine, which includes virtual hard disks \(VHDs\) and configuration information, or move only specific VHDs to a different location.

#### To perform live migration of storage between two locations on a stand\-alone host

1.  Open the **VMs and Services** workspace.

2.  In the **VMs and Services** pane, expand **All Hosts**. Locate, and then click the stand\-alone host where the virtual machine resides.

    For example, click the host **StandAlone2** in the host group **Stand\-Alone HG**.

3.  In the **VMs** pane, click the running virtual machine on which you want to try live storage migration. Start the virtual machine if it is not running.

    For example, click the virtual machine **StandAloneVM1**.

4.  On the **Virtual Machine** tab, in the **Virtual Machine** group, click **Migrate Storage** to start the **Migrate Virtual Machine Wizard**.

5.  On the **Select Path** page, in the **Storage location** list, click one of the default storage locations on the host. Or, click **Browse** to view all possible storage destinations, click the destination SMB 3.0 file share or location on the local hard disk, and then click **OK**.

    > [!IMPORTANT]
    > If you specify an SMB 3.0 file share in the **Storage location** list, ensure that you use the fully qualified domain name \(FQDN\) of the destination server in the share path. For example, instead of *\\\\fileserver1\\smbshare*, use *\\\\fileserver1.contoso.com\\smbshare*.

6.  Optionally, select the **Add this path to the list of default storage locations on the host** check box, and then click **Next**.

7.  On the **Summary** page, click **Move**.

8.  To track the job status, open the **Jobs** workspace.

## <a name="BKMK_Concurrent"></a>Concurrent live migrations
To run live migrations concurrently, perform any of the procedures in this topic on multiple virtual machines so that two migrations occur at the same time on the same host. In the user interface, you cannot multi\-select virtual machines to perform live migrations. Instead, you must manually start each migration. You can specify how many concurrent migrations to run. The default setting is two, which is the number of simultaneous live migration and storage migrations that are enabled in Hyper\-V. For example, a host can participate in one outgoing live migration plus one incoming, two outgoing live migrations, or two incoming live migrations. Live migrations and live storage migrations are independent. Therefore, you can perform two live migrations and two live storage migrations simultaneously. [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] considers live virtual machine and storage migration \(live VSM\) as one live migration and one storage migration. Use the following procedure to view concurrent migrations.

#### To view concurrent migrations

1.  Open Hyper\-V Manager on the host, and then in the **Actions** pane, click **Hyper\-V Settings**. Under **Server**, you can view **Live Migrations** and **Storage Migrations** settings.

2.  In the **Jobs** workspace, verify that the migrations occur simultaneously.

## <a name="BKMK_Faster"></a>Faster live migrations
On Hyper\-V hosts, live migration speed can be increased by using compression, by using SMB as the transport, or by using both. The compression method uses algorithms that reduce the data that is transmitted over the wire. The SMB method can allow for faster data transfer.

By default, faster live migration is enabled to use the compression method. You can disable, enable, or change the method of faster live migration by changing the live storage migration settings, either at the Hyper\-V host level, or for each live migration instance.

#### To change live migration settings

1.  Open Hyper\-V Manager on the host, and then in the **Actions** pane, click **Hyper\-V Settings**. Under **Server**, click  **Live Migration**, and then click **Advanced Features**.

2.  In the **Migration settings** page, under **Live migration settings**, do one of the following:

    -   To disable faster live migration, click **Standard live migration**.

    -   To use compression for faster live migration, click **Use compression**.

    -   To use SMB for faster live migration, click **Use SMB as Transport**.

## See Also
[Overview: migrating virtual machines and storage](Overview--migrating-virtual-machines-and-storage.md)
[Migrating virtual machines and storage in VMM](Migrating-virtual-machines-and-storage-in-VMM.md)
[Managing virtual machines with VMM](assetId:///d403f964-cff2-4caa-978d-b9dc08a39594)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


