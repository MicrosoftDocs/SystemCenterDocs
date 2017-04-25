---
title: Configure the Activities Toolbox
description: You can configure the activities toolbox in the Service Manager Authoring Tool to add or remove custom activities and to personalize it.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fed6eb78-2fb6-432d-9c47-8d3502956ab4
---

# Configure the Activities Toolbox in the Service Manager Authoring Tool

>Applies To: System Center 2016 - Service Manager

There are two ways to configure the Activities Toolbox in the Service Manager Authoring Tool:

- Modify the default toolbox by adding or removing custom activities. These changes require administrative-level permissions, and they are visible to all users of the Authoring Tool.

- Personalize the toolbox. These changes do not require special permissions. Changes made by one user affect only that user.

## Modify the default toolbox

If the default set of Windows Workflow Foundation (WF) activities does not meet the needs of your organization, you can use custom activities with the Service Manager Authoring Tool. Custom activities include activities you or your organization develops or activities that non-Microsoft parties develop. These activities must be compiled into assembly files (*activitysetname*.dll). For information about developing WF activities, see the [Workflow Activity Reference](http://go.microsoft.com/fwlink/p/?LinkID=233694).

Installing or removing custom activity assemblies changes the set of available activities for all Authoring Tool users. When you install or remove an activity assembly, remember to notify Authoring Tool users of the changes. Custom activities do not appear automatically in the Activities Toolbox; in order to use custom activities, users must add them to personalized activity groups.

### Install a custom activity assembly

So that you can use custom or third-party Windows Workflow Foundation (WF)  activities in workflows, the activity assembly files must first be installed. You must have administrative permissions on the computer running the Service Manager Authoring Tool and the computer running Service Manager. Like the default activities, custom activities must be available on the computer running Service Manager as well as on the computer running the Authoring Tool.

1. On the computer running the Authoring Tool, browse to the Authoring Tool Workflow Activity Library folder, for example, D:Program Files (x86)Microsoft System CenterService Manager 2016 AuthoringWorkflow Activity Library. Paste the custom activity assembly into this folder.

2. On the computer running Service Manager, browse to the Service Manager installation folder, and then paste the custom activity assembly into this folder.

3. After you have installed the custom activity assembly, notify the Authoring Tool users that they can now add the custom activities to personalized activity groups, by using the following procedures:

    > [!NOTE]
    > Users can only add custom activities to personalized activity groups; they cannot add custom activities to the default activity groups.

### Remove a custom activity assembly

To remove a custom activity assembly, you must have administrative permissions on the computer running the Service Manager Authoring Tool and on the computer running the Service Manager console. After the custom activity assembly has been removed, the activities compiled into that assembly are no longer available in personalized activity groups.

1. On the computer running the Authoring Tool, browse to the Authoring Tool Workflow Activity Library folder, for example, D:Program Files (x86)Microsoft System CenterService Manager 2016 AuthoringWorkflow Activity Library. Remove the custom activity assembly from this folder.

2. On the computer running the Service Manager console, browse to the Service Manager installation folder. Remove the custom activity assembly from this folder.

3. After you have removed the custom activity assembly, notify the Authoring Tool users that the custom activities are no longer available.

## Personalize the activities toolbox

Use the procedures in this section to personalize the **Activities Toolbox** pane in the Service Manager Authoring Tool. Each user can personalize the **Activities Toolbox** differently; the Authoring Tool stores this information as part of each user's profile.

> [!IMPORTANT]
> You can only modify personalized activity groups. You cannot modify the default activity groups.

Use these procedures to create activity groups in the **Activities Toolbox** pane in the Service Manager Authoring Tool.

### Create a top-level activity group

1. In the **Activities Toolbox** pane, right-click **Activity Groups**, and then click **New Group**.

2. Enter a name for the new group.

### Create an activity subgroup

1. In the **Activities Toolbox** pane, right-click the parent group, and then click **New Group**.

2. Enter a name for the new group.

### Rename a personalized activity group

Use this procedure to change the name of a personalized activity group in the Service Manager Authoring Tool.

> [!IMPORTANT]
> You can only rename personalized activity groups. You cannot change the names of the default activity groups.

1. In the **Activities Toolbox** pane, right-click the group, and then click **Rename Group**.

2. Enter a new name for the group.

### Add activities to a personalized activity group

Use this procedure to add activities to a personalized activity group in the Service Manager Authoring Tool. Activities can belong to more than one group; for example, you can create a **Favorites** group and populate it with both default activities and custom activities that already belong to other groups.

> [!IMPORTANT]
> You can only add activities to personalized activity groups. You cannot add activities to the default activity groups.

If you want to use custom activities in workflows, you must add them to a group in order to make them available in the **Activities Toolbox** pane. Note that before you can add custom activities to groups, an administrator must install the appropriate activity assembly files on the computer running the Authoring Tool.

1. In the **Activities Toolbox** pane, right-click the group, and then click **Choose Activities**.

2. In the **Choose Activities for a Group** dialog box, scroll the list to find the activities you want to add. Select the check boxes for the activities you want to add.

3. If you want to use custom activities that do not appear in the list, click **Add Custom Activities**. In the **Select Custom Activity Assembly** dialog box, select the custom activity assembly file, and then click **Open**. This adds the custom activities from this assembly file to the activity list.

4. After you have selected all of the activities for the group, click **OK**.

### Remove activities from a personalized activity group

Use this procedure to remove activities from a personalized activity group in the Service Manager Authoring Tool. Note that removing an activity from a group does not remove the activity from the Activity Library or from any other group.

> [!IMPORTANT]
> You can only remove activities from personalized activity groups. You cannot remove activities from  the default activity groups.

1. In the **Activities Toolbox** pane, right-click the group, and then click **Choose Activities**.

2. In the **Choose Activities for a Group** dialog box, scroll the list to find the activities you want to remove. Clear the check boxes for the activities you want to remove, and then click **OK**.

### Delete a personalized activity group

Use this procedure to delete an activity group in the Service Manager Authoring Tool. If the activity group contains one or more subgroups, the subgroups will also be deleted. Note that deleting an activity group does not remove its member activities from the Activity Library or from any other groups.

> [!IMPORTANT]
> You can only delete personalized activity groups. You cannot delete the default activity groups.

- In the **Activities Toolbox** pane, right-click the group, and then click **Delete Group**.
