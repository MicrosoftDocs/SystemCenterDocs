---
title: How to Test a Runbook
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5af704c9-6007-4de6-9c75-d7bfba3d4935
---
# How to Test a Runbook
After you build a runbook, you can test it before it is run in production. To test, you use the **Runbook Tester** which you start in the **Runbook Designer**. The **Runbook Tester** lets you run the runbook to view the Published Data from each activity. You can run through the entire runbook, step through each activity one at a time, or set breakpoints at certain activities.

### To test a runbook

1.  In the **Runbook Designer**, open the runbook, and on the menu bar, click **Runbook Tester**.

2.  If prompted, click **Yes** to check out the runbook.

3.  To run through the runbook from beginning to end without stopping, click **Run to Breakpoint**.

    If you want to step through it one activity at a time, click **Step**.

4.  View the **Log** pane to see the completion status of each activity. To view the details and Published Data from an activity, select the activity, and click **Show Details**.

### To set a breakpoint

1.  Select the activity on which to set the breakpoint.

2.  Click **Toggle Breakpoint**.

3.  Click **Run to Breakpoint**.

    Each activity up to the breakpoint runs. The runbook pauses before running the activity with the breakpoint.

4.  To continue through to the end of the runbook, click **Run to Breakpoint** again, or to step through it one activity at a time, click **Step**.

## See Also
[Design and Build Runbooks](Design-and-Build-Runbooks.md)


