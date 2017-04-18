---
title: Exchange Administrator Activities
description: The following configuration instructions apply to all activities that are performed in the Exchange Admin Integration Pack.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a15cd3e-3838-4e20-a092-07b2470d5717
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Exchange Administrator Activities

Applies To: System Center 2016 - Orchestrator

The following configuration instructions apply to all activities that are performed in the Exchange Admin Integration Pack. The detailed configuration topics for specific Exchange Admin activities all contain links back to these general instructions.

Each procedure in this topic is performed on an activity that has been placed in the runbook window of the **Orchestrator Runbook Designer**.

## Activity properties

Each activity is configured with a set of required or optional properties. These define how the activity connects to other activities or how the activity performs its actions. When an activity has been placed in the runbook window, you can view or modify its properties.

#### To view and configure the properties for an activity

1.  Double-click the activity. Alternatively, you can right-click the activity, and then click **Properties**.

2.  View and configure the activity properties as needed.

3.  To save your configuration entries, click **Finish**.

In the activity properties dialog box, various tabs provide access to general and specific settings for the activity. The number of available tabs for object properties will vary according to the activity.

### General tab

The **General** tab contains the **Name** and **Description** properties for the activity. By default, the **Name** of the activity is the same as its activity type and the **Description** is blank. You can modify these properties to provide a more specific name or to add a description as necessary.

### Properties tab

The **Properties** tab contains properties that are specific to the activity. All activities in this integration pack have the **Configuration Name** property on the **Properties** tab. The **Configuration Name** property is used to specify the connection to the Exchange server.

#### To configure the Configuration Name property

1.  Click the ellipsis **(...)** button next to the **Name** field.

2.  Select the applicable connection name. Connections displayed in the list have been previously configured as described in <span>Exchange Admin Integration Pack for System Center 2016 - Orchestrator</span>.

### Criteria for filters

The **Get** activities use filters to determine the values that will invoke a runbook or retrieve activities. Property values of potential candidates are compared to the values of the filters to determine if they meet the criteria. When you specify filter criteria, you can select one of the available methods of comparison. The system provides an option to either match or not match the filter using each method. For example, the "Does not" version of a method finds items that do not match the filter. All text filters are case sensitive.

-   **Equals**: The property of the item matches the text or number specified in the filter.
-   **Does not equal**: The property of the item does not match the text or number specified in the filter.
-   **Is less than**: The numeric property of the item is less than the number specified in the filter.
-   **Is less than or equal to**: The numeric property of the item is less than or equal to the number specified in the filter.
-   **Is greater than**: The numeric property of the item is greater than the number specified in the filter.
-   **Is greater than or equal to**: The numeric property of the item is greater than or equal to the number specified in the filter.
-   **Contains**: The property of the item contains the exact text specified in the filter. There can be other text surrounding the matching text.
-   **Does not contain**: The property of the item does not contain the exact text specified in the filter.
-   **Matches pattern**: This comparison method uses regular expressions to specify a pattern that the text must match.
-   **Does not match pattern**: This comparison method uses regular expressions to specify a pattern that the text must not match.
-   **Starts with**: The property of the item starts with the exact text specified in the filter.
-   **Ends with**: The property of the item ends with the exact text specified in the filter.

### The Run Behavior tab

The **Run Behavior** tab contains the properties that determine how the activity handles multi-value published data and which notifications will be sent if the activity fails or runs for an excessive period of time.

### Multiple values in published data

The **Get** activities retrieve information from another activity or outside source and can then return one or more values in the published data. For example, the data output from the **Get Mailbox** activity could be the details of an existing mailbox.

By default, the data from the **Get** activity will be passed on as multiple individual outputs. These multiple outputs will invoke the next prescribed activity as many times as there are items in the output. Alternatively, to request a single combined output for the activity, you can enable the **Flatten** option. When you enable the **Flatten** option, you must specify the output format:

-   **Separate with line breaks**. Each item is on a new line. This format is useful for creating human-readable text files.
-   **Separate with**. Each item is separated by one or more characters of your choice.
-   **Use CSV format**. All items are in CSV (comma-separated value) format. This format is useful for importing data into spreadsheets or other applications.

The **Get** activity will produce a new set of data every time it runs. The **Flatten** feature does not flatten data across multiple instances of the same activity.

## Timeout and failure event notifications

Some activities are expected to take only a limited amount of time to complete. If they do not complete within an expected timeframe, they may be stalled or there may be another issue preventing completion. You can define the number of seconds to wait for completion of the action. If the processing of the activity exceeds this timeout threshold, a platform event will be sent and the issue will be reported. You can also choose whether to generate a platform event if the activity returns a failure.

#### To be notified when the activity takes longer than a specified time to run or fails to run

1.  In the **Event Notifications** box, enter the **number of seconds** of run time before a notification is generated.

2.  Select **Report if activity fails to run** to generate run failure notifications.

## Published data

Published data is the data produced as a result of the actions of an activity. This data is published to an internal data bus that is unique for each runbook. Published data is the foundation of a working runbook. Subsequent activities in the runbook can subscribe to this data and use it in their configuration. Link conditions also use this information to add decision-making capabilities to runbooks.

An activity can subscribe only to data from the activities that are linked before it in the runbook. You can use published data to automatically populate the property values needed by activities.

#### To use published data

1.  Right-click the property value box, click **Subscribe**, and then click **Published Data**.

2.  Click the **Activity** drop-down box and select the activity from which you want to obtain the data. To view additional data elements common to all runbooks, select **Show Common Published Data**.

3.  Click the published data element that you want to use, and then click **OK**.

For a list of the data elements published by each activity, see the **Published Data** table in the specific activity topic. For information about the common published data items, see <span>Common Published Data</span>.

## Activities
--

This integration pack adds the **Exchange Admin** category to the **Activity** pane in the Runbook Designer. This category contains the following activities:

[Create Mailbox](create-mailbox.md)

[Create Move Request](create-move-request.md)

[Create Remote Mailbox (Hybrid)](create-remote-mailbox-hybrid.md)

[Disable Mailbox](disable-mailbox.md)

[Disable Remote Mailbox (Hybrid)](disable-remote-mailbox-hybrid.md)

[Enable Mailbox](enable-mailbox.md)

[Enable Remote Mailbox (Hybrid)](enable-remote-mailbox-hybrid.md)

[Get Mailbox](get-mailbox.md)

[Get Move Request](get-move-request.md)

[Get Move Request Statistics](get-move-request-statistics.md)

[Get Remote Mailbox (Hybrid)](get-remote-mailbox-hybrid.md)

[Remove Mailbox](remove-mailbox.md)

[Remove Remote Mailbox (Hybrid)](remove-remote-mailbox-hybrid.md)

[Run Exchange PowerShell Command](run-exchange-powershell-command.md)

[Update Mailbox](../orch/manage/update-mailbox.md)

[Update Move Request](../orch/manage/update-move-request.md)

[Update Remote Mailbox (Hybrid)](../orch/manage/update-remote-mailbox-hybrid.md)
