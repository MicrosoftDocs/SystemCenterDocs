---
title: Deploy Runbooks
description: Provides an overview of the process for making runbooks available for operations.
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
author: cfreemanwa
ms.author: cfreeman
ms.date: 03/23/2017
manager: carmonm
---
# Deploy runbooks with System Center 2016 - Orchestrator

>Applies To: System Center 2016 - Orchestrator

There are tools available in Orchestrator to help you manage the versions of your runbooks. These tools are described in the following sections.  

## Version control  
In System Center 2016 - Orchestrator, multiple users can create and update runbooks. However, only one user at a time can make changes to a runbook. This protects your work from being overwritten by someone else with the same permission level.  

To edit a runbook, you must check it out. Another user cannot edit that runbook until you either commit all changes by checking the runbook in or revert all changes by undoing the checkout.  

### Check in and check out  

-   **Check Out**: When a user is editing a runbook, the runbook is checked out and cannot be edited by anyone else. If someone else is already editing the runbook, a pop\-up window opens informing you that someone is already editing the runbook.  

-   **Check In**: When a user editing the runbook performs a Check In operation, all changes that were made are committed, and other users can then edit the runbook after they check it out. Check in comments describe the changes that have been made.  

-   **Undo Check Out**: When a user editing the runbook performs an Undo Check Out operation, all changes that were made are reverted after the runbook was checked out. After the Undo Check Out operation is completed, another user can edit the runbook.  

## Audit Log  
When a runbook has been changed and is checked in by a user, an entry appears in the **Audit History** log.  

> [TIP]  
> When a runbook has been altered to a state where it is no longer functioning, you can select the **Audit History** tab at the bottom of the Runbook Designer to see the changes that were made and then reverse them.  

### To view runbook change details  

1.  In the Runbook Designer, select the **Audit History** tab at the bottom, double\-click the entry item to open the **Details** dialog box.  

2.  In the **Name** column, click each item in the list to view the changes that were made.  

3.  When you select an item, the **Action** type displays beneath the **Activities** box. For example, **Action: Modified** or **Action: Added**. When you select the **Action: Modified** type, the **Attribute**, **Old Value**, and **New Value** are listed in the bottom text box.  

## Next steps  
- To learn more about how to design and build runbooks see [Design and build runbooks](../manage/design-and-build-runbooks.md)

