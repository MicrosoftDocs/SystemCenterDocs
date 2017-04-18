---
title: Configuration Manager Integration Pack Activities
description: Configuration instructions for activities provided by the Configuration Manager integration pack.
ms.custom: na
ms.date: 03/08/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab4cf719-4cd3-4a38-92f6-c3019452e8ca
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---

# Configuration Manager Integration Pack Activities for System Center 2016 - Orchestrator

Applies To: System Center 2016 - Orchestrator

The following configuration instructions apply to all activities in this integration pack.

**Activity Properties**

Each activity has a set of required or optional properties that define
the configuration of that activity. This includes how it connects to
other activities or how the activity performs its actions. You can view
or modify activity properties when the activity is placed in the current
runbook.

**To configure the properties for an activity**

- Double-click the activity. Alternatively, you can right-click the activity, and then click **Properties**.
- To save your configuration entries, click **Finish**.

> [!Note]
> The filters for all activities are case sensitive. A value that does not match the case of your filter entry is not returned.

In the activity properties dialog box, several tabs along the left side
provide access to general and specific settings for the activity.
Although the number of available tabs for activity properties differs
from activity to activity, all activities will have a **General** tab, a
**Details** tab, and a **Run Behavior** tab. Some activities may have
additional tabs.

**General Tab**

This tab contains the **Name** and **Description** properties for the
activity. By default, the **Name** of the activity is the same as its
activity type, and the **Description** is blank. You can modify these
properties to create a more descriptive name or provide a detailed
description of the actions of the activity.

**Details Tab**

This tab contains properties that are specific to the activity. All
activities in this integration pack except for the Perform Client Action
activity have the **Connection Name** property at the top of the
**Details** tab. This property is used to specify the connection to the
Configuration Manager server.

**To configure the Connection Name property**

-   Click the ellipsis **(…)** button next to the **Name** field, and
    then select the applicable connection name. Connections displayed in
    the list have been previously configured as described in
    [Configuration Manager Integration Pack](configuration-manager-integration-pack.md).

**Value Type** properties are common across many of the activities.
These properties provide flexibility in the type of data you provide to
the activity, allowing you to specify ID values or names of objects to
be used. Each Value Type property is linked directly to another property
listed immediately above the Value Type property.

**To configure Value Type properties**

-   Click the ellipsis **(…)** button next to the **Value Type** field,
    and then select the setting that correctly identifies the type of
    value in the associated property.

**Schedule Tab**

The **Schedule** tab allows you to define availability, expiration and
mandatory assignments for deployments. Options available on the tab may
vary depending on the type of deployment. Mandatory assignment schedules
cause Configuration Manager to automatically run the program at a
specific time or according to a specific event, such as user
Logon/Logoff. The settings on this tab are optional.

**Mandatory Assignment Schedules**

To add a new mandatory assignment, click the **New** button. The
Mandatory Schedule dialog appears.

The Mandatory Schedule dialog box contains the following elements:

  
- Use the following schedule
  * Enables the **Schedule** group which allows you to define a specific schedule.
    * **None**: Specifies that the operation does not recur.
    * **Weekly**: Specifies that the operation recurs every N weeks. If this option is selected, you must specify the day of the week on which the operation will occur.
    * **Monthly**: Specifies that the operation recurs every N months. If this option is selected, you must specify the day of the month on which the operation will occur.
    * **Custom interval** (varies depending on the recurrence pattern selected): Specifies the frequency with which the operation will recur. You may set this in terms of minutes, hours, or days.
- Assign immediately after this event
  * Enables the selector for event-based assignment. Options are:
    * **As soon as possible**: Specifies that the program will automatically run as soon as it reaches the client and all program requirements are met. This value is specified by default.
    * **Logon**: Specifies that the program will automatically run the next time a user logs on to the client.
    * **Logoff**: Specifies that the program will automatically run the next time a user logs off the client.

**To add a mandatory assignment**

-   Click **Add**. The **Mandatory Schedule** dialog box opens.

-   To schedule the advertisement at a specified date and time select
    **Use the following schedule**.

    1.  To schedule the event, click the ellipsis **(…)** button to open
        the **Date Time Selection** dialog. Modify the date and time
        according to your needs, and then click **OK**.

    2.  If you want all clients to run the program at the same time
        regardless of time zone, select the **UTC** check box.

    3.  If you want the advertisement to run on a recurring schedule,
        select one of the options: **Weekly**, **Monthly** or **Custom
        Interval** and set the properties according to your needs.

-   To run the advertisement after an event, select **Assign immediately
    after this event**. Select the applicable option **As soon as
    possible**, **Logoff**, or **Logon**.

-   Click **OK** to save the schedule.

> [!Note]
> You can create multiple mandatory assignments.

**Run Behavior Tab**

This tab contains the properties that determine how the activity handles
multi-value published data and what notifications will be sent if the
activity fails or runs for an excessive period of time.

**Returned Data Behavior**

The “Get” activities retrieve information from another activity or
outside source, and can return one or more values in the published data.
For example, when you use the Get Collection Member activity, the data
output from that activity might be a list of computers that belong to
the specified collection.

By default, the data from the activity will be passed on as multiple
individual outputs. This triggers the next activity as many times as
there are items in the output. Alternatively, you can provide a single
output for the Get activity by enabling the **Flatten** option. When you
enable this option, you also choose a formatting option:

-   **Separate with line breaks**. Each item is on a new line. This
    format is useful for creating human-readable text files for the
    output.

-   **Separate with \_** . Each item is separated by one or more
    characters of your choice.

-   **Use CSV format**. All items are in CSV (comma-separated value)
    format. This format is useful for importing data into spreadsheets
    or other applications.

The activity will produce a new set of data every time it runs. The
**Flatten** feature does not flatten data across multiple executions of
the same activity.

**Event Notifications**

Some activities are expected to take a limited amount of time to
complete. If they do not complete within that time they may be stalled
or there may be another issue preventing them from completing. You can
define the number of seconds to wait for completion of the action. After
this period a platform event will be sent and the issue will be
reported. You can also choose whether to generate a platform event if
the activity returns a failure.

**To be notified when the activity takes longer than a specified time to
run or fails to run**

1.  In the **Event Notifications** box, enter the **number of seconds**
    of run time before a notification is generated.

2.  Select the **Report if activity fails to run** check box to generate
    run failure notifications.

**Published Data**

Published data is the foundation of a working runbook. It is the data
produced as a result of the actions of an activity. This data is
published to an internal data bus that is unique for each runbook.
Subsequent activities in the runbook can subscribe to this published
data and use it in their configuration. Link conditions also use this
information to add decision-making capabilities to runbooks.

An activity can only subscribe to published data from the activities
that are linked before it in the runbook. You can use published data to
automatically populate the property values needed by activities.

**To use published data**

1.  Right-click the property value box, click **Subscribe**, and then
    click **Published Data**.

2.  Click the **Activity** drop-down box and select the activity from which you want to obtain the data. To view additional data elements common to all policies, select **Show Common Published Data**.

3.  Click the published data element that you want to use, and then click **OK**.

## Activities

This integration pack adds the Microsoft Configuration Manager category to the Activity pane in the Runbook Designer. This category contains the following activities:

- [Add Collection Rule](add-collection-rule.md)
- [Create Collection](create-collection.md)
- [Delete Collection Rule](../orch/manage/delete-collection-rule.md)
- [Delete Collection](../orch/manage/delete-collection.md)
- [Deploy Application](../orch/manage/deploy-application.md)
- [Deploy Configuration Baseline](../orch/manage/deploy-configuration-baseline.md)
- [Deploy Program](../orch/manage/deploy-program.md)
- [Deploy Software Update](../orch/manage/deploy-software-update.md)
- [Deploy Task Sequence](../orch/manage/deploy-task-sequence.md)
- [Get Collection Member](../orch/manage/get-collection-member.md)
- [Get Deployment Status](../orch/manage/get-deployment-status.md)
- [Perform Client Action](../orch/manage/perform-client-action.md)
- [Query Configuration Manager](../orch/manage/query-configuration-manager.md)
- [Update Collection Membership](../orch/manage/update-collection-membership.md)