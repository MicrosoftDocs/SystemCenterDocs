---
title: Active Directory Activities
description: The following configuration instructions apply to all activities in this integration pack.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 73d76ac0-8eee-466a-b11b-3df39e045d6d
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Active Directory Activities

Applies To: System Center 2016 - Orchestrator

The following configuration instructions apply to all activities in this integration pack.

## Activity properties

Each activity has a set of required or optional properties that define the configuration of that activity. This includes how it connects to other activities or how the activity performs its actions. You can view or modify activity properties in the Runbook Designer.

#### To configure the properties for an activity

1.  Double-click the activity that you want to configure. Alternatively, you can right-click the activity, and then click **Properties**.

2.  Click **Finish**, to save your configuration entries.

In the activity Properties dialog box, there are several tabs that provide access to general and specific settings for the activity. The number of available tabs for object properties varies from one activity to another.

### General tab

This tab contains the **Name** and **Description** properties for the Active Directory Activities. By default, the **Name** of the activity is the same as its activity type, and the **Description** is blank. You can modify these properties to create more descriptive names or provide detailed descriptions of the activity actions.

### Properties tab

This tab contains properties that are specific to the activity. All activities in this integration pack have the **Configuration Name** property on the **Properties or Filters** tab. You can use this property to specify the connection to the Active Directory domain.

#### To configure the Connection Name property

1.  Click the ellipsis **(...)** button next to the **Name** field.

2.  Select the applicable connection name. Connections that are displayed in the list have been previously configured as described in.

### Filter behavior

The Monitor and Get activities use filters to determine the values that will invoke a runbook or retrieve activities. The property values of potential candidates are compared to the values of the filters to determine if the candidates meet the criteria. Then, you can select one of the available methods of comparison. You are provided with an option to either match or not match the filter using each method. For example, the "Does not" version of a method finds the messages that do not match the filter to trigger the runbook.

-   **Equals**: the property of the message exactly matches the text or number specified in the filter.
-   **Does not equal**: the property of the message does not exactly match the text or number specified in the filter.
-   **Is less than**: the property of the message is less than the number specified in the filter.
-   **Is less than or equal to**: the property of the message is less than or equal to the number specified in the filter.
-   **Is greater than**: the property of the message is greater than the number specified in the filter.
-   **Is greater than or equal to**: the property of the message is greater than or equal to the number specified in the filter.
-   **Contains**: the property of the message contains the exact text specified in the filter. Unlike the Equals behavior, there can be other text surrounding the matching text.
-   **Does not contain**: the property of the message does not contain the exact text specified in the filter. Unlike the Equals behavior, there can be other text surrounding the matching text.
-   **Starts with**: the property of the message starts with the exact text specified in the filter.
-   **Ends with**: the property of the message ends with the exact text specified in the filter.

### Run Behavior tab

The Behavior tab contains the properties that determine how the activity handles the multi-value published data, and what notifications will be sent if the activity fails or runs for an excessive period of time.

#### Multi-value published data behavior

The Get activity option retrieves information from another activity or outside source, and can return one or more values in the published data. For example, when you use the Get Collection Member activity, the data output from that activity might be a list of computers that belong to the specified collection.

By default, the data from the Get activity will be passed on as multiple individual outputs. This invokes the next activity as many times as there are items in the output. Alternatively, you can provide a single output for the activity by enabling the **Flatten** option. When you enable this option, you must also choose a formatting option:

-   **Separate with line breaks**. Each item is on a new line. This format is useful for creating human-readable text files for the output.
-   **Separate with \_** . Each item is separated by one or more characters of your choice.
-   **Use CSV format**. All items are in a comma-separated value (CSV) format. You can use this format to import data into spreadsheets or other applications.

The activity will produce a new set of data every time it runs. The **Flatten** feature does not flatten data across multiple instances of the same activity.

#### Event notifications

Some activities are expected to take a specific amount of time to complete. If they do not complete within that time, then they might be stalled or there might be another issue that prevents them to complete. You can define the amount of time in which action has to complete. After this period, a platform event will be sent and the issue will be reported. You can also choose whether to generate a platform event if the activity returns a failure.

#### To be notified when the activity takes longer to run than the specified time, or if the activity fails to run

1.  In the **Event Notifications** box, enter the **number of seconds** of run time before a notification is generated.

2.  Select **Report if activity fails to run**, to generate run failure notifications.

For more information about Orchestrator events, see [Activity Events](https://technet.microsoft.com/en-us/library/hh489611.aspx).

## Published data

Published data is the foundation of a working runbook. It is the data produced as a result of the actions of an activity. This data is published to an internal data bus that is unique for each runbook. Subsequent activities in the runbook can subscribe to this data and use it in their configuration. The link conditions also use this information to add decision-making capabilities to runbooks.

An activity can subscribe to data only from the activities that are linked before it in the runbook. You can use published data to automatically populate the property values that are needed by activities.

#### To use published data

1.  Right-click the **Property Value** box, click **Subscribe**, and then click **Published Data**.

2.  Click the **Activity** drop-down box and select the activity from which you want to obtain the data. To view additional data elements that are common to all runbooks, select **Show Common Published Data**.

3.  Click the published data element that you want to use, and then click **OK**.

For a list of the data elements published by each activity, see the Published Data tables in the activity topic. For information about the common published data items, see [Common Published Data](https://technet.microsoft.com/en-us/library/e339c027-4c69-43e5-a59b-ac7ea0a676c8#CommonPublishedData).

## Activities

This integration pack adds the Microsoft Active Directory category to the **Activity** pane in the Runbook Designer. This category contains the following activities:

[Add Computer To Group](add-computer-to-group.md)

[Add Group To Group](add-group-to-group.md)

[Add User To Group](add-user-to-group.md)

[Create Computer](create-computer.md)

[Create Group](create-group.md)

[Create User](../orch/manage/create-user.md)

[Delete Computer](../orch/manage/delete-computer.md)

[Delete Group](../orch/manage/delete-group.md)

[Delete User](../orch/manage/delete-user.md)

[Disable Computer](../orch/manage/disable-computer.md)

[Disable User](../orch/manage/disable-user.md)

[Enable Computer](../orch/manage/enable-computer.md)

[Enable User](../orch/manage/enable-user.md)

[Get Computer](../orch/manage/get-computer.md)

[Get Group](../orch/manage/get-group.md)

[Get Organizational Unit](../orch/manage/get-organizational-unit.md)

[Get User](../orch/manage/get-user.md)

[Move Computer](../orch/manage/move-computer.md)

[Move Group](../orch/manage/move-group.md)

[Move User](../orch/manage/move-user.md)

[Remove Computer From Group](../orch/manage/remove-computer-from-group.md)

[Remove Group From Group](../orch/manage/remove-group-from-group.md)

[Remove User From Group](../orch/manage/remove-user-from-group.md)

[Rename Group](../orch/manage/rename-group.md)

[Rename User](../orch/manage/rename-user.md)

[Reset User Password](../orch/manage/reset-user-password.md)

[Unlock User](../orch/manage/unlock-user.md)

[Update Computer](../orch/manage/update-computer.md)

[Update Group](../orch/manage/update-group.md)

[Update User](../orch/manage/update-user.md)


