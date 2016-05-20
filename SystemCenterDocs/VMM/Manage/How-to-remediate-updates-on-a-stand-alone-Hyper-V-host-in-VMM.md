---
title: How to remediate updates on a stand-alone Hyper-V host in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f98a78c4-eea8-4b65-af06-5494bc77be48
---
# How to remediate updates on a stand-alone Hyper-V host in VMM
Use the following procedure to remediate updates for stand\-alone Hyper\-V hosts that are managed by [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)]. You can also orchestrate updates of a managed Hyper\-V host cluster in [!INCLUDE[vmm12short](Token/vmm12short_md.md)]. For information, see [How to perform rolling updates on a Hyper-V host cluster in VMM](How-to-perform-rolling-updates-on-a-Hyper-V-host-cluster-in-VMM.md).

> [!NOTE]
> The **Remediate** action is only available after you install a WSUS server for [!INCLUDE[vmm12short](Token/vmm12short_md.md)], enable update management, create and assign update baselines for computers managed by [!INCLUDE[vmm12short](Token/vmm12short_md.md)], and scan the computers for compliance. For more information, see [Managing fabric updates in VMM](Managing-fabric-updates-in-VMM.md).

### To remediate updates for a Hyper\-V host in [!INCLUDE[vmm12short](Token/vmm12short_md.md)]

1.  Display **Compliance** view for the managed computers:

    1.  Open the **Fabric** workspace.

    2.  In the **Fabric** pane, click **Servers**.

    3.  On the **Home** tab, in the **Show** group, click **Compliance**.

2.  Select the computers that you want to remediate. Click a computer to display all the baselines checked for that computer.

    The system may be compliant for some baselines and not compliant for others. You can select a single update baseline or a single update within a baseline.

3.  On the **Home** tab, in the **Compliance** group, click **Remediate**. \(The **Remediate** task is only available when the selected objects are noncompliant.\)

    The **Update Remediation** dialog box opens.

4.  Optionally select or clear update baselines or individual updates to determine which updates to remediate. If you selected a computer to remediate, all updates are initially selected.

5.  If you prefer to restart the computers manually after remediation completes instead of letting the wizard do that, select the **Do not restart the servers after remediation** check box.

    By default, the wizard restarts the computer after installing updates if any of the updates requires a restart. If you choose not to restart the servers after remediation, and any updates require a restart, the operational status of the computer changes to **Pending Machine Reboot** after the remediation. The updates will not be activated until you restart the computer.

    > [!NOTE]
    > If you choose to manually restart computers after installing updates, that status of the computers will remain **Pending Reboot** until after you scan the computer for updates again. [!INCLUDE[vmm12short](Token/vmm12short_md.md)] does not scan computers to assess their update compliance status during refreshes.

6.  Click **Remediate** to start update remediation.

## See Also
[Performing update remediation in VMM](Performing-update-remediation-in-VMM.md)
[Managing fabric updates in VMM](Managing-fabric-updates-in-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


