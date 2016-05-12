---
title: About Groups, Queues, and Lists
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1202fb9-32a4-40c3-99b4-c709dfcbac55
robots: noindex,nofollow
---
# About Groups, Queues, and Lists
The **Library** pane in [!INCLUDE[smlong12](Token/smlong12_md.md)] contains items, such as groups, queues, and lists. You can use groups to manage configuration items, and you can use queues to manage work items. You can use lists to customize forms.

## Using Groups to Manage Configuration Items
In [!INCLUDE[smshort](Token/smshort_md.md)], groups contain objects. Typically, these objects are configuration items. Groups can include collections of objects of the same class or of different classes. For example, say that you decide to create the **Exchange Servers** group. You have several methods to do this. You can create a static group, a dynamic group, or a combination of static and dynamic groups. A static group is defined by specific objects, such as “Exchange1” and “Exchange2”. A dynamic group is defined by inclusion rules. Inclusion rules are based on comparing a formula to the actual property value of a configuration item. The following table shows samples of inclusion rules.

|Class.Property|Operator|Value|
|------------------|------------|---------|
|Active Directory.Domain|Contains|Woodgrove|
|Windows Server.Display Name|Contains|Exchange Servers|
|Operating System.Display Name|Starts with|Windows Server|

For example, say that you want to restrict access to Exchange servers to only specific users. To do this, you create a new group that is named **Exchange Servers** and add all Exchange servers in this environment to the group. Later, you can configure user roles to limit access to the **Exchange Servers** group to only the specific users to whom you want to grant access. You can use the **Exchange Servers** group as criteria when you configure notification subscriptions. You can also use the **Exchange Servers** group as criteria for a report parameter.

## Using Queues to Manage Work Items
In [!INCLUDE[smshort](Token/smshort_md.md)], queues are used to group similar work items that meet specified criteria, for example, all incidents that are classified by analysts as E\-mail incidents. All work items in a queue must be of the same type, such as incidents, change requests, activities, or trouble tickets. Queues use membership rules to determine which work items should be included in each queue. Queue membership rules are dynamic, and they are periodically recalculated to ensure that the queue membership list is current.

You can create a queue to group work items with a specific type or with a specific priority. You can then configure user roles to limit access to that queue to only specific users.

For incident escalation, you can use queues in various ways to speed the resolution of higher priority or common incidents. For example, you can configure Incident Management to automatically escalate specific incidents to a high\-priority queue

For example, you can use queues as follows:

-   In notifications, you can use a queue as criteria in a subscription to specify which work items to notify about.

-   In security, you can use a queue in user role configuration to limit the scope of control that groups of users have over work items.

> [!NOTE]
> When you delete a queue, the work items that are contained in the queue are preserved. You can delete a queue only if it is in an unsealed management pack.

## Using Lists to Customize Forms
You can use lists in [!INCLUDE[smshort](Token/smshort_md.md)] to classify different objects, such as incidents, change requests, activities, or configuration items. A list represents a property of an object, and it includes one or more *list items*. Each list item represents a possible value for a property.

Lists are used in forms and dialog boxes throughout the [!INCLUDE[smcons](Token/smcons_md.md)]. Lists and list items make it possible for users to select a value from a predefined list of values. When you use lists, you can customize the console to reflect the business practices of your organization. Additionally, [!INCLUDE[smshort](Token/smshort_md.md)] contains several predefined lists, such as the **Incident Classification** list.

For example, when you are creating an incident, you notice that **Printer Problems** is an option under **Classification Category**. At your company, some standard laser printers in your accounting department might be used as specialized check\-writing printers. To better route incidents, you want printer\-related incidents to be categorized as being either for standard laser printers or for check\-writing printers. Because lists are customizable, you can add a list item, such as **Laser Printers** and **Check\-Writing Printers**, to the **Classification Category** list when you create an incident. Optionally, you can build lists as a hierarchy; for example, laser printers and check\-writing printers could be listed under printers. To do this, you can add **Laser Printer** and **Check\-Writing Printer** list items to the **Incident Classification** list.

### About List Items
In [!INCLUDE[smshort](Token/smshort_md.md)], several default list items exist. It is important that you not delete the default list items. Each default list item is defined by a globally unique identifier \(GUID\). Some of the default management packs reference these list items by their GUID. If you delete a list item, some management packs or workflows might not work.

If the name of a default list item causes an issue in your environment, you can change the display name of the existing item but leave the GUID intact. For example, you can change the name of the **Printing Problems** default list item to *Laser Printing Problems* if that is better in your environment.

## See Also
[How to Create a Group](How-to-Create-a-Group.md)
[How to Create a Queue](How-to-Create-a-Queue.md)
[How to Edit a Queue](How-to-Edit-a-Queue.md)
[How to Add a List Item](How-to-Add-a-List-Item.md)


