---
title: How to configure storage on a Hyper-V host cluster in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f5ba36d-4fc3-4852-8dbc-9ef05b20a8c0
---
# How to configure storage on a Hyper-V host cluster in VMM
You can use the following procedure to configure storage on a managed Hyper\-V host cluster in [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)]. The storage must already be provisioned before you can configure it for the cluster.

**Account requirements** To complete this procedure, you must be a member of the Administrator user role or a member of the Delegated Administrator user role where the management scope includes the host group where the Hyper\-V host cluster is located.

### To configure storage on a Hyper\-V host cluster in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]

1.  Make sure you have completed the process of discovering, classifying, and provisioning storage. For more information, see [Prerequisites: creating a host cluster in VMM from existing Windows servers](./Prerequisites--creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md). As described in that topic,make sure you have allocated either storage pools or logical units to the host group \(or parent host group\) of the host cluster.

2.  Open the **Fabric** workspace.

3.  In the **Fabric** pane, expand **Servers** > **All Hosts**.

4.  Locate the Hyper\-V host cluster that you want to configure, right\-click it, and then click **Properties**.

5.  In the *Host Cluster Name* **Properties** dialog box, click a tab:

    -   **Available Storage**: for adding available storage, converting available storage to shared storage \(CSV\), or removing available storage.

    -   **Shared Volumes**: for adding cluster shared volumes \(CSVs\), converting CSVs to available storage, or removing CSVs. The cluster must run at least [!INCLUDE[win8_server_2](./Token/win8_server_2_md.md)] to support CSVs.

6.  Configure storage for the host cluster, using the notes in the following table:

    |Action|Notes|
    |----------|---------|
    |Add available storage or CSVs|-   For a logical unit name, use only alphanumeric characters.<br />-   You cannot change the partition style of a disk that has already been initialized.|
    |Convert available storage to CSVs|-   Make sure that there are no virtual machines on the cluster that have their associated .vhd or .vhdx files located on the storage that you want to convert.<br />-   Convert volumes one at a time.<br />-   After conversion, confirm that the logical unit appears on the **Shared Volumes** tab.|
    |Convert CSVs to available storage|-   Make sure that there are no virtual machines on the cluster that have their associated .vhd or .vhdx files located on the storage that you want to convert. **Caution:**     If you convert shared to available storage, and the storage is being used by virtual machines, serious data loss can result.<br />-   Convert volumes one at a time.<br />-   After conversion, confirm that the logical unit appears on the **Available Storage** tab.|
    |Remove available storage or CSVs|-   If there are virtual machines on the cluster that currently use the storage for their associated .vhd or .vhdx files, the **Remove** option is disabled.|

7.  When you are ready to commit the changes, click **OK**.

## See Also
[Modifying Hyper-V host clusters in VMM](./Modifying-Hyper-V-host-clusters-in-VMM.md)
[Managing Hyper-V hosts and host clusters with VMM](./Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)


