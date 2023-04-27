---
title: IBM Tivoli Netcool OMNIbus Activities
description: This integration pack adds the IBM Tivoli Netcool/OMNIbus category to the Activity pane in the Runbook Designer.
ms.custom: UpdateFrequency3
ms.date: 04/27/2023
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9438aacb-3900-4aaf-8cd4-4b73f771c15a
author: jyothisuri
ms.author: jsuri
manager: mkluck
robots: noindex
monikerRange: '<=sc-orch-2019'
---
# IBM Tivoli Netcool OMNIbus Activities

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

This integration pack adds the IBM Tivoli Netcool/OMNIbus category to the **Activity** pane in the Runbook Designer. This category contains the following activities:

- [Create Alert Activity](create-alert-activity.md)

- [Delete Alert Activity](delete-alert-activity.md)

- [Get Alerts Activity](get-alerts-activity.md)

- [Monitor Alerts Activity](monitor-alerts-activity.md)

[Update Alert Activity](update-alert-activity.md)

## Common Configuration Instructions for All Activities

The following configuration instructions apply to all the activities in this integration pack. The links to this section are included in the configuration instructions for each activity.

### Activity Properties

Each activity can have a set of properties that define the configuration of that activity. These properties can includes how the activity connects to other activities or how the activity performs its actions. You can view or modify an activity's properties when the activity is in the runbook window.

#### To configure the properties for an activity

1.  Double-click the activity name.

    Optionally, you can right-click the activity name, and select **Properties**.

2.  Select **Finish** to save your configuration entries.

### Property Tabs

In the activity properties dialog, tabs along the left side provide access to settings for the activity. The number of available tabs for activity properties can differ from one activity to another; all activities have a **General**, a **Details**, and a **Run Behavior** tab. Some activities have additional tabs.

#### General Tab

This tab contains the **Name** and **Description** properties for the activity. By default, the **Name** of the activity is the same as its activity type, and the **Description** is blank. You can modify these properties to create descriptive names or provide detailed descriptions of the activity.

#### Details Tab

This tab contains the properties that are specific to the activity.

##### Connection Name Property

All activities in this integration pack have a **Connection Name** property at the top of the **Details** tab. This property specifies the connection to the IBM Tivoli Netcool/OMNIbus server.

#### To configure the Connection Name property

-   Select the ellipsis **(...)** button next to the **Name** field, and then select the applicable connection name.

##### Filter Behavior Property

The Monitor and Get activities use filters to determine the values that invoke a runbook or retrieve activity. Property values of potential matches are compared to the filter values to determine if they meet the criteria. When configuring filter values, select one of the available methods of comparison. There is an option to either match or not match the filter for each method.

-   **Equals**: The property of the alert exactly matches the text or the number specified in the filter.
-   **Does not equal**: The property of the alert doesn't match the text or the number specified in the filter.
-   **Is less than or equal to**: The property of the alert is less than or equal to the value specified in the filter.
-   **Is less than**: The property of the alert is less than the value specified in the filter.
-   **Is greater than or equal to**: The property of the alert is greater than or equal to the value specified in the filter.
-   **Is greater than**: The property of the alert is greater than the value specified in the filter.
-   **Matches pattern**: This condition uses the Netcool Regular Expressions Library syntax described in the Netcool User Guide.
-   **Does not match pattern**: This condition uses the Netcool Regular Expressions Library syntax described in the Netcool User Guide.

#### Run Behavior Tab

This tab contains the properties that determine how the activity handles multi-value published data and what notifications to send if the activity fails or runs longer than the timeout period.

##### Multi-Value Published Data Behavior

Get activities retrieve information from another activity or an outside source. They can return one or more values in available from published data. For example, the Get Collection Member activity, the data might be a list of computers that belong to a specified collection.<br>By default, the data from the Get activity published as multiple individual outputs. This can trigger another activity in a workflow, as many times as there are items published. You can also provide a single output for the activity by enabling the **Flatten** option. When you enable the **Flatten** option, you must choose a formatting option:

-   **Separate with line breaks**. Each output is on a new line. This format is useful for creating human-readable text files as output.
-   **Separate with \_**. One or more characters of your choice separate each output.
-   **Use CSV format**. All output is in the CSV (comma-separated value) format. This format is useful for importing data into spreadsheets.

Activities produce a new set of data every time they run. The **Flatten** feature doesn't flatten data across multiple instances of the same activity.

##### Event Notification

Some activities take a limited amount of time to complete. If the activity doesn't complete within a specified time, it can appear to stop responding. You can configure the number of seconds to wait for the completion of an activity. After this wait period, a platform event is sent and the issue is reported. Additionally, you can choose whether to generate a platform event if the activity returns a failure.

#### To send a notification when an activity fails

1.  In the **Event Notifications** box, enter the **number of seconds** of time before generating a notification.

2.  Select **Report if activity fails to run** to generate a failure notification.

For more information about events, see the [Activity Events](/previous-versions/system-center/system-center-2012-R2/hh489611(v=sc.12)) article in [Administering System Center - Orchestrator](/previous-versions/system-center/system-center-2012-R2/hh674377(v=sc.12)).

##### Published Data

Published data is the method that one activity shares information with other activities in a runbook. It's the data produced by the actions of an activity. This data is published to an internal data bus unique for each runbook. Activities in a workflow can subscribe to the published data of another activity and use it in their configuration. Link conditions also use published data to add decision-making capabilities to a runbook.<br>An activity can only subscribe to published data from activities that run before it in the runbook. You can use published data to populate the property values needed by an activity.

#### To use published data

1.  Right-click the **Property Value** box, select **Subscribe**, and select **Published Data**.

2.  Select the **Activity** dropdown list box and select the activity from which you want to obtain the data.

3.  To view data elements common to all the policies, select **Show Common Published Data**.

4.  Select the published data element that you want to use, and select **OK**.

For a list of data elements published by each activity, see the Published Data tables in the activity section. For information about the Common Published Data items, see the [Common Published Data](/previous-versions/system-center/system-center-2012-R2/hh403821(v=sc.12)#CommonPublishedData) article in [Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md).