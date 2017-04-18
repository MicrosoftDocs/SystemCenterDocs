---
title: HP Operations Manager Activities
description: The following configuration instructions apply to all activities in this integration pack.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dd525101-1078-46d0-93a5-f0761c6ad5e8
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# HP Operations Manager Activities

Applies To: System Center 2016 - Orchestrator

The following configuration instructions apply to all activities in this integration pack.

## Activity Properties

Each activity has a set of required or optional properties that define the configuration of that activity. This includes how it connects to other activities or how the activity performs its actions. You can view or modify activity properties in the Runbook Designer.

#### To configure the properties for an activity

1.  Double-click the activity. Alternatively, you can right-click the activity, and then click **Properties**.

2.  To save your configuration entries, click **Finish**.

In the activity properties dialog box, several tabs along the left side provide access to general and specific settings for the activity. The number of available tabs for object properties differs from activity to activity

### General Tab

This tab contains the **Name** and **Description** properties for the activity. By default, the **Name** of the activity is the same as its activity type, and the **Description** is blank. You can modify these properties to create more descriptive names or provide detailed descriptions of the actions of the activity.

### Properties Tab

This tab contains properties that are specific to the activity. All activities in this integration pack have the **Configuration Name** property at the top of the **Properties or Filters** tab. This property is used to specify the connection to the HP Operations Manager management server.

#### To configure the Configuration Name property

1.  Click the ellipsis **(...)** button next to the **Name** field.

2.  Select the applicable connection name. Connections displayed in the list have been previously configured as described in <span>Configuring the HP Operations Manager Connections</span>.

### Filter Behavior

The Monitor and Get activities use filters to determine the values that will invoke a runbook or retrieve activities. Property values of potential candidates are compared to the values of the filters to determine if they meet the criteria. When matching against values, you select one of the available methods of comparison. An option is provided to either match or not match the filter using each method. For example, the "Does not" version of a method finds messages that do not match the filter to trigger the policy.

-   **Equals**: the property of the message exactly matches the text or number specified in the filter.
-   **Does not equal**: the property of the message does not exactly match the text or number specified in the filter.
-   **Is less than**: the property of the message is less than the number specified in the filter.
-   **Is less than or equal to**: the property of the message is less than or equal to the number specified in the filter.
-   **Is greater than**: the property of the message is greater than the number n the filter.
-   **Is greater than or equal to**: the property of the message is greater than or equal to the number specified in the filter.
-   **Contains**: the property of the message contains the exact text specified in the filter. Unlike the Equals behavior, there can be other text surrounding the matching text.
-   **Does not contain**: the property of the message does not contain the exact text specified in the filter. Unlike the Equals behavior, there can be other text surrounding the matching text.
-   **Matches pattern**: use regular expressions to specify a pattern that the text must match.
-   **Does not match pattern**: use regular expressions to specify a pattern that the text must not match.
-   **Starts with**: the property of the message starts with the exact text specified in the filter.
-   **Ends with**: the property of the message starts with the exact text specified in the filter.
-   **Is greater than**: the property of the message is after the date/time specified in the filter.
-   **Is less than**: the property of the message is before the date/time specified in the filter.

### Run Behavior Tab

This tab contains the properties that determine how the activity handles multi-value published data and what notifications will be sent if the activity fails or runs for an excessive period of time.

#### Multi-Value Published Data Behavior

Get activities retrieve information from another activity or outside source, and can return one or more values in the published data. For example, when you use the Get Collection Member activity, the data output from that activity might be a list of computers that belong to the specified collection.

By default, the data from the Get activity will be passed on as multiple individual outputs. This invokes the next activity as many times as there are items in the output. Alternatively, you can provide a single output for the activity by enabling the **Flatten** option. When you enable this option, you also choose a formatting option:

-   **Separate with line breaks**. Each item is on a new line. This format is useful for creating human-readable text files for the output.
-   **Separate with \_** . Each item is separated by one or more characters of your choice.
-   **Use CSV format**. All items are in CSV (comma-separated value) format. This format is useful for importing data into spreadsheets or other applications.

The activity will produce a new set of data every time it runs. The **Flatten** feature does not flatten data across multiple instances of the same activity.

#### Event Notifications

Some activities are expected to take a limited amount of time to complete. If they do not complete within that time they may be stalled or there may be another issue preventing them from completing. You can define the number of seconds to wait for completion of the action. After this period a platform event will be sent and the issue will be reported. You can also choose whether to generate a platform event if the activity returns a failure.

#### To be notified when the activity takes longer than a specified time to run or fails to run

1.  In the **Event Notifications** box, enter the **number of seconds** of run time before a notification is generated.

2.  Select **Report if activity fails to run** to generate run failure notifications.

For more information about Orchestrator events, see [Activity Events](https://technet.microsoft.com/en-us/library/hh489611.aspx).

## Published Data


Published data is the foundation of a working runbook. It is the data produced as a result of the actions of an activity. This data is published to an internal data bus that is unique for each runbook. Subsequent activities in the runbook can subscribe to this data and use it in their configuration. Link conditions also use this information to add decision-making capabilities to runbooks.

An activity can only subscribe to data from the activities that are linked before it in the runbook. You can use published data to automatically populate the property values needed by activities.

#### To use published data

1.  Right-click the property value box, click **Subscribe**, and then click **Published Data**.

2.  Click the **Activity** drop-down box and select the activity from which you want to obtain the data. To view additional data elements common to all runbooks, select **Show Common Published Data**.

3.  Click the published data element that you want to use, and then click **OK**.

For a list of the data elements published by each activity, see the Published Data tables in the activity topic. For information about the common published data items, see [Common Published Data](https://technet.microsoft.com/en-us/library/e339c027-4c69-43e5-a59b-ac7ea0a676c8#CommonPublishedData).

## Activities

This integration pack adds the HP Operations Manager category to the **Activities** pane in the Runbook Designer. This category contains the following activities:

[Acknowledge Message](acknowledge-message.md)

[Add Annotation to Message](../orch/manage/add-annotation-to-message.md)

[Create Message](../orch/manage/create-message.md)

[Delete Annotation](../orch/manage/delete-annotation.md)

[Delete Custom Attribute](../orch/manage/delete-custom-attribute.md)

[Get Annotation](../orch/manage/get-annotation.md)

[Get Message](../orch/manage/get-message.md)

[Launch Tool](../orch/manage/launch-tool.md)

[Monitor Message](../orch/manage/monitor-message.md)

[Own/Disown Message](../orch/manage/own-or-disown-message.md)

[Set Custom Attribute](../orch/manage/set-custom-attribute.md)

[Update Annotation](../orch/manage/update-annotation.md)

[Update Message](../orch/manage/update-message.md)
