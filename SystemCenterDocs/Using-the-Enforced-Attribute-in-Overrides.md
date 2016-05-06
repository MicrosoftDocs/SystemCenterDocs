---
title: Using the Enforced Attribute in Overrides
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f87c672-5eb9-4f10-b3b3-b693b51651d0
---
# Using the Enforced Attribute in Overrides
When you configure an override to a rule, monitor, or discovery in Operations Manager for System Center 2012, you will notice an **Enforced** check box in the row for each value that you can override, as shown in the following illustration.

![](/Image/OverrideEnforced.gif)

When the Enforced attribute is selected for an override, this setting ensures that the override will take precedence over all other overrides of the same type and context that do not have **Enforced** set.

Overrides that apply to a class are applied first, then overrides that apply to a group, and finally overrides that apply to a specific object. The Enforced attribute assures that the override will take precedence when two overrides of the same type and context conflict.

For example, you have two Windows computers, COMPUTER1 and COMPUTER2. COMPUTER1 is member of GROUP\-A and is also member of GROUP\-B. COMPUTER2 is not a member of any group. The default threshold for a CPU monitor is 80%.

You apply an override to the Windows Computer class that changes the CPU monitor threshold to 70%. You create another override to that monitor that applies to GROUP\-A and sets the threshold to 90%. At this point, the threshold for COMPUTER1 is 90% and the threshold for COMPUTER2 is 70%.

If you create an override that applies to GROUP\-B and sets the threshold to 95%, the resulting threshold for COMPUTER1, which is member of both GROUP\-A and GROUP\-B, is unpredictable. However, if you used the Enforced attribute on the override that applies to GROUP\-B, you ensure that the 95% threshold applies to COMPUTER1.

If you create an override that applies to COMPUTER1 and sets the threshold to 60%, the resulting threshold for COMPUTER1 is 60% because the object override takes precedence over the class and group overrides.

## See Also
[Using Classes and Groups for Overrides in Operations Manager](./Using-Classes-and-Groups-for-Overrides-in-Operations-Manager.md)
[How to Override a Rule or Monitor](./How-to-Override-a-Rule-or-Monitor.md)
[How to Enable or Disable a Rule or Monitor](./How-to-Enable-or-Disable-a-Rule-or-Monitor.md)
[How to Enable Recovery and Diagnostic Tasks](./How-to-Enable-Recovery-and-Diagnostic-Tasks.md)


