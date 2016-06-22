---
title: How to deploy a Scale-Out File Server from bare metal in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a13a8ace-ccc8-4ecc-ba69-b2c9fb05c9c4
---
# How to deploy a Scale-Out File Server from bare metal in VMM
You can use Virtual Machine Manager (VMM) to deploy a Scale-Out File Server, either to “bare-metal computers” (no operating system installed), or computers with an installed operating system that will be overwritten during the process. For this deployment, VMM does the following:

1.  Discovers the physical computers through out-of-band management

2.  Deploys an operating system image on the computers by using the selected physical computer profile

3.  Installs the failover clustering feature and the file server role.

4.  After creating the cluster, enables the Scale-Out File Server role.

5.  Brings the provisioned Scale-Out File Server under VMM management

### To deploy a Scale-Out File Server from bare metal

1.  Ensure that you have met the requirements in [Prerequisites: creating Scale-Out File Servers from bare metal with VMM](Prerequisites--creating-Scale-Out-File-Servers-from-bare-metal-with-VMM.md).

2.  Open the **Fabric** workspace.

3.  In the **Fabric** pane, click **Servers**.

4.  On the **Home** tab, in the **Create** group, click **Create** and then click **File Server Cluster**. The wizard opens.

5.  On the **General Configuration** page,  specify a **Cluster name**, a **Scale-Out File Server name**, and (if you are not using DHCP) **Cluster IP addresses**. For example, you could use the names **Cluster03**, **SOFileSrv02**, and an appropriate IP address for your environment.

    If the existing servers are running Windows Server Technical Preview, also choose a **Storage configuration**:

    -   For shared storage, click **Storage connected to the cluster using shared SAS, FC, or iSCSI**.

    -   For Storage Spaces Direct, click **Disk subsystem directly connected to individual nodes in the cluster**. For information about this configuration, see [Storage Spaces Direct in Windows Server Technical Preview](https://technet.microsoft.com/library/mt126109.aspx).

    Then click **Next**.

6.  On the **Resource Type** page, select **Physical computers to be provisioned**, then fill in the options:

    1.  Select the physical computer profile (which will provide the domain name and administrator Run As account for each node).

    2.  Next to the **BMC Run As account** box, click **Browse**, select a Run As account that has permissions to access the BMC, and then click **OK**. For example, if you had a Run As account called **BMC Administrator**, you could select that account.

        If you do not already have a Run As account, click **Browse**, and then in the **Select a Run As Account** dialog box, click **Create Run As Account**.

    3.  In the **Out-of-band management protocol** list, click the protocol that your BMCs use.

        > [!NOTE]
        > If you want to use Data Center Management Interface (DCMI), click **Intelligent Platform Management Interface (IPMI)**. Although DCMI 1.0 is not listed, it is supported.

    4.  For **Out of band management port**, ensure that the correct port is selected.

    5.  If the **Skip cluster validation** option appears, and you do not require support from Microsoft for this cluster, you can skip validation.

        This option does not appear for a Scale-Out File Server cluster using Storage Spaces Direct (**Disk subsystem directly connected to individual nodes in the cluster**).

    Then click **Next**.

7.  On the **Discovery Scope** page, specify the IP address scope that includes the IP addresses of the BMCs. You can enter a single IP address, an IP subnet, or an IP address range.

    Deep discovery provides detailed information about a computer (for example, MAC addresses of network adapters) but restarts the computer, and requires additional time. You can allow or skip deep discovery.

    Then click **Next**.

8.  If you specified a single IP address on the previous page, skip this step. Otherwise, the **Target Resources** page appears. Review the list of discovered BMCs (identified by IP addresses), and select the ones you want to include in the cluster.

    If you don't see all the BMCs that you expect, confirm that they are on a network accessible to the VMM server, and as needed, click **Refresh**. If BMCs still appear to be missing, review [Prerequisites: creating Scale-Out File Servers from bare metal with VMM](Prerequisites--creating-Scale-Out-File-Servers-from-bare-metal-with-VMM.md).

    Deep discovery provides detailed information about a computer (for example, MAC addresses of network adapters) but restarts the computer, and requires additional time. You can allow or skip deep discovery.

    When you have finished making selections, click **Next**.

9. On the **Deployment Customization** page, review the list of computers again, and provide information for each computer that you want to include. If you see a computer that you don't want to include, select the BMC (identified by IP address) and then click **Remove**.

    > [!CAUTION]
    > Review the list carefully. On a computer that already has a deployed operating system, proceeding with deployment can overwrite the operating system.

    Configure computers as follows:

    1.  Click the BMC IP address.

    2.  In the **Computer name** box, type a unique name, without any wildcard characters. (Until you type a computer name for the computer, a **Missing settings** warning appears.)

        For example, type **ClusNode01**.

    3.  Select or clear **Skip Active Directory check for this computer name**. The Active Directory check prevents deployment if the computer account already exists in Active Directory Domain Services (AD DS). This helps prevent deploying a computer with the same name as an existing computer.

        > [!CAUTION]
        > If you skip the Active Directory check, and there is an existing computer account in AD DS other than the Run As account that was specified in the physical computer profile, the deployment process will fail to join the computer to the domain.

    4.  For the computer you are configuring, click a network adapter (on the left). You can leave the displayed configuration unchanged, or fill in more information by clicking the button on the right, labeled either with **Configure** or with an ellipsis (**...**).

        If you click the button, in the **Network Adapter IP Configuration** box, you can specify the following:

        -   **Specify static IP settings for this network adapter**: If you check this box, select a logical network and (if applicable in that logical network) an IP subnet. If the selected IP subnet includes IP address pool, you can check **Obtain an IP address corresponding to the selected subnet**. Otherwise, type an IP address that is in within the logical network or its subnet.

            > [!IMPORTANT]
            > If you select an IP subnet, make sure that it corresponds to the physical location where you are deploying the hosts and to the network that the adapter is connected to. Otherwise, deployment may fail.

    5.  Repeat the configuration process for each network adapter in a computer.

        > [!IMPORTANT]
        > If the number of physical network adapters in a computer does not match the number of physical network adapters that are defined in the physical computer profile, you must specify any information that is missing for the adapters. If you decide not to provision this computer right now (for example, if physical hardware needs to be installed or uninstalled), you can select the computer's BMC IP address from the list and then click **Remove**.

    6.  Repeat the entire process for each BMC IP address in the list.

    When you have filled in needed information for all the computers you want to provision, click **Next**.

10. On the **Summary** page, confirm the settings, and then click **Finish** to deploy the computers, create the cluster, and bring it under VMM management.

    Depending on your settings, the **Jobs** dialog box might appear. Make sure that all steps in the job reach the **Completed** status, and then close the dialog box.

11. To confirm that the Scale-Out File Server was added:

    1.  Open the **Fabric** workspace.

    2.  In the **Fabric** pane, expand **Storage** > **File Servers**, and then locate and click the new Scale-Out File Server. In the **File Servers** pane, verify that the status of the cluster is **OK**.

After you have deployed the Scale-Out File Server, configure storage pools and file shares as described in [Configuring storage using Scale-Out File Servers in VMM](Configuring-storage-using-Scale-Out-File-Servers-in-VMM.md)

## See Also
[Deploying Scale-Out File Servers from bare metal with VMM](Deploying-Scale-Out-File-Servers-from-bare-metal-with-VMM.md)
[Modifying Scale-Out File Servers in VMM](Modifying-Scale-Out-File-Servers-in-VMM.md)
[Configuring storage using Scale-Out File Servers in VMM](Configuring-storage-using-Scale-Out-File-Servers-in-VMM.md)
[Creating a Scale-Out File Server in VMM from existing Windows servers](Creating-a-Scale-Out-File-Server-in-VMM-from-existing-Windows-servers.md)
[Managing Scale-Out File Servers with VMM](Managing-Scale-Out-File-Servers-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing infrastructure resources with VMM](Managing-infrastructure-resources-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


