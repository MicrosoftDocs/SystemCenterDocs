---
title: How to add a bare-metal computer to a Scale-Out File Server in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1ddee956-c5e0-4b74-9796-b38b28c503e5
---
# How to add a bare-metal computer to a Scale-Out File Server in VMM
You can use the following procedure to add one or more bare\-metal computers to a host cluster or Scale\-Out File Server cluster in Virtual Machine Manager \(VMM\).

### To add a bare\-metal computer to a Scale\-Out File Server in VMM

1.  As needed, review [Prerequisites: creating Scale-Out File Servers from bare metal with VMM](Prerequisites--creating-Scale-Out-File-Servers-from-bare-metal-with-VMM.md). If you created the cluster from bare metal, you can use the same physical computer profile, PXE server, and other similar elements that you used when creating the cluster.

2.  Open the **Fabric** workspace.

3.  In the **Fabric** pane, expand **Storage** > **File Servers**, and in the **File Servers** pane, locate the Scale\-Out File Server cluster. Right\-click it and then click **Add File Server Nodes**.

4.  On the **Resource Type** page, select **Physical computers to be provisioned**, then fill in the options:

    1.  Select the physical computer profile \(which will provide the administrator Run As account and domain name\).

    2.  Next to the **BMC Run As account** box, click **Browse**, select a Run As account that has permissions to access the BMC, and then click **OK**. For example, if you had a Run As account called **BMC Administrator**, you could select that account.

        If you do not already have a Run As account, click **Browse**, and then in the **Select a Run As Account** dialog box, click **Create Run As Account**.

    3.  In the **Out\-of\-band management protocol** list, click the protocol that your BMCs use.

        > [!NOTE]
        > If you want to use Data Center Management Interface \(DCMI\), click **Intelligent Platform Management Interface \(IPMI\)**. Although DCMI 1.0 is not listed, it is supported.

    4.  For **Out of band management port**, ensure that the correct port is selected.

    5.  If the **Skip cluster validation** option appears, and you do not require support from Microsoft for this cluster, you can skip validation.

        This option does not appear for a Scale\-Out File Server cluster using Storage Spaces Direct.

    Then click **Next**.

5.  On the **Discovery Scope** page, specify the IP address scope that includes the IP addresses of the BMCs. You can enter a single IP address, an IP subnet, or an IP address range.

    Deep discovery provides detailed information about a computer \(for example, MAC addresses of network adapters\) but restarts the computer, and requires additional time. You can allow or skip deep discovery.

    If you are adding a single computer, you can either specify a single IP address, or specify an IP address range that both starts and ends with the intended IP address. If you specify a single IP address, and allow deep discovery, when you click **Next**, the computer will be restarted. If you specify an IP address range, when you click **Next**, information about the computer will be displayed, and you can confirm that you specified the computer that you meant to.

    Then click **Next**.

6.  If you specified a single IP address on the previous page, skip this step. Otherwise, the **Target Resources** page appears. Review the list of discovered BMCs \(identified by IP addresses\), and select the ones you want to include in the cluster.

    If you don't see all the BMCs that you expect, confirm that they are on a network accessible to the VMM server, and as needed, click **Refresh**. If BMCs still appear to be missing, review [Prerequisites: creating Scale-Out File Servers from bare metal with VMM](Prerequisites--creating-Scale-Out-File-Servers-from-bare-metal-with-VMM.md).

    Deep discovery provides detailed information about a computer \(for example, MAC addresses of network adapters\) but restarts the computer, and requires additional time. You can allow or skip deep discovery.

    When you have finished making selections, click **Next**.

7.  On the **Deployment Customization** page, review the list of computers again, and provide information for each computer that you want to include. If you see a computer that you don't want to include, select the BMC \(identified by IP address\) and then click **Remove**.

    > [!CAUTION]
    > Review the list carefully. On a computer that already has a deployed operating system, proceeding with deployment can overwrite the operating system.

    Configure computers as follows:

    1.  Click the BMC IP address.

    2.  In the **Computer name** box, type a unique name, without any wildcard characters. \(Until you type a computer name for the computer, a **Missing settings** warning appears.\)

        For example, type **ClusNode04**.

    3.  Select or clear **Skip Active Directory check for this computer name**. The Active Directory check prevents deployment if the computer account already exists in Active Directory Domain Services \(AD DS\). This helps prevent deploying a computer with the same name as an existing computer.

        > [!CAUTION]
        > If you skip the Active Directory check, and there is an existing computer account in AD DS other than the Run As account that was specified in the physical computer profile, the deployment process will fail to join the computer to the domain.

    4.  For the computer you are configuring, click a network adapter \(on the left\). You can leave the displayed configuration unchanged, or fill in more information by clicking the button on the right, labeled either with **Configure** or with an ellipsis \(**...**\).

        If you click the button, in the **Network Adapter IP Configuration** box, you can specify IP settings:

        -   **Specify static IP settings for this network adapter**: If you check this box, select a logical network and \(if applicable in that logical network\) an IP subnet.

            > [!IMPORTANT]
            > If you select an IP subnet, make sure that it corresponds to the physical location where you are deploying the hosts and to the network that the adapter is connected to. Otherwise, deployment may fail.

        -   **Obtain an IP address corresponding to the selected subnet**: check this option if you selected an IP subnet that includes an IP address pool. Otherwise, type an IP address that is in within the logical network or its subnet.

    5.  Repeat the configuration process for each network adapter in a computer.

        > [!IMPORTANT]
        > If the number of physical network adapters in a computer does not match the number of physical network adapters that are defined in the physical computer profile, you must specify any information that is missing for the adapters. If you decide not to provision this computer right now \(for example, if physical hardware needs to be installed or uninstalled\), you can select the computer's BMC IP address from the list and then click **Remove**.

    6.  Repeat the entire process for each BMC IP address in the list.

    When you have filled in needed information for all the computers you want to provision, click **Next**.

8.  On the **Summary** page, confirm the settings, and then click **Finish** to provision the computers and add them to the cluster under VMM management.

    Depending on your settings, the **Jobs** dialog box might appear. Make sure that all steps in the job reach the **Completed** status, and then close the dialog box.

9. To confirm that the node was added to the cluster:

    1.  Open the **Fabric** workspace.

    2.  In the **Fabric** pane, expand **Storage** > **File Servers**, and then locate and click the cluster. In the **File Servers** pane, verify that the new nodes are **OK**.

If you added a node to a cluster configured with Storage Spaces Direct, you also added one or more disks to the cluster. If the disks have not been added into your storage pools, see [How to create or modify a storage pool on a Scale-Out File Server in VMM](How-to-create-or-modify-a-storage-pool-on-a-Scale-Out-File-Server-in-VMM.md).

## See Also
[Deploying Scale-Out File Servers from bare metal with VMM](Deploying-Scale-Out-File-Servers-from-bare-metal-with-VMM.md)
[Managing Scale-Out File Servers with VMM](Managing-Scale-Out-File-Servers-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing infrastructure resources with VMM](Managing-infrastructure-resources-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


