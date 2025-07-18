---
title: Exchange Users Activities
description: The configuration instructions in this article apply to all activities in the Exchange Users Integration Pack.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 624f4afd-f248-4e1c-a2c2-e747d2ed3fd4
author: jyothisuri
ms.author: jsuri
---

# Exchange Users Activities

The configuration instructions in this article apply to all the activities in the Exchange Users Integration Pack. Activities include creating, modifying, and managing tasks, appointments, emails, and contact groups. The task-specific configuration instruction articles for all activities include links to this article.

The procedures in this article are performed on any activity that has been placed in the runbook window of the Orchestrator Runbook Designer.

## Activity Properties

Each activity has a set of required or optional properties that define the configuration of that activity. The configuration defines how the activity performs its actions and how it connects to other activities as applicable. You can view or modify an activity's properties when the activity has been placed in the runbook window.

### View and configure the properties for an activity

1. Locate the activity in the runbook window and double-click the activity. Alternatively, you can right-click the activity, and select **Properties**.
2. To save your configuration entries, select **Finish**.

In the activity properties dialog, several tabs along the left side provide access to general and specific settings for the activity. The number of available tabs for object properties varies according to the activity type.

#### General Tab

The **General** tab contains the **Name** and **Description** properties for the activity. By default, the **Name** of the activity is the same as its activity type, and the **Description** is blank. You can modify these properties to create more descriptive names or to provide detailed descriptions of the actions of the activity.

#### Properties Tab

The **Properties** tab contains properties that are specific to the activity. All activities in this integration pack have the **Configuration Name** property at the top of the **Properties** or **Filters** tab. This property is used to specify the connection to the Exchange server.

### Configure the Configuration Name property

1. Select the ellipsis **(...)** button next to the **Name** field.

2. Select the applicable connection name. The connections that are displayed in the list have been previously configured as described in <span>Exchange Users Integration Pack for System Center - Orchestrator</span>.

### Filter Behavior

The **Monitor** and **Get** activities use filters to determine the values that will invoke a runbook or retrieve activities. Property values of potential candidates are compared to the values of the filters to determine if they meet the criteria. To specify filtering criteria, you can select one of the available methods of comparison. An option is provided to either match or not match the filter using each method. For example, the "Does not" version of a method finds any message that doesn't match the filter. All text filters are case sensitive. Here are the available filtering options:

- **Equals**: The property of the message matches the text or number specified in the filter.
- **Does not equal**: The property of the message doesn't match the text or number specified in the filter.
- **Is less than**: The property of the message is less than the number specified in the filter.
- **Is less than or equal to**: The property of the message is less than or equal to the number specified in the filter.
- **Is greater than**: The property of the message is greater than the number in the filter.
- **Is greater than or equal to**: The property of the message is greater than or equal to the number specified in the filter.
- **Contains**: The property of the message contains the exact text specified in the filter. Unlike the Equals filter behavior, there can be other text surrounding the matching text.
- **Does not contain**: The property of the message doesn't contain the exact text specified in the filter. Unlike the Equals filter behavior, there can be other text surrounding the matching text.
- **Starts with pattern**: The property of the message starts with the exact text specified in the filter. Unlike the Equals filter behavior, there can be other text following the matching text.

### The Run Behavior Tab

The **Run Behavior** tab contains the properties that determine how the activity handles multi-value published data and also determine what notifications will be sent if the activity fails or runs for an excessive period of time.

### Multi-Value Published Data Behavior

The **Get** activities retrieve information from another activity or outside source, and can return one or more values in the published data. For example, the data output from the **Get Item** activity could be the details of an existing appointment.

By default, the data from the **Get** activity will be passed on as multiple individual outputs. The multiple outputs will invoke the next activity as many times as there are items in the output. Alternatively, you can provide a single output for the activity by enabling the **Flatten** option. When you enable this option, you must choose a formatting option:

- **Separate with line breaks**. Each item is on a new line. This format is useful for creating human-readable text files for the output.
- **Separate with**. Each item is separated by one or more characters of your choice.
- **Use CSV format**. All the items are in a CSV (comma-separated value) format. This format is useful for importing data into spreadsheets or other applications.

The activity will produce a new set of data every time it runs. The **Flatten** feature doesn't flatten data across multiple instances of the same activity.

## Event Notifications

Some activities are expected to take a limited amount of time to complete. If they don't complete within that time, they might be stalled or there might be another issue preventing them from completing. You can define the number of seconds to wait for the completion of the action. After this specified time period, a platform event will be sent and the issue will be reported. You can also choose whether to generate a platform event if the activity returns a failure.

### To be notified when the activity takes longer than a specified time to run or fails to run

1. In the **Event Notifications** box, enter the **number of seconds** of run time before a notification is generated.
2. Select **Report if activity fails to run** to generate run failure notifications.

## Published Data

Published data is the foundation of a working runbook. It's the data produced as a result of the actions of an activity. This data is published to an internal data bus that is unique for each runbook. Subsequent activities in the runbook can subscribe to this data and use it in their configuration. Link conditions also use this information to add decision-making capabilities to runbooks.

An activity can subscribe only to data from the activities that are linked before it in the runbook. You can use published data to automatically populate the property values needed by activities.

### Use published data

1. Right-click the property value box, select **Subscribe**, and select **Published Data**.
2. Select the **Activity** dropdown box and select the activity from which you want to obtain the data. To view additional data elements common to all runbooks, select **Show Common Published Data**.
3. Select the published data element that you want to use, and select **OK**.

For a list of the data elements published by each activity, see the **Published Data** table in the activity section. For information about the common published data items, see [Common Published Data](/previous-versions/system-center/system-center-2012-R2/hh403821(v=sc.12)#CommonPublishedData).

## Activities

This integration pack adds the **Exchange Users** category to the **Activity** pane in the Runbook Designer. This category contains the following activities:

- Create and Send E-Mail
- Create Item
- Delete Item
- Find Appointment
- Forward Item
- Get Item
- Monitor Item
- Move or Copy Item
- Reply To E-Mail
- Send E-Mail
- Update Item
