---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Using Groups, Queues, and Lists in System Center 2016   Service Manager
ms.technology:  service-manager
ms.assetid:  360fa976-6b9c-4521-a9d4-77250233449e
---

# Using Groups, Queues, and Lists in System Center 2016 - Service Manager
In Service Manager, you can use groups to manage configuration items, queues to manage work items, and lists to customize forms to classify different objects, such as incidents, change requests, activities, or configuration items. Use the overview and the procedures in the following topics to help manage these items.

## About Groups, Queues, and Lists

The **Library** pane in Service Manager contains items, such as groups, queues, and lists. You can use groups to manage configuration items, and you can use queues to manage work items. You can use lists to customize forms.

### Using Groups to Manage Configuration Items
In Service Manager, groups contain objects. Typically, these objects are configuration items. Groups can include collections of objects of the same class or of different classes. For example, say that you decide to create the **Exchange Servers** group. You have several methods to do this. You can create a static group, a dynamic group, or a combination of static and dynamic groups. A static group is defined by specific objects, such as “Exchange1” and “Exchange2”. A dynamic group is defined by inclusion rules. Inclusion rules are based on comparing a formula to the actual property value of a configuration item. The following table shows samples of inclusion rules.

|Class.Property|Operator|Value|
|------------------|------------|---------|
|Active Directory.Domain|Contains|Woodgrove|
|Windows Server.Display Name|Contains|Exchange Servers|
|Operating System.Display Name|Starts with|Windows Server|

For example, say that you want to restrict access to Exchange servers to only specific users. To do this, you create a new group that is named **Exchange Servers** and add all Exchange servers in this environment to the group. Later, you can configure user roles to limit access to the **Exchange Servers** group to only the specific users to whom you want to grant access. You can use the **Exchange Servers** group as criteria when you configure notification subscriptions. You can also use the **Exchange Servers** group as criteria for a report parameter.

### Using Queues to Manage Work Items
In Service Manager, queues are used to group similar work items that meet specified criteria, for example, all incidents that are classified by analysts as E-mail incidents. All work items in a queue must be of the same type, such as incidents, change requests, activities, or trouble tickets. Queues use membership rules to determine which work items should be included in each queue. Queue membership rules are dynamic, and they are periodically recalculated to ensure that the queue membership list is current.

You can create a queue to group work items with a specific type or with a specific priority. You can then configure user roles to limit access to that queue to only specific users.

For incident escalation, you can use queues in various ways to speed the resolution of higher priority or common incidents. For example, you can configure Incident Management to automatically escalate specific incidents to a high-priority queue

For example, you can use queues as follows:

-   In notifications, you can use a queue as criteria in a subscription to specify which work items to notify about.

-   In security, you can use a queue in user role configuration to limit the scope of control that groups of users have over work items.

> [!NOTE]
> When you delete a queue, the work items that are contained in the queue are preserved. You can delete a queue only if it is in an unsealed management pack.

### Using Lists to Customize Forms
You can use lists in Service Manager to classify different objects, such as incidents, change requests, activities, or configuration items. A list represents a property of an object, and it includes one or more *list items*. Each list item represents a possible value for a property.

Lists are used in forms and dialog boxes throughout the Service Manager console. Lists and list items make it possible for users to select a value from a predefined list of values. When you use lists, you can customize the console to reflect the business practices of your organization. Additionally, Service Manager contains several predefined lists, such as the **Incident Classification** list.

For example, when you are creating an incident, you notice that **Printer Problems** is an option under **Classification Category**. At your company, some standard laser printers in your accounting department might be used as specialized check-writing printers. To better route incidents, you want printer-related incidents to be categorized as being either for standard laser printers or for check-writing printers. Because lists are customizable, you can add a list item, such as **Laser Printers** and **Check-Writing Printers**, to the **Classification Category** list when you create an incident. Optionally, you can build lists as a hierarchy; for example, laser printers and check-writing printers could be listed under printers. To do this, you can add **Laser Printer** and **Check-Writing Printer** list items to the **Incident Classification** list.

### About List Items
In Service Manager, several default list items exist. It is important that you not delete the default list items. Each default list item is defined by a globally unique identifier (GUID). Some of the default management packs reference these list items by their GUID. If you delete a list item, some management packs or workflows might not work.

If the name of a default list item causes an issue in your environment, you can change the display name of the existing item but leave the GUID intact. For example, you can change the name of the **Printing Problems** default list item to *Laser Printing Problems* if that is better in your environment.


## How to Create a Group

Use the following procedures to create a new group (such as the **Exchange Servers** group) that includes the servers in your environment that are running Microsoft Exchange Server.

> [!NOTE]
> We recommend that you create a Configuration Manager connector before you run this procedure.

### To create a new group

1.  In the Service Manager console, click **Library**.

2.  In the **Library** pane, expand **Library**, and then click **Groups**.

3.  In the **Tasks** pane, under **Groups**, click **Create Group**. The Create Group Wizard starts.

4.  On the **Before You Begin** page, click **Next**.

5.  On the **General** page, do the following:

    1.  Provide a name for the group, such as **Exchange Servers**.

    2.  In the **Description** text box, type a description for the group. For example, type **All Exchange servers that require an update.**

    3.  Under **Management pack**, make sure that an unsealed management pack is selected. For example, select **Service Catalog Generic Incident Request**. Then, click **Next**.

6.  On the **Included Members** page, click **Add**.

7.  In the **Select Objects** dialog box, in the **Filter by class** list, select a class, such as **Windows Computer**.

8.  In the **Search by name** box, type the search criteria that you want to use to locate an object, and then click the filter (magnifying glass) button.

9. Select one or more items in the **Available Objects** list, and then click **Add**. For example, select all the Exchange servers in your organization.

10. Verify that the objects that you selected in the **Available Objects** list appear in the **Selected objects** list, and then click **OK**.

11. On the **Included Members** page, click **Next**.

12. Optionally, on the **Dynamic members** page, click the ellipsis (…) button to specify a type, such as **Windows Computer**, to build the dynamic members. Choose any property you want to build your criteria. For example, after you specify the **Windows Computer** type, select the **Principal Name** property, and then click **Add**. In the related text box, enter **woodgrove** so that all the computers whose principal name contains this text are included, and then click **Next**.

13. Optionally, on the **Subgroups** page, click **Add**, and then select the specific groups that you want as subgroups of this group. If any group that you want to select as a subgroup is from an unsealed management pack, that subgroup must be from the same management pack as the group that you are creating. Click **OK**, and then click **Next**.

14. Optionally, on the **Excluded Members** page, click **Add**, and then select the specific configuration items that you want to exclude from this group. Click **OK**, and then click **Next**.

15. On the **Summary** page, confirm the group settings that you made, and then click **Create**.

16. On the **Completion** page, make sure that you receive the following confirmation message, and then click **Close**:

    `The new group was created successfully.`

### To validate the creating of a new group

-   Make sure that **Exchange Servers** appears in the **Groups** pane. If necessary, press the F5 key to refresh the Service Manager console view.

    In the **Tasks** pane, under the name of the group, click **View Group Members** to make sure that the Exchange servers appear in the **Group Members** window.

![](../../media/pssymbol.png)You can use a Windows PowerShell command to retrieve groups from Operations Manager and from Service Manager. For more information, see [Get-SCSMGroup](http://go.microsoft.com/fwlink/p/?LinkID=225402).



## How to Create a Queue

You can create queues to create a grouping of related work items, such as incidents and change requests. For example, you can create a queue that you use for escalation, named **Exchange Send Problems Queue**, and then escalate that type of incident to that queue.

You can use the following procedure to create a queue.

### To create a queue

1.  In the Service Manager console, click **Library**.

2.  In the **Library** pane, expand **Library**, and then click **Queues**.

3.  In the **Tasks** pane, click **Create Queue**.

4.  Complete these steps to complete the Create Queue Wizard:

    1.  On the **Before You Begin** page, click **Next**.

    2.  On the **General** page, type a name in the **Queue name** box. For example, type **Exchange Send Problems Queue**.

    3.  Next to the **Work item type** box, click the ellipsis button (**…**). In the **Select a Class** dialog box, select a class, such as **Incident**, and then click **OK**.

    4.  In the **Management pack** list, select the unsealed management pack in which you want to store the new queue definition. For example, select **Service Manager Incident Management Configuration Library**. Then, click **Next**.

    5.  On the **Criteria** page, build the criteria that you want to use to filter work items for the queue, and then click **Next**. Only work items that meet the specified criteria will be added to that queue.

        For example, select the **Classification Category** property in the **Available Properties** area, and then click **Add**. In the list that was just added to the **Criteria** area, in the area that is now surrounded by a red box, select **E-Mail Problems**, and then click **Next**.

    6.  On the **Summary** page, click **Create** to create the queue.

    7.  On the **Completion** page, click **Close**.

### To validate the creation of a queue

1.  In the Service Manager console, verify that the new queue appears in the **Queues** pane.

2.  In the **Tasks** pane, click **Properties**, and then verify that the queue appears as you defined it.

![](../../media/pssymbol.png)You can use a Windows PowerShell command to complete this task. For information about how to use Windows PowerShell to retrieve queues that are defined in Service Manager, see [Get-SCSMQueue](http://go.microsoft.com/fwlink/p/?LinkId=225331).



## How to Edit a Queue

You can use the following procedure to edit a queue.

### To edit a queue

1.  In the Service Manager console, click **Library**.

2.  In the **Library** pane, expand **Library**, and then click **Queues**.

3.  In the **Queues** pane, select the queue that you want to edit, such as **Exchange Send Problems Queue**. Then, in the **Tasks** pane, click **Properties**.

4.  In the **Queue Properties** dialog box, on the **General** and **Criteria** tabs, make the changes you want. For example, change the description of the queue.

5.  Click **OK** to save the changes.



## How to Add a List Item
You can use these procedures to add a list item to an existing list and then validate it. For example, you can use this procedure to add a Laser Printer and Check-Writing Printer list item to the **Incident Classification** list.

### To add list items to Service Manager lists

1.  In the Service Manager console, click **Library**.

2.  In the **Library** pane, click **Lists**. The **Lists** pane displays all the existing lists.

3.  Select the list to which you want to add a list item. For example, select the **Incident Classification** list. In the **Tasks** pane, under **Incident Classification**, click **Properties**.

4.  In the **List Properties** dialog box, click **Printing Problems**, and then click **Add Child**. Notice that a new **List Value** list item is added.

    > [!NOTE]
    > When you click **Add Item** or **Add Child**, a **Select management pack** dialog box might appear. If this dialog box appears, select the default management pack, select another unsealed management pack, or create a new management pack.

5.  Click the new **List Value** list item. In the **Name** box, type a name for the new list item. For example, type **Laser Printer**. If you want, you can optionally type a description in the **Description** box.

6.  Repeat steps 4 and 5 and create a new list item with the name **Check-Writing Printer**, and then click **OK**.

### To validate the addition of a new list item

1.  Select the same list again, click **Properties** in the **Tasks** pane, and then verify that the new list item appears.

2.  In the Service Manager console, create a new incident, and then locate the new list item in the **Classification Category** list. For example, expand **Printer Problems**, and then locate the **Laser Printer** and **Check-Writing Printer** list items.


