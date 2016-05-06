---
title: Runbook Permissions_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 27f74a8a-c82e-42ce-b037-9c5d00d6110c
---
# Runbook Permissions_1
Runbook access permissions are set through the Runbook Designer. By default, only users in the Orchestrator Users Group have full access to a runbook. You give access to additional users to run, start, stop, view, and change runbooks at either the folder level or the individual runbook level.

### To view or modify the permissions of a runbook

1.  In the Runbook Designer, in the **Connections** pane, click the **Runbooks** folder.

2.  In the **Runbook Designer** Design workspace, right\-click the tab for a runbook to select **Permissions**.

3.  To give another user or security group access to the runbook, click the **Add** button, and select the user or security group from the local computer or from the domain.

4.  If the user or security group should be able to view and run the runbook, select the **Allow** check box next to **Read**.

    If the user or security group should be able to change the runbook, select the **Allow** check box next to **Write**.

    If the user or security group should be able to change permissions for the runbook, select the **Allow** check box next to **Full Control**.

5.  To close the **Permissions for Runbook** dialog box and save any changes, click **OK**.

## See Also
[Runbook Concepts](./Runbook-Concepts.md)


