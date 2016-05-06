---
title: Using Classes and Groups for Overrides in Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65b166bc-2e18-41f3-8062-ca3f8e8b412b
---
# Using Classes and Groups for Overrides in Operations Manager
This topic describes the differences between classes and groups in [!INCLUDE[om12long](./Token/om12long_md.md)], and how workflows, such as rules and monitors, apply to each. The following sections define classes and groups, and provide examples for applying overrides with the available override options.

## Classes
In [!INCLUDE[om12short](./Token/om12short_md.md)], a *class* is a definition of an item that can be discovered and managed. A class can represent a computer, a database, a service, a disk, an application, or any other kind of object that requires monitoring. Monitors, rules, discoveries, overrides, and tasks can apply to a class. For example, **Windows Server 2003 Logical Disk** is a class that defines logical disks on a computer that is running the Windows Server 2003 operating system. A monitor that applies to the **Windows Server 2003 Logical Disk** class will be applied only to objects that meet that class definition.

> [!NOTE]
> In the Operations console, the term *target* is used instead of *class*.

Classes are defined in the Operations Manager management pack libraries and in individual product management packs that you import.

## Groups
In Operations Manager, a *group* is a logical set of objects that can be used to define the scope of overrides, views, user roles, and notifications. Some groups are provided in the Operations Manager installation, such as **All Windows Computers** group and **Agent Managed Computer Group**. You can create your own groups and add members to groups explicitly or dynamically.

## Overrides
You have seen that classes are used to target workflows such as rules and monitors. A monitor or rule is applied to a specific class. To change the value for a parameter of a rule or monitor, you create an override. You have the following options for applying your override:

-   **For all objects of class:** *Class*

    When you select this option for your override, the override settings apply to all objects in the class at which the rule or monitor is targeted.

-   **For a group**

    When you select this option for your override, the override settings apply only to members of the group. The rule or monitor without the override settings continues to apply to all objects in the targeted class except for those objects that are also members of the group used for the override.

    When you create a group, you save it to an unsealed management pack. However, an element in an unsealed management pack, such as an override, cannot reference an element in a different unsealed management pack, such as a group. If you are going to use a group to limit the application of an override, you must either save the group to the same unsealed management pack as the override, or you must seal the management pack that contains the group.

-   **For a specific object of class:** *Class*

    When you select this option for your override, the override settings apply only to the specified object. The rule or monitor without the override settings continues to apply to all other objects in the targeted class.

-   **For all objects of another class**

    When you select this option for your override, the override settings apply only to objects of a class other than the targeted class. The rule or monitor without the override settings continues to apply to all objects in the targeted class.

Overrides that apply to a class are applied first, then overrides that apply to a group, and finally overrides that apply to a specific object. For more information, see [Using the Enforced Attribute in Overrides](./Using-the-Enforced-Attribute-in-Overrides.md).

## How to Apply Overrides
Here are some examples of when you would use the override options.

### You want to change the priority of an alert
Select to override **For all objects of class:** *Class*.

### You want to change the priority of an alert for computers that meet a specific criteria
Select to override **For a group** and create a group that dynamically adds members based on specific criteria.

### You want to change the priority of an alert for a specific computer only
Select to override **For a specific object of class:** *Class*. You could also select **For a group** and create a group that has the specific computer added as an explicit member.

### You want to change the priority of an alert that applies to all operating systems for a specific operating system
Select **For all objects of another class** and select the class that represents the operating system for which you want to have a different alert priority.

### You want the rule or monitor to apply only to specific computers
In this common scenario, you must perform the following two tasks:

1.  Select to override **For all objects of class:** *Class*, and change **Enabled** to **False**. This will disable the rule or monitor.

2.  Select to override **For a group**, **For a specific object of class:** *Class*, or **For all objects of another class**, and change **Enabled** to **True**. This enables the rule or monitor for members of that group, the specified object, or the selected class only.

## See Also
[How to Override a Rule or Monitor](./How-to-Override-a-Rule-or-Monitor.md)
[How to Enable or Disable a Rule or Monitor](./How-to-Enable-or-Disable-a-Rule-or-Monitor.md)
[Using the Enforced Attribute in Overrides](./Using-the-Enforced-Attribute-in-Overrides.md)
[How to Enable Recovery and Diagnostic Tasks](./How-to-Enable-Recovery-and-Diagnostic-Tasks.md)


