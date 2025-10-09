---
ms.assetid: 954164df-4d78-45a7-868e-a7639747b761
title: Enable or Disable a Rule or Monitor
description: This article provides specific instructions on how to enable or enable Management Pack monitoring rules and monitors.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.custom: engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
---

# Enable or disable a rule or monitor


In System Center - Operations Manager, if a management pack's default settings contain a monitor or rule that isn't necessary in your environment, you can use overrides to disable this monitor or rule. In addition, some management packs ship with some rules or monitors disabled; you should read the management pack guide to identify the workflows that are disabled by default and determine if you should enable any of them for your monitoring needs. For example, the management packs for network monitoring contain rules and monitors that are vendor-specific. Many vendor-specific rules and monitors in the network management pack are disabled to avoid performance impact. You should identify the devices used in your environment and use overrides to enable the rules and monitors specific to your devices.  

## Enable or disable a monitor or rule using overrides  

1. Sign in to the computer with an account that is a member of the Operations Manager Advanced Operator role.  

2. In the Operations console, select **Authoring**.  

3. In the **Authoring** workspace, select **Monitors** (or **Rules** if you want to disable a rule).  

4. In the **Monitors** or **Rules** section, select the monitor or rule that you want to disable.  

5. On the Operations console toolbar, select **Overrides** and then point to **Override the Monitor** (or **Rule**). You can choose to override this monitor or rule for objects of a specific type or for all objects within a group. After you choose which group of object type to override, the **Override Properties** dialog opens, enabling you to view the default settings contained in this monitor or rule. For more information about applying an override, see [Using Classes and Groups for Overrides](~/scom/manage-mp-overview-override-targets.md).  

6. In the **Override Properties** dialog, select the **Override** checkbox that corresponds to the **Enabled** parameter.  

    > [!NOTE]  
    > If you select **Disable** instead of **Override**, the **Override Properties** dialog opens with the **Override** checkbox selected and the **Enabled** value set to **False**.  

7. In the **Override Setting** column, select **True** to enable the rule or monitor or **False** to disable the rule or monitor.  

8. In the **Select destination management pack** list, select the appropriate management pack in which to store the override or create a new unsealed management pack by selecting **New**. For more information about selecting a destination management pack, see [Creating a Management Pack for Overrides](manage-mp-create-unsealed-mp.md).  

9. When you complete your changes, select **OK**.  

## Next steps

- To understand the differences between classes and groups in Operations Manage and how workflows apply to each, review [Using Classes and Groups for Overrides in Operations Manager](~/scom/manage-mp-overview-override-targets.md).

- Before making changes to the monitoring settings defined in an Operations Manager management pack, review [How to Override a Rule or Monitor](~/scom/manage-mp-override-rule-monitor.md) to understand how to configure the changes.

- To understand how they can help investigate and auto-remediate issues identified by monitors, review [How to Enable Recovery and Diagnostic Tasks](~/scom/manage-enable-recovery-and-diagnostic-tasks.md).  
