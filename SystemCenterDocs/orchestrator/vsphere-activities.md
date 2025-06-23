---
title: VMware vSphere Activities
description: This integration pack adds the VMware vSphere category to the Activities pane in the Runbook Designer.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39775552-06b7-4a54-aece-6b62ce7ee766
author: jyothisuri
ms.author: jsuri
robots: noindex
ms.date: 11/01/2024
---
# VMware vSphere Activities

This integration pack adds the VMware vSphere category to the **Activities** pane in the Runbook Designer. This category contains the following activities:

- [Add Network Adapter Activity](add-network-adapter-activity.md)
- [Add VM Disk Activity](add-vm-disk-activity.md)
- [Clone Linux VM Activity](clone-linux-vm-activity.md)
- [Clone Windows VM Activity](clone-windows-vm-activity.md)
- [Create VM Activity](create-vm-activity.md)
- [Customize VM Activity](customize-vm-activity.md)
- [Delete Network Adapter Activity in System Center ](delete-network-adapter-activity-in-system-center-2016.md)
- [Delete VM Activity](delete-vm-activity.md)
- [Delete VM Disk Activity in System Center ](delete-vm-disk-activity-in-system-center-2016.md)
- [Get Cluster Properties Activity](get-cluster-properties-activity.md)
- [Get Datastore Capacity Activity](get-datastore-capacity-activity.md)
- [Get Host Datastores Activity](get-host-datastores-activity.md)
- [Get Host Properties Activity](get-host-properties-activity.md)
- [Get Hosts Activity](get-hosts-activity.md)
- [Get Resource Pool Properties Activity](get-resource-pool-properties-activity.md)
- [Get Resource Pools Activity](get-resource-pools-activity.md)
- [Get VM List Activity](get-vm-list-activity.md)
- [Get VM Properties Activity](get-vm-properties-activity.md)
- [Get VM Status Activity](get-vm-status-activity.md)
- [Maintenance Mode Activity](maintenance-mode-activity.md)
- [Migrate VM Activity](migrate-vm-activity.md)
- [Modify VM Disk Activity in System Center ](modify-vm-disk-activity-in-system-center-2016.md)
- [Move VM Activity](move-vm-activity.md)
- [Reconfigure VM Activity](reconfigure-vm-activity.md)
- [Reset VM Activity](reset-vm-activity.md)
- [Revert VM Snapshot Activity](revert-vm-snapshot-activity.md)
- [Set VM CD/DVD to ISO Image Activity](set-vm-cd-or-dvd-to-iso-image-activity.md)
- [Set VM Networks Activity](set-vm-networks-activity.md)
- [Start VM Activity](start-vm-activity.md)
- [Stop VM Activity](stop-vm-activity.md)
- [Suspend VM Activity](suspend-vm-activity.md)
- [Take VM Snapshot Activity](take-vm-snapshot-activity.md)

## Common Configuration Instructions for All Activities

The following configuration instructions apply to all the activities in this integration pack. Links to this section are included in the configuration instructions for each activity.

### Activity Properties

Each activity has a set of required or optional properties that define the configuration of that activity. This includes how it connects to other activities or how the activity performs its actions. You can view or modify activity properties when the activity is placed in the runbook window.

#### Configure the properties for an activity

1.  Double-click the activity. Alternatively, you can right-click the activity, and select **Properties**.

2.  To save your configuration entries, select **Finish**.

In the activity properties dialog, several tabs along the left side provide access to general and specific settings for the activity. Although the number of available tabs for activity properties differs from activity to activity, all the activities will have a **General** tab, a **Properties** tab, and a **Run Behavior** tab. Some activities may have additional tabs.

### General Tab

This tab contains the **Name** and **Description** properties for the activity. By default, the **Name** of the activity is the same as its activity type, and the **Description** is blank. You can modify these properties to create more descriptive names or provide detailed descriptions of the actions of the activity.

### Properties Tab

This tab contains properties that are specific to the activity.

All the activities in this integration pack have the **Configuration** property at the top of the **Properties** tab. This property is used to specify the connection to the VMware vSphere vCenter server.

#### Configure the Configuration property

-   Select the ellipsis **(...)** button next to the **Name** field, and then select the applicable connection name.

#### Filter Behavior

The Monitor and Get activities use filters to determine the values that will invoke a runbook or retrieve activities. Property values of potential candidates are compared to the values of the filters to determine if they meet the criteria. When matching against values, you select one of the available methods of comparison. An option is provided to either match or not match the filter using each method. For example, the "Does not" version of a method causes alerts that don't match the filter to invoke the runbook.

-   **Equals**: The property of the alert exactly matches the text or the number specified in the filter.
-   **Does not equal**: The property of the alert does not exactly match the text or the number specified in the filter.
-   **Contains**: The property of the alert contains the exact text specified in the filter. Unlike the Equals behavior, there can be other text surrounding the matching text.
-   **Does not contain**: The property of the alert doesn't contain the exact text specified in the filter. Unlike the Equals behavior, there can be other text surrounding the matching text.
-   **Matches pattern**: Use wildcards to specify a pattern that the text must match. The two wildcard values are the asterisk (\*) and the question mark (?). The behavior of the wildcards is similar to the Command Prompt. The asterisk will match any number of characters, while the question mark will only match one character. For example, if you've a filter specified as "a\*b", the pattern would match any text that has an "a" at the beginning and a "b" at the end. So, it will match "aab", "abbbbbb", and "abbcb", but it won't match "ba" or "abba". Using the question mark, if you've a filter specified as "a?b", the pattern will match any text that has an "a" at the beginning, any single character in the middle, and "b" at the end. So, this filter will match "a b", "abb", and "aqb", but it won't match "abbb" or "ab".
-   **Does not match pattern**: Use wildcards to specify a pattern that the text must not match.
-   **Starts with**: The property of the alert starts with the exact text specified in the filter.
-   **Ends with**: The property of the alert starts with the exact text specified in the filter.

### Run Behavior Tab

This tab contains the properties that determine how the activity handles multi-value published data and what notifications will be sent if the activity fails or runs for an excessive period of time.

#### Multi-Value Published Data Behavior

The Get activities retrieve information from another activity or outside source and can return one or more values in the published data. For example, when you use the Get Hosts activity, the data output from that activity will be a list of hosts managed by the vSphere server.

By default, the data from the Get activity will be passed on as multiple individual outputs. This triggers the next activity as many times as there are items in the output. Alternatively, you can provide a single output for the activity by enabling the **Flatten** option. When you enable this option, you also choose a formatting option:

-   **Separate with line breaks**. Each item is on a new line. This format is useful for creating human-readable text files for the output.
-   **Separate with \_**. Each item is separated by one or more characters of your choice.
-   **Use CSV format**. All the items are in a CSV (comma-separated value) format. This format is useful for importing data into spreadsheets or other applications.

The activity will produce a new set of data every time it runs. The **Flatten** feature doesn't flatten data across multiple instances of the same activity.

#### Event Notifications

Some activities are expected to take a limited amount of time to complete. If they don't complete within that time, they may be stalled or there may be another issue preventing them from completing. You can define the number of seconds to wait for completion of the action. After this period, a platform event will be sent and the issue will be reported. You can also choose whether to generate a platform event if the activity returns a failure.

#### To be notified when the activity takes longer than a specified time to run or fails to run

1.  In the **Event Notifications** box, enter the **number of seconds** of run time before a notification is generated.

2.  Select **Report if activity fails to run** to generate run failure notifications.

>[!NOTE]
>For more information, see [Activity Events](/previous-versions/system-center/system-center-2012-R2/hh489611(v=sc.12)).

### Published Data

Published data is the foundation of a working runbook. It's the data produced as a result of the actions of an activity. This data is published to an internal data bus that's unique for each runbook. Subsequent activities in the workflow can subscribe to this data and use it in their configuration. Link conditions also use this information to add decision-making capabilities to policies.

An activity can only subscribe to published data from the activities that are linked before it in the runbook. You can use published data to automatically populate the property values needed by activities.

#### Use published data

1.  Right-click the property value box, select **Subscribe**, and select **Published Data**.

2.  Select the **Activity** dropdown box and select the activity from which you want to obtain the data.

    To view additional data elements common to all policies, select **Show Common Published Data**.

3.  Select the data element that you want to use, and select **OK**.

For a list of data elements published by each activity, see the Published Data tables in the activity topic. For information about the Common Published Data items, see [Common Published Data](/previous-versions/system-center/system-center-2012-R2/hh403821(v=sc.12)#CommonPublishedData).
