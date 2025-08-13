---
title: Configuration Manager Integration Pack Activities
description: This article contains configuration instructions for activities provided by the Configuration Manager integration pack.
ms.date: 04/21/2025
ms.update-cycle: 1095-days
ms.service: system-center
ms.subservice: orchestrator
<<<<<<< HEAD
ms.topic: article
=======
ms.topic: concept-article
>>>>>>> 514ff88bf71927f01716634de7955b7c0a0c063b
author: jyothisuri
ms.author: jsuri
ms.custom: UpdateFrequency3
---

# Configuration Manager integration pack activities

This article contains configuration instructions for activities provided by the Configuration Manager integration pack.

The following configuration instructions apply to all the activities in this integration pack:

## Activity properties

Each activity has a set of required or optional properties that define
the configuration of that activity. This includes how it connects to
other activities or how the activity performs its actions. You can view
or modify activity properties when the activity is placed in the current
runbook.

## Configure activity properties

To configure activity properties, follow these steps:

1. Double-click the activity. Alternatively, you can right-click the activity, and select **Properties**.
2. To save your configuration entries, select **Finish**.

> [!NOTE]
> The filters for all the activities are case sensitive. A value that doesn't match the case of your filter entry isn't returned.

In the activity properties dialog, several tabs along the left side
provide access to general and specific settings for the activity.
Although the number of available tabs for activity properties differs
from activity to activity, all activities will have a **General** tab, a
**Details** tab, and a **Run Behavior** tab. Some activities may have
additional tabs.

## General tab

This tab contains the **Name** and **Description** properties for the
activity. By default, the **Name** of the activity is the same as its
activity type, and the **Description** is blank. You can modify these
properties to create a more descriptive name or provide a detailed
description of the actions of the activity.

## Details tab

This tab contains properties that are specific to the activity. All
the activities in this integration pack except for the Perform Client Action
activity have the **Connection Name** property at the top of the
**Details** tab. This property is used to specify the connection to the
Configuration Manager server.

## Configure the Connection Name property

- Select ellipsis **(…)** next to the **Name** field, and then select the applicable connection name. Connections displayed in the list have been previously configured as described in [Configuration Manager Integration Pack](configuration-manager-integration-pack.md).

**Value Type** properties are common across many of the activities.
These properties provide flexibility in the type of data you provide to
the activity, allowing you to specify ID values or names of objects to
be used. Each Value Type property is linked directly to another property
listed immediately above the Value Type property.

## Configure Value Type properties

- Select ellipsis **(…)** next to the **Value Type** field,
    and then select the setting that correctly identifies the type of
    value in the associated property.

## Schedule tab

The **Schedule** tab allows you to define availability, expiration, and
mandatory assignments for deployments. Options available on the tab may
vary depending on the type of deployment. Mandatory assignment schedules
cause Configuration Manager to automatically run the program at a
specific time or according to a specific event, such as user
Logon/Logoff. The settings on this tab are optional.

## Mandatory assignment schedules

To add a new mandatory assignment, select **New**. The Mandatory Schedule dialog appears.

The Mandatory Schedule dialog contains the following elements:

- Use the following schedule
  * Enables the **Schedule** group, which allows you to define a specific schedule.
    * **None**: Specifies that the operation doesn't recur.
    * **Weekly**: Specifies that the operation recurs every N weeks. If this option is selected, you must specify the day of the week on which the operation will occur.
    * **Monthly**: Specifies that the operation recurs every N months. If this option is selected, you must specify the day of the month on which the operation will occur.
    * **Custom interval** (varies depending on the recurrence pattern selected): Specifies the frequency with which the operation will recur. You may set this in terms of minutes, hours, or days.
- Assign immediately after this event
  * Enables the selector for event-based assignment. Options are:
    * **As soon as possible**: Specifies that the program will automatically run as soon as it reaches the client and all program requirements are met. This value is specified by default.
    * **Logon**: Specifies that the program will automatically run the next time a user signs in to the client.
    * **Logoff**: Specifies that the program will automatically run the next time a user signs out of the client.

## Add a mandatory assignment

To add a mandatory assignment, follow these steps:

1. Select **Add**. The **Mandatory Schedule** dialog opens.
2. To schedule the advertisement at a specified date and time, select **Use the following schedule**.
3. To schedule the event, select ellipsis **(…)** to open the **Date Time Selection** dialog. Modify the date and time according to your needs, and select **OK**.
4. If you want all the clients to run the program at the same time regardless of time zone, select the **UTC** checkbox.
5. If you want the advertisement to run on a recurring schedule, select one of the options: **Weekly**, **Monthly**, or **Custom Interval** and set the properties according to your needs.
6. To run the advertisement after an event, select **Assign immediately after this event**. Select the applicable option **As soon as possible**, **Logoff**, or **Logon**.
7. Select **OK** to save the schedule.

> [!NOTE]
> You can create multiple mandatory assignments.

## Run Behavior tab

This tab contains the properties that determine how the activity handles
multi-value published data and what notifications will be sent if the
activity fails or runs for an excessive period of time.

## Returned data behavior

The “Get” activities retrieve information from another activity or
outside source and can return one or more values in the published data.
For example, when you use the Get Collection Member activity, the data
output from that activity might be a list of computers that belong to
the specified collection.

By default, the data from the activity will be passed on as multiple
individual outputs. This triggers the next activity as many times as
there are items in the output. Alternatively, you can provide a single
output for the Get activity by enabling the **Flatten** option. When you
enable this option, you also choose a formatting option:

- **Separate with line breaks**. Each item is on a new line. This
    format is useful for creating human-readable text files for the
    output.

- **Separate with \_**. Each item is separated by one or more
    characters of your choice.

- **Use CSV format**. All the items are in a CSV (comma-separated value)
    format. This format is useful for importing data into spreadsheets
    or other applications.

The activity will produce a new set of data every time it runs. The
**Flatten** feature doesn't flatten data across multiple executions of
the same activity.

## Event notifications

Some activities are expected to take a limited amount of time to
complete. If they don't complete within that time, they may be stalled
or there may be another issue preventing them from completing. You can
define the number of seconds to wait for the completion of the action. After
this period, a platform event will be sent and the issue will be
reported. You can also choose whether to generate a platform event if
the activity returns a failure.

To be notified when the activity takes longer than a specified time to
run or fails to run, follow these steps:

1. In the **Event Notifications** box, enter the **number of seconds**
    of run time before a notification is generated.

2. Select the **Report if activity fails to run** checkbox to generate
    run failure notifications.

## Published data

Published data is the foundation of a working runbook. It's the data
produced as a result of the actions of an activity. This data is
published to an internal data bus that is unique for each runbook.
Subsequent activities in the runbook can subscribe to this published
data and use it in their configuration. Link conditions also use this
information to add decision-making capabilities to runbooks.

An activity can only subscribe to published data from the activities
that are linked before it in the runbook. You can use published data to
automatically populate the property values needed by activities.

To use published data, follow these steps:

1. Right-click the property value box, select **Subscribe**, and select **Published Data**.

2. Select the **Activity** dropdown box and select the activity from which you want to obtain the data. To view additional data elements common to all the policies, select **Show Common Published Data**.

3. Select the published data element that you want to use, and select **OK**.

## Activities

This integration pack adds the Microsoft Configuration Manager category to the Activity pane in the Runbook Designer. This category contains the following activities:

- [Add Collection Rule](add-collection-rule.md)
- [Create Collection](create-collection.md)
- [Delete Collection Rule](delete-collection-rule.md)
- [Delete Collection](delete-collection.md)
- [Deploy Application](deploy-application.md)
- [Deploy Configuration Baseline](deploy-configuration-baseline.md)
- [Deploy Program](deploy-program.md)
- [Deploy Software Update](deploy-software-update.md)
- [Deploy Task Sequence](deploy-task-sequence.md)
- [Get Collection Member](get-collection-member.md)
- [Get Deployment Status](get-deployment-status.md)
- [Perform Client Action](perform-client-action.md)
- [Query Configuration Manager](query-configuration-manager.md)
- [Update Collection Membership](update-collection-membership.md)
