---
title: How to perform rolling updates on a Hyper-V host cluster in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d15222b4-ba51-417b-addf-cca88d43663a
---
# How to perform rolling updates on a Hyper-V host cluster in VMM
Use the following procedure to orchestrate rolling updates of a Hyper\-V host cluster that is managed by [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)]. [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] rolls through the host cluster, remediating one cluster node at a time. If a cluster node is compliant, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] bypasses that node.

Before [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] begins remediating a host in a cluster, it places the host in maintenance mode. You have the option of migrating all virtual machines to other hosts in the cluster. If you do not select this option, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] saves state and does not migrate virtual machines.

> [!NOTE]
> The **Remediate** action is only available after you install a WSUS server for [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], enable update management, create update baselines for computers managed by [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], and scan the computers for compliance. For more information, see [Managing fabric updates in VMM](Managing-fabric-updates-in-VMM.md).

### To perform rolling update remediation on a Hyper\-V host cluster

1.  Display **Compliance** view for the managed computers:

    1.  Open the **Fabric** workspace.

    2.  In the **Fabric** pane, click **Servers**.

    3.  On the **Home** tab, in the **Show** group, click **Compliance**.

2.  On the **Home** tab, in the **Compliance** group, click **Remediate**. \(The **Remediate** task is only available when the selected objects are noncompliant.\)

    The **Update Remediation** dialog box opens.

3.  In the resource list, select the host cluster by its cluster name.

    If you select the cluster by its cluster name, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] assumes you want to orchestrate remediation of the hosts in the cluster, and displays cluster remediation options. If you select individual hosts in the cluster, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] assumes that you want to update them as you would a stand\-alone host, and does not display cluster remediation options.

4.  If you prefer to restart the computers manually after remediation completes if any updates require a restart, select the **Do not restart the servers after remediation** check box.

    > [!NOTE]
    > If you choose to manually restart computers after installing updates, that status of the computers will remain **Pending Reboot** until after you scan the computer for updates again. [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] does not scan computers to assess their update compliance status during refreshes.

5.  Select the **Allow remediation of clusters with nodes already in maintenance mode check box** if you want to bypass maintenance mode.

    By default, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] places each host in maintenance mode before it remediates updates on the host.

6.  Specify **Live migration** to remove virtual machines from a host before performing update remediation or **Save state** to shut down virtual machines and proceed with remediation.

7.  Click **Remediate** to start update remediation on the host cluster.

You can watch the status of the remediation in the **Jobs** window or the **Jobs** workspace.

After the remediation completes successfully, and no reboot is pending for any machine, the compliance status of each node in the host cluster changes to **Compliant**.

> [!NOTE]
> If any computer has a **Machine Reboot Pending** status, restart the computer to complete the update installation and bring the computer into compliance.

## See Also
[Performing update remediation in VMM](Performing-update-remediation-in-VMM.md)


