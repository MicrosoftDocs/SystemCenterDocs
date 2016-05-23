---
title: How to upgrade a Hyper-V host cluster to Windows Server 2016 Technical Preview
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b90e0e52-a56a-4a75-b0de-4ba85b48ffde
---
# How to upgrade a Hyper-V host cluster to Windows Server 2016 Technical Preview
Use the following procedure to upgrade a [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]\-managed  [!INCLUDE[winblue_server_2](../../Token/winblue_server_2_md.md)] cluster to [!INCLUDE[winthreshold_server_2](../../Token/winthreshold_server_2_md.md)]. Before you begin, be sure to review the prerequisites listed in [Upgrading Windows Server 2012 R2 host clusters to Windows Server 2016 Technical Preview in VMM](Upgrading-Windows-Server-2012-R2-host-clusters-to-Windows-Server-2016-Technical-Preview-in-VMM.md).

### To upgrade a [!INCLUDE[winblue_server_2](../../Token/winblue_server_2_md.md)] host cluster to [!INCLUDE[winthreshold_server_2](../../Token/winthreshold_server_2_md.md)]

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers** > **All Hosts**, and locate the host cluster. Right\-click it and then click **Upgrade Cluster**.

3.  On the **Nodes** page, click the nodes that you want to upgrade. To upgrade the entire cluster at once, click **Select All**. Then click **Physical computer profile**, and click the physical computer profile for the cluster nodes. Click **Next**.

4.  On the **BMC Configuration** page, configure the following:

    1.  Next to the **BMC Run As account** box, click **Browse**, select a Run As account that has permissions to access the BMC, and then click **OK**. For example, if you had a Run As account called **BMC Administrator**, you could select that account.

        If you do not already have a Run As account, click **Browse**, and then in the **Select a Run As Account** dialog box, click **Create Run As Account**.

    2.  In the **Out\-of\-band management protocol** list, click the protocol that your BMCs use.

        > [!NOTE]
        > If you want to use Data Center Management Interface \(DCMI\), click **Intelligent Platform Management Interface \(IPMI\)**. Although DCMI 1.0 is not listed, it is supported.

    3.  For **Out of band management port**, ensure that the correct port is selected.

    Then click **Next**.

5.  On the **Deployment Customization** page, review the list of nodes to upgrade. The wizard displays the configuration of each node. If the wizard was not able to determine all of the required information for a node, it displays a **Missing settings** alert for that node.  For example, if the nodes were not provisioned by [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] using its bare\-metal provisioning process, the BMC settings may not be complete. In addition, if you want to change the configuration of one or more nodes, you can do so from this page.

    In the list of nodes on the left of the pane, click the node you want to check. Check the following configuration areas:

    -   **Computer name and BMC information**.

        1.  If the BMC has not been configured, click **BMC IP address** and type the IP address.

        2.  If you want to change the name of the node, click **Computer name** and then type a new name.

            > [!NOTE]
            > Do not clear **Skip Active Directory check for this computer name** unless you are changing the name of the node and you want to make sure that the name has not already been used.

    -   **Network adapter configuration**.

        1.  For the node you are configuring, click a network adapter \(on the left\). You can leave the displayed configuration unchanged, or fill in more information by clicking the button on the right, labeled either with **Configure** or with an ellipsis \(**...**\).

        2.  If you click the button, in the **Network Adapter IP Configuration** box, you can specify the following:

            -   **MAC address\(host clusters only—management NIC\)**: If this is the management NIC for a host cluster, and you want to configure it as a virtual network adapter, type a MAC address.

                > [!NOTE]
                > This is not the MAC address of the BMC. It is the MAC address of the management NIC, which [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] uses to communicate with the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] management server.

            -   **Specify static IP settings for this network adapter**: If you check this box, select a logical network and \(if applicable in that logical network\) an IP subnet. If the selected IP subnet includes IP address pool, you can check **Obtain an IP address corresponding to the selected subnet**. Otherwise, type an IP address that is in within the logical network or its subnet.

                > [!IMPORTANT]
                > If you select an IP subnet, make sure that it corresponds to the physical location where you are deploying the hosts and to the network that the adapter is connected to. Otherwise, deployment may fail.

        3.  Repeat the configuration process for each network adapter in the node.

    -   Repeat the entire process for each node in the list. When you have filled in needed information for all the nodes, click **Next**.

6.  On the **Summary** page, confirm the settings, and then click **Finish** to upgrade the cluster nodes.

    Depending on your settings, the **Jobs** dialog box might appear. Make sure that all steps in the job reach the **Completed** status, and then close the dialog box.

    If the wizard finishes the node upgrades successfully and all of the cluster nodes are running [!INCLUDE[winthreshold_server_2](../../Token/winthreshold_server_2_md.md)], the wizard updates the cluster functional level to [!INCLUDE[winthreshold_server_2](../../Token/winthreshold_server_2_md.md)].

> [!NOTE]
> To view detailed status information for a host cluster, including a link to the cluster validation test report, right\-click the cluster, click **Properties**, and then click the **Status** tab.
> 
> On a host cluster, you can perform cluster validation at any time. To do this, click the cluster and then on the ribbon, click **Validate Cluster**. Cluster validation begins immediately.

## See Also
[Upgrading Windows Server 2012 R2 host clusters to Windows Server 2016 Technical Preview in VMM](Upgrading-Windows-Server-2012-R2-host-clusters-to-Windows-Server-2016-Technical-Preview-in-VMM.md)
[Managing Hyper-V hosts and host clusters with VMM](Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


