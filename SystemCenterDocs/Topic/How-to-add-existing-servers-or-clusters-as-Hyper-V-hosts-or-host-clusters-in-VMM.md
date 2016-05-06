---
title: How to add existing servers or clusters as Hyper-V hosts or host clusters in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c02fa3c2-fd4b-4479-abec-92d40bf00fd6
---
# How to add existing servers or clusters as Hyper-V hosts or host clusters in VMM
You can use this procedure for servers or clusters regardless of whether the Hyper\-V role is already installed on them. If the servers or clusters are in a perimeter network, do not use this procedure, but instead see [How to add Hyper-V hosts in a perimeter network in VMM](../Topic/How-to-add-Hyper-V-hosts-in-a-perimeter-network-in-VMM.md). Additional links are provided at the end of this topic.

> [!IMPORTANT]
> Before you begin this procedure, see [Prerequisites: adding servers or clusters as Hyper-V hosts or host clusters in VMM](../Topic/Prerequisites--adding-servers-or-clusters-as-Hyper-V-hosts-or-host-clusters-in-VMM.md).

### To add existing servers or clusters as Hyper\-V hosts or host clusters in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, click **Servers**.

3.  On the **Home** tab, in the **Add** group, click **Add Resources**, and then click **Hyper\-V Hosts and Clusters**.

    The Add Resource Wizard starts.

4.  On the **Resource location** page, the option that corresponds to your servers—trusted domain, untrusted domain, or disjointed namespace—and then click **Next**.

5.  On the **Credentials** page, enter the credentials for a domain account that has administrative permissions on all hosts that you want to add, and then click **Next**. \(For computers in an untrusted domain, you must use a Run As account.\)

    To create a Run As account, click **Browse** and then click **Create Run As Account**.

    > [!IMPORTANT]
    > The account must fulfill [Prerequisites: adding servers or clusters as Hyper-V hosts or host clusters in VMM](../Topic/Prerequisites--adding-servers-or-clusters-as-Hyper-V-hosts-or-host-clusters-in-VMM.md).

6.  On the **Discovery scope** page, specify computers as listed in the following table, and then click **Next**:

    |Domain of servers you're adding in relation to domain of VMM server|What to specify|
    |-----------------------------------------------------------------------|-------------------|
    |Same domain or domains with two\-way trust|-   If you click **Specify Windows Server computers by names**, in the **Computer names** box, enter computer names or IP addresses, one per line. If you are adding a Hyper\-V host cluster, specify the name or IP address of the cluster or of any cluster node. **Tip:**     If you type part of a computer name, when you click **Next**, you will see a list all computers that have names that begin with the text you typed.<br />-   If you click **Specify an Active Directory query to search for Windows Server computers**, you can type or generate a query. For information about Lightweight Directory Access Protocol \(LDAP\) queries, see [Creating a Query Filter](http://msdn.microsoft.com/library/ms675768.aspx).|
    |Untrusted domain|The **Discovery scope** page does not appear. Skip to the next step.|
    |Disjointed namespace|On the **Discovery scope** page, enter the fully qualified domain name \(FQDN\) of the host. Also, select the **Skip AD verification** check box.|

7.  On the **Target resources** page:

    -   For servers or clusters in a trusted domain or disjointed namespace, select the check box next to each computer that you want to add, and then click **Next**. If you specified a cluster name or cluster node in the previous step, select the check box next to the cluster name. \(The cluster name is listed together with the associated cluster nodes.\)

        For example, select the check box next to **HyperVHost01.contoso.com**, and then click **Next**.

    -   For servers in an untrusted domain, on the **Target resources** page, enter fully qualified domain name \(FQDN\) or IP address of the server or cluster that you want to add, and then click **Add**. For a cluster, you can enter an FQDN or IP address of the cluster or of one of the cluster nodes.

        If discovery succeeds, the host is listed under **Computer Name**.

        Repeat this step to add multiple hosts. When you're finished, click **Next**.

        For example, enter the name **HyperVHost02.fabrikam.com**, where *fabrikam.com* is the name of the untrusted domain.

    If the Hyper\-V role is not enabled on a selected server, you receive a message that [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] will install the Hyper\-V role and restart the server. Click **OK** to continue.

8.  On the **Host settings** page, do the following:

    1.  In the **Host group** list, click the host group to which you want to assign the host or host cluster.

        For example, click the host group **Seattle\\Tier0\_SEA**.

    2.  If the host is already associated with a different [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server, select the **Reassociate this host with this VMM environment** check box.

        > [!NOTE]
        > If the host was associated with a different [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server, it will stop working on that server.

    3.  For a stand\-alone host, in the **Add the following path** box, enter a path on the host for storing files for virtual machines that are deployed on the host, and then click **Add**. Repeat this step to add more than one path. Note:

        -   If you leave the box empty, the default is %SystemDrive%\\ProgramData\\Microsoft\\Windows\\Hyper\-V. It is a best practice not to add default paths that are on the same drive as the operating system files.

        -   If you specify a path that does not already exist, the path is created automatically.

        > [!NOTE]
        > When you add a host cluster, you do not specify default virtual machine paths, as you would for a stand\-alone host. For a host cluster, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] automatically manages the paths that are available for virtual machines, based on the shared storage that is available to the host cluster.

    4.  When you're finished, click **Next**.

9. On the **Summary** page, confirm the settings, and then click **Finish**.

    The **Jobs** dialog box appears to show the job status. Make sure that the job has a status of **Completed**, and then close the dialog box.

    If the hosts are in a disjointed namespace and the job fails, review the permissions requirement for Service Principal Names \(SPNs\) in [Prerequisites for a disjointed namespace](../Topic/Prerequisites--adding-servers-or-clusters-as-Hyper-V-hosts-or-host-clusters-in-VMM.md#BKMK_disjoint) in "Prerequisites: adding servers or clusters as Hyper\-V hosts or host clusters in VMM."

10. To verify that the host or host cluster was successfully added, in the **Fabric** pane, expand the host group and then click the host or host cluster. Then, in the **Hosts** pane, verify that the host status is **OK**.

    > [!TIP]
    > To view detailed information about host status, right\-click a host in the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console, and then click **Properties**. On the **Status** tab, you can view the health status for various areas such as overall health, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] agent health, and Hyper\-V role health. If there is an issue, you can click **Repair all**. [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] will try to automatically fix the issue.

## See Also
[Adding Windows servers as Hyper-V hosts or host clusters in VMM](../Topic/Adding-Windows-servers-as-Hyper-V-hosts-or-host-clusters-in-VMM.md)
[Configuring Hyper-V host properties in VMM](../Topic/Configuring-Hyper-V-host-properties-in-VMM.md)
[Creating a host cluster in VMM from existing Windows servers](../Topic/Creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md)
[Deploying Hyper-V hosts or host clusters from bare metal with VMM](../Topic/Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)
[Managing Hyper-V hosts and host clusters with VMM](../Topic/Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)
[Managing hosts and host clusters with VMM](../Topic/Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)

