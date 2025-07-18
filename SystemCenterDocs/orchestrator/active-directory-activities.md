---
title: Active Directory Activities
description: This article contains configuration instructions for Active Directory activities.
ms.custom: UpdateFrequency2, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 73d76ac0-8eee-466a-b11b-3df39e045d6d
author: jyothisuri
ms.author: jsuri
robots: noindex
---
# Active Directory Activities

The following configuration instructions apply to all activities in this integration pack.

## Activity properties

Each activity has a set of required or optional properties that define the configuration of that activity. This includes how it connects to other activities or how the activity performs its actions. You can view or modify activity properties in the Runbook Designer.

### Configure the properties for an activity

1. Double-click the activity that you want to configure. Alternatively, you can right-click the activity and select **Properties**.

2. Select **Finish** to save your configuration entries.

In the activity Properties dialog, there are several tabs that provide access to general and specific settings for the activity. The number of available tabs for object properties varies from one activity to another.

### General tab

This tab contains the **Name** and **Description** properties for the Active Directory Activities. By default, the **Name** of the activity is the same as its activity type, and the **Description** is blank. You can modify these properties to create more descriptive names or provide detailed descriptions of the activity actions.

### Properties tab

This tab contains properties that are specific to the activity. All activities in this integration pack have the **Configuration Name** property on the **Properties or Filters** tab. You can use this property to specify the connection to the Active Directory domain.

#### Configure the Connection Name property

1. Select the ellipsis **(...)** button next to the **Name** field.

2. Select the applicable connection name. Connections that are displayed in the list have been previously configured as described in.

### Filter behavior

The Monitor and Get activities use filters to determine the values that will invoke a runbook or retrieve activities. The property values of potential candidates are compared to the values of the filters to determine if the candidates meet the criteria. Then you can select one of the available methods of comparison. You're provided with an option to either match or not match the filter using each method. For example, the "Does not" version of a method finds the messages that don't match the filter to trigger the runbook.

- **Equals**: The property of the message exactly matches the text or number specified in the filter.
- **Does not equal**: The property of the message doesn't exactly match the text or number specified in the filter.
- **Is less than**: The property of the message is less than the number specified in the filter.
- **Is less than or equal to**: The property of the message is less than or equal to the number specified in the filter.
- **Is greater than**: The property of the message is greater than the number specified in the filter.
- **Is greater than or equal to**: The property of the message is greater than or equal to the number specified in the filter.
- **Contains**: The property of the message contains the exact text specified in the filter. Unlike the Equals behavior, there can be other text surrounding the matching text.
- **Does not contain**: The property of the message doesn't contain the exact text specified in the filter. Unlike the Equals behavior, there can be other text surrounding the matching text.
- **Starts with**: The property of the message starts with the exact text specified in the filter.
- **Ends with**: The property of the message ends with the exact text specified in the filter.

### Run Behavior tab

The Behavior tab contains the properties that determine how the activity handles the multi-value published data, and what notifications will be sent if the activity fails or runs for an excessive period of time.

#### Multi-value published data behavior

The Get activity option retrieves information from another activity or outside source and can return one or more values in the published data. For example, when you use the Get Collection Member activity, the data output from that activity might be a list of computers that belong to the specified collection.

By default, the data from the Get activity will be passed on as multiple individual outputs. This invokes the next activity as many times as there are items in the output. Alternatively, you can provide a single output for the activity by enabling the **Flatten** option. When you enable this option, you must also choose a formatting option:

- **Separate with line breaks**: Each item is on a new line. This format is useful for creating human-readable text files for the output.
- **Separate with \_**: Each item is separated by one or more characters of your choice.
- **Use CSV format**: All items are in a comma-separated value (CSV) format. You can use this format to import data into spreadsheets or other applications.

The activity will produce a new set of data every time it runs. The **Flatten** feature doesn't flatten data across multiple instances of the same activity.

#### Event notifications

Some activities are expected to take a specific amount of time to complete. If they don't complete within that time, then they might be stalled or there might be another issue that prevents them to complete. You can define the amount of time in which an action has to complete. After this period, a platform event will be sent and the issue will be reported. You can also choose whether to generate a platform event if the activity returns a failure.

#### To be notified when the activity takes longer to run than the specified time, or if the activity fails to run

1. In the **Event Notifications** box, enter the **number of seconds** of run time before a notification is generated.

2. Select **Report if activity fails to run** to generate run failure notifications.

For more information about Orchestrator events, see [Activity Events](/previous-versions/system-center/system-center-2012-R2/hh489611(v=sc.12)).

## Published data

Published data is the foundation of a working runbook. It's the data produced as a result of the actions of an activity. This data is published to an internal data bus that is unique for each runbook. Subsequent activities in the runbook can subscribe to this data and use it in their configuration. The link conditions also use this information to add decision-making capabilities to runbooks.

An activity can subscribe to data only from the activities that are linked before it in the runbook. You can use published data to automatically populate the property values that are needed by activities.

### Use published data

1. Right-click the **Property Value** box, select **Subscribe**, and select **Published Data**.

2. Select the **Activity** dropdown box and select the activity from which you want to obtain the data. To view additional data elements that are common to all runbooks, select **Show Common Published Data**.

3. Select the published data element that you want to use, and select **OK**.

For a list of the data elements published by each activity, see the Published Data tables in the activities section. For information about the common published data items, see [Common Published Data](/previous-versions/system-center/system-center-2012-R2/hh403821(v=sc.12)#CommonPublishedData).

## Activities

This integration pack adds the Microsoft Active Directory category to the **Activity** pane in the Runbook Designer. This category contains the following activities:

- [Add Computer To Group](add-computer-to-group.md)

- [Add Group To Group](add-group-to-group.md)

- [Add User To Group](add-user-to-group.md)

- [Create Computer](create-computer.md)

- [Create Group](create-group.md)

- [Create User](create-user.md)

- [Delete Computer](delete-computer.md)

- [Delete Group](delete-group.md)

- [Delete User](delete-user.md)

- [Disable Computer](disable-computer.md)

- [Disable User](disable-user.md)

- [Enable Computer](enable-computer.md)

- [Enable User](enable-user.md)

- [Get Computer](get-computer.md)

- [Get Group](get-group.md)

- [Get Organizational Unit](get-organizational-unit.md)

- [Get User](get-user.md)

- [Move Computer](move-computer.md)

- [Move Group](move-group.md)

- [Move User](move-user.md)

- [Remove Computer From Group](remove-computer-from-group.md)

- [Remove Group From Group](remove-group-from-group.md)

- [Remove User From Group](remove-user-from-group.md)

- [Rename Group](rename-group.md)

- [Rename User](rename-user.md)

- [Reset User Password](reset-user-password.md)

- [Unlock User](unlock-user.md)

- [Update Computer](update-computer.md)

- [Update Group](update-group.md)

- [Update User](update-user.md)
