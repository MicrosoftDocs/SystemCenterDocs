---
title: Embedded Loops
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc9e2b46-a272-415c-a7f7-ab5b2242bcaa
author:bwren
manager:cfreemanwa
---
# Embedded Loops
In [!INCLUDE[orchlong](../../orch/deploy/includes/orchlong_md.md)], looping can be configured for any runbook. By using loops, you can build automatic retries and monitor at any location in a runbook.  
  
Each activity can create a loop so that you can retry operations if they fail or test the output information of the activity for valid data. You can also use these mechanisms to build wait conditions into your workflows.  
  
When a loop is configured for an activity, it continues to run with the same input data until a desired exit looping criteria is reached. The exit criteria is built in a similar way as smart link configurations. You can use any published data item from the activity as part of the exit or do not exit configuration. Included in the common published data are special data items such as **Loop: Number of attempts** and **Loop: Total duration** that let you use information from the loop itself in the looping conditions.  
  
Loops run one time for each incoming piece of data that is passed to the activity. For example, consider a runbook that uses a **Query Database** activity followed by **Append Line**. If the **Query Database** activity returned three rows, the **Append Line** activity would run three times. If you have a loop on the **Append Line** activity, it would run three separate loops. After the first data item has looped through the **Append Line** activity, the next item goes through **Append Line** and loops until it exits, and then the third begins. After all three items have been processed, the next activity in the runbook runs.  
  
## Configuring Looping  
Use the following procedure to configure looping.  
  
#### To configure looping  
  
1.  Right\-click an activity in the runbook to select **Looping**. The **Looping Properties** dialog box opens.  
  
2.  On the **General** tab, click **Enable**.  
  
3.  In the **Delay between attempts** box, type the number of seconds to pause between each attempt to run the activity.  
  
## Exit and Do Not Exit Conditions  
The rules on the **Exit** tab specify the conditions that determine whether the loop exits. The rules on the **Do Not Exit** tab specify the conditions that cause the loop to continue.  
  
> [!IMPORTANT]  
> The rules on the **Do Not Exit** tab supersede the rules on the **Exit** tab.  
  
The rules within each tab are joined by using an **Or** condition. Only one of the conditions on a tab must be true for the entire tab to be true.  
  
Use the following procedure to add or remove an **Exit** condition.  
  
#### To add an exit condition  
  
1.  In the **Looping Properties** dialog box, click either the **Exit** tab or **Do Not Exit** tab, and then select the condition listed in the box, or click **Add** to add a condition.  
  
    > [!IMPORTANT]  
    > To change the values that make up the rule, you have to select each underlined portion of the link condition.  
  
2.  Click the listed activity in the condition to open the **Published Data** dialog box.  
  
3.  Check the **Show common Returned Data** box to display properties that are common to all activities.  
  
4.  Select a property from the published data, and then click **OK**. The criteria expression is changed depending on the type of data that the property returns.  
  
5.  To change the different parts of the expression, select the underlined text and either select or type in an appropriate value. For more information about criteria, see [Smart Link Criteria](assetId:///4a5cf9c2-d19a-4fd4-af5a-be420b5fecb7).  
  
6.  Click **Finish**.  
  
#### To remove an exit condition  
  
1.  In the **Looping Properties** dialog box, click either the **Exit** tab or the **Do Not Exit** tab.  
  
2.  To select the condition you want to remove, click **Or** to the right of the link condition, and then click **Remove**.  
  
3.  Click **Finish**.  
  
## See Also  
[Workflow Control](../../orch/manage/Workflow-Control.md)  
  
