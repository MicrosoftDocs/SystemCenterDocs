---
title: Runbook permissions
description: This article describes how to set permissions for users to access runbook properties.
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 0b0304df-364d-4f75-b9d5-6b3ddfea6bef
ms.date: 12/17/2024
author: Jeronika-MS
ms.author: v-gajeronika
ms.custom: engagement-fy23
---
# Runbook permissions

Runbook access permissions are set through the Runbook Designer. By default, only users in the Orchestrator Users Group have full access to a runbook. You give access to additional users to run, start, stop, view, and change runbooks at either the folder level or the individual runbook level.

For supported features in the Orcestrator console, see [Overview of the Orchestration console](./console-overview.md).

## View or modify the permissions of a runbook  

Follow these steps to view or modify the permissions of a runbook:

1.  In the Runbook Designer, in the **Connections** pane, select the **Runbooks** folder.  

2.  In the **Runbook Designer** Design workspace, right-click the tab for a runbook to select **Permissions**.  

3.  To give another user or security group access to the runbook, select the **Add** button, and select the user or security group from the local computer or from the domain.  

4.  If the user or security group should be able to view and run the runbook, select the **Allow** checkbox next to **Read**.  

    If the user or security group should be able to change the runbook, select the **Allow** checkbox next to **Write**.  

    If the user or security group should be able to change permissions for the runbook, select the **Allow** checkbox next to **Full Control**.  

5.  To close the **Permissions for Runbook** dialog and save any changes, select **OK**.  

## Next steps  

Read [Runbook Concepts](~/orchestrator/automate-runbooks.md) for an overview of runbook concepts and operations in System Center Orchestrator.
