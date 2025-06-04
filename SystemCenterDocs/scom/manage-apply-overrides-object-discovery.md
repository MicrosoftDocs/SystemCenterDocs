---
ms.assetid: f286e1fc-57f5-469f-bee5-e3756b560810
title: Apply Overrides to Object Discoveries
description: This article describes how to target and apply overrides to object discovery rules.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
ms.custom: UpdateFrequency2
---

# Apply overrides to object discoveries



System Center Operations Manager monitors computers and devices that it has discovered, and it also monitors applications and features that it discovers on monitored computers. There may be situations where you want to limit discovery. For example, you might want only some instances of SQL Server to be discovered and monitored, or you want to remove a computer that has already been discovered.

The precise steps to limit or restrict discovery depend on the object, application, or feature that you want to exclude from discovery. However, the general procedure is the same: identify the discovery that you want to limit and create an override to disable the discovery.

The override to disable the discovery can apply to:

- All objects in the class that the discovery applies to. If you use this selection for your override, you disable the discovery completely.

- A group. Group membership can be defined explicitly or dynamically. When you create a group, you save it to an unsealed management pack. However, an element in an unsealed management pack, such as an override, can't reference an element in a different unsealed management pack, such as a group. If you're going to use a group to limit the application of an override, you must either save the group to the same unsealed management pack as the override, or you must seal the management pack that contains the group. For more information, see [Creating and Managing Groups](manage-create-manage-groups.md).

- One or more specific objects in the class that the discovery applies to. Using this method, you can select from discovered objects.

- All objects of another class. Using this method, you specify a class of objects to apply the override to.

Choosing how to apply the override to disable the discovery depends on your situation. The simplest situation is when you want to disable discovery for a specific object or for all objects in a class. When you want to disable the discovery for any object that meets certain criteria, you must use a group that contains those objects or create a group that will identify those objects.

For example, you want to disable discovery of logical disks on management servers. You can configure an override to disable the discovery of applicable Windows Server logical disks and apply it to the Operations Manager Management Servers group, which is created automatically when you install Operations Manager. If, instead, you want to disable discovery of logical disks on computers in a specific organizational unit, there's no built-in group that satisfies that definition and so you would need to create a group that identifies those computers.

After an object has already been discovered, if you want to delete the object and not let it be discovered again, disable the discovery for that object and then run the **Remove-SCOMDisabledClassInstance** cmdlet in Operations Manager Shell. For help with this cmdlet, open Operations Manager Shell, and then enter **Get-Help Remove-SCOMDisabledClassInstance**.

## Next steps

- To learn how to create a custom writeable management pack to store your overrides, see [How to Create a Management Pack for Overrides](~/scom/manage-mp-create-unsealed-mp.md).

- Before making changes to the monitoring settings defined in an Operations Manager management pack, review [How to Override a Rule or Monitor](~/scom/manage-mp-override-rule-monitor.md) to understand how to configure the change.

- To understand the differences between classes and groups in Operations Manage and how workflows apply to each, review [Using Classes and Groups for Overrides in Operations Manager](manage-mp-overview-override-targets.md).
