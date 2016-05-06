---
title: Counters
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6f0353ac-5847-483d-ac1d-d2bbc1268838
---
# Counters
When building runbooks in [!INCLUDE[orchlong](../Token/orchlong_md.md)], you might find that there are values that must be incremented, such as keeping track of the number of backup attempts that a runbook made. Counters let you modify and check the status of a number that you can use to keep track of important statistics. You create a counter in the Connections pane in the Runbook Designer, and then get and modify it by using the [Get Counter Value](../Topic/Get-Counter-Value.md) and [Modify Counter](../Topic/Modify-Counter.md) activities. Each of these activities presents the value of the counter as [Published Data](../Topic/Published-Data.md) so that it can be used by other activities and links.

> [!IMPORTANT]
> The access permissions for counters can be modified, but the Runbook server does not enforce these permissions.

> [!WARNING]
> You cannot run multiple, simultaneous jobs for runbooks that contain Modify Counter activities because simultaneous jobs of the same runbook that modify \(set, reset, increment, or decrement\) a counter can cause the counter value to become unreliable. You can, however, read the value of counters in runbooks that run simultaneously.

> [!IMPORTANT]
> [!INCLUDE[orchshort](../Token/orchshort_md.md)] does not support moving multiple counters with multiple\-selection. To move more than one counter to another folder, you must move each counter individually.

Use the following procedures to create a counter and to organize counters.

#### To create a counter

1.  In the **Connections** pane, double\-click the **Global Settings** folder, right\-click the **Counters** folder or a subfolder of the **Counters** folder to select **New**, and then click **Counter** to open the **New Counter** dialog box.

2.  In the **Name** box, type a name for the counter.

3.  In the **Description** box, type a description that explains the purpose of the counter.

4.  In the **Default Value** box, type the starting value of the counter. This value is the starting value of the counter when it is created or reset.

5.  To modify a counter, double\-click the counter.

    To remove a counter, right\-click the counter to select **Delete**.

6.  Click **Finish**.

#### To organize counters

1.  You can group counters in folders to organize them. To create a folder, right\-click the **Counters** folder to select **New**, and then click **Folder**.

2.  To move a counter to a different folder, right\-click the counter to select **Move** to open the **Select a Folder** dialog box.

3.  Select the destination folder, and then click **OK**. The counter is moved to the new folder location.

## See Also
[Get Counter Value](../Topic/Get-Counter-Value.md)
[Modify Counter](../Topic/Modify-Counter.md)
[Published Data](../Topic/Published-Data.md)

