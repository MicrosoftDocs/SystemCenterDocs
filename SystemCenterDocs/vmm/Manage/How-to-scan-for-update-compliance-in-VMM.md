---
title: How to scan for update compliance in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1598fe63-91a9-42a6-8fad-837ff31f060d
---
# How to scan for update compliance in VMM
After you assign computers to an update baseline in [!INCLUDE[vmm12sp1_long](../../includes/vmm12sp1_long_md.md)], you can scan the computers to determine their compliance status for the baselines.

When a computer is scanned for compliance, WSUS checks each update in the assigned update baselines to determine whether the update is applicable and, if the update is applicable, whether the update has been installed. After a compliance scan, for every computer, each update has a compliance status of **Compliant**, **Non Compliant**, **Error**, **Pending Reboot**, or **Unknown**. You can view compliance properties for additional information.

The compliance scan focuses only on the updates that the administrator has identified as important by adding them to a baseline. That enables organizations to monitor for compliance for what is deemed important for their organization.

The following changes can cause an **Unknown** update status for a computer, and should be followed by a scan operation to access the computer's compliance status:

-   A host is moved from one host group to another host group.

-   An update is added to or removed from a baseline that is assigned to a computer.

-   The computer is added to the scope of a baseline.

> [!IMPORTANT]
> You should perform all updates in **Compliance** view. The **Scan** and **Remediate** actions also are available in **Fabric Resources** view. However, if you scan and remediate updates in **Fabric Resource** view, you cannot see the results of the operations.

### To display Compliance view in the Fabric workspace

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, click **Servers**.

3.  On the **Home** tab, in the **Show** group, click **Compliance**.

    The results pane displays the compliance status of the computers in the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] fabric. Because you have not yet scanned the computers for compliance, the computers that you added to a baseline have a compliance status of **Unknown** and an operational status of **Pending Compliance Scan**.

### To scan computers for compliance

1.  In **Compliance** view of the **Fabric** workspace, select the computers that you want to scan.

2.  On the **Home** tab, in the **Compliance** group, click **Scan**.

    While the scan is in progress, the compliance status changes to **Unknown**. After the compliance scan completes, the computer's compliance status of each update is **Compliant**, **NonCompliant**, or **Error**. To bring noncompliant computers into compliance, you will perform update remediations in [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)].

## See Also
[How to configure update baselines in VMM](How-to-configure-update-baselines-in-VMM.md)
[Performing update remediation in VMM](Performing-update-remediation-in-VMM.md)
[Managing fabric updates in VMM](Managing-fabric-updates-in-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


