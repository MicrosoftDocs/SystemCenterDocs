---
title: How to configure update baselines in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 72d2c7b2-334f-485d-a384-f776fcd3eff7
---
# How to configure update baselines in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

After you add a Windows Server Update Services (WSUS) server to Virtual Machine Manager (VMM), you can prepare to manage updates for the VMM fabric by configuring update baselines. An update baseline contains a set of required updates that is then scoped to an assignment such as a host group, a stand-alone host, a host cluster, a VMM management server, or an infrastructure server. Update baselines can be assigned to host groups and to individual computers based on their role in VMM. Update baselines that are assigned to a host group are applied to all stand-alone hosts and host clusters in the host group, as well as the stand-alone hosts and host clusters in child host groups.

During a compliance scan, computers that are assigned to a baseline are graded for compliance with their assigned baselines. After a computer is found noncompliant, an administrator brings the computer into compliance through update remediation.

If a host is moved from one host group to another, the baselines for the new host group are applied to the host, and the baselines for the preceding host group no longer apply - that is, unless the baseline is assigned to both host groups. Explicit baseline assignments to a managed host stay with the host when it is moved from one host group to another. It is only when the baseline is assigned to a host group that baseline assignments get revoked during the move.

You can use two methods to prepare update baselines for remediation:

-   Use one of the built-in update baselines that VMM provides: **Sample Baseline for Critical Updates** and **Sample Baseline for Security Updates**.

-   Create your own update baseline.

> [!IMPORTANT]
> To help you get started with update management, the built-in security and critical baselines provide a starter set of updates in those categories. If you choose to use the built-in baselines, you must maintain them. They are not continuously updated.

The following procedures explain both methods. We recommend that you use the first procedure to update the built-in security baseline before you create your own baseline.

**Account requirements** To create or configure update baselines, you must be an administrator or delegated administrator in VMM. Delegated administrators can only assign the update baselines to computers that are within the scope of their user role.

## Assign Computers to a Built-in Update Baseline
VMM provides two sample built-in updates baselines that you can use to apply security updates and critical updates to the computers in your VMM environment. Before you can use a baseline, you must specify an assignment scope which contains the host groups, host clusters, individual managed computers, or infrastructure servers for which the baseline is used. The following procedure explains how to assign computers to the sample security baseline.

#### To assign computers to a built-in update baseline

1.  Open the **Library** workspace.

2.  On the **Library** pane, expand **Update Catalog and Baselines**, and then click **Update Baselines**.

    The **Baselines** pane displays the two built-in baselines: **Sample Baseline for Security Updates** and **Sample Baseline for Critical Updates**.

3.  On the **Baselines** pane, click **Sample Baseline for Security Updates**.

4.  On the **Home** page, in the **Properties** group, click **Properties**.

    The **Properties** dialog box for the **Sample Baseline for Security Updates** opens.

    > [!NOTE]
    > On the left of the dialog box, click **Updates** to open the **Updates** page.

5.  On the **Updates** page, optionally add or remove update baselines from the baselines that are listed. The **Sample Baseline for Security Updates** includes all security updates. To ensure that all security updates are remediated, do not remove any updates from this baseline.

6.  Click **Assignment Scope** to open the **Assignment Scope** page. Then select host groups, host clusters, computers, and infrastructure servers to add to the baseline.

    Computers are represented by the roles they perform in VMM. When you select a computer with a role, such as **VMM server**, all the other roles that the computer performs in VMM are selected. For example, if your VMM management server is also a library server, selecting your VMM management server under **VMM Server** causes the same computer under **Library Servers** to be selected.

    To apply a baseline to all hosts, select the **All Hosts** root host group.

7.  Click **OK** to save your changes.

## Create a New Update Baseline
Now that you have experience assigning computers to a built-in update baseline in VMM, try creating a new baseline by using the following procedure.

#### To create an update baseline in VMM

1.  Open the **Library** workspace.

2.  On the **Library** pane, expand **Update Catalog and Baselines**, and then click **Update Baselines**.

3.  On the **Home** page, in the **Create** group, click  **Baseline**.

    The **Update Baseline Wizard** starts.

4.  On the **General** page, enter a name (for example, **Critical Updates for Hyper-V Hosts**) and a description for the update baseline. Click Next to proceed to the **Updates** page.

5.  On the **Updates** page, add the updates that you want to include in the baseline.

    For example, to add critical updates for your Hyper-V hosts:

    1.  Click **Add**.

    2.  In the search box, type **critical updates** to filter the selection.

    3.  Select each critical update that you want to apply to your Hyper-V hosts.

        > [!TIP]
        > To select more than one update, hold down the CTRL key while you click the updates. To select a set of consecutive updates, click the first update, press and hold down the Shift key, and then click the last update in the set.

    4.  Click **Add**.

    Click **Next** to proceed to the **Assignment Scope** page.

6.  On the **Assignment Scope** page, expand **Host Groups** and **Infrastructure**. **Host Groups** lists all host groups, standalone hosts and clusters. **Infrastructure** lists all VMM role servers and any infrastructure servers. Select the items that you want to apply the baseline to. You can apply a baseline to computers that are performing any of the following roles in VMM:

    -   Host groups or individual hosts

    -   Library servers

    -   PXE servers

    -   Update server

    -   VMM management server

    Click Next to proceed to the **Summary** page.

7.  On the **Summary** page, review your settings, and then click **Finish**.

    If any of the selected updates require that you accept a Microsoft license agreement, the **Microsoft License Terms** dialog box opens.

8.  To start installing the updates, after you review the license terms, click **Accept** if you accept the license terms.

    > [!NOTE]
    > If multiple updates require a license agreement, VMM prompts for acceptance of each license.

To verify that the update baseline was created successfully, on the **Library** pane, expand **Updates and Baselines Catalog**, and then click **Baselines**. The results pane should display the new baseline.

## See Also
[Managing fabric updates in VMM](Managing-fabric-updates-in-VMM.md)
[How to scan for update compliance in VMM](How-to-scan-for-update-compliance-in-VMM.md)
[Performing update remediation in VMM](Performing-update-remediation-in-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



