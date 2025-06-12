---
title: System Center VMM activities
description: This article describes all activities in the System Center integration pack for System Center - VMM.
ms.date: 11/01/2024
ms.service: system-center
ms.subservice: orchestrator
ms.topic: concept-article
author: jyothisuri
ms.author: jsuri
ms.custom: UpdateFrequency3, engagement-fy24
---
# System Center VMM Activities

The following configuration instructions apply to all the activities in the System Center Integration Pack for System Center - Virtual Machine Manager (VMM).

## Activity properties

Each activity has a set of required or optional properties that define the configuration of that activity. This includes how it connects to other activities or how the activity performs its actions. You can view or modify activity properties when the activity is placed in the runbook window.

To configure the properties for an activity:

1.  Double-click the activity. Alternatively, you can right-click the activity, and select **Properties**.

2.  To save your configuration entries, select **Finish**.

In the activity properties dialog, several tabs along the left side provide access to general and specific settings for the activity. The number of available tabs for object properties differs between different activities.

## General tab

This tab contains the **Name** and **Description** properties for the activity. By default, the **Name** of the activity is the same as its activity type, and the **Description** is blank. You can modify these properties to create more descriptive names or provide detailed descriptions of the actions of the activity.

## Properties tab

This tab contains properties that are specific to the activity. All the activities in this integration pack have the **Configuration Name** property at the top of the **Properties** or **Filters** tab. This property is used to specify the connection to the VMM server.

### Set the Configuration Name property

1.  Select the ellipsis button **(...)** next to the **Name** field.

2.  Select the applicable connection name. Connections displayed in the list have been previously configured as described in [Configuring the System Center 2016 Virtual Machine Manager Connections](/previous-versions/system-center/packs/hh830700(v=technet.10)#BKMK_ConfigureVMMConnections).

### Filter behavior

The Monitor and Get activities use filters to determine the values that will invoke a runbook or retrieve activities. Property values of potential candidates are compared to the values of the filters to determine if they meet the criteria. When matching against values, you select one of the available methods of comparison. An option is provided to either match or not match the filter using each method. For example, the "Does not" version of a method finds messages that do not match the filter to trigger the policy.

-   **Equals**: The property of the message exactly matches the text or the number specified in the filter.
-   **Does not equal**: The property of the message does not exactly match the text or the number specified in the filter.
-   **Is less than**: The property of the message is less than the number specified in the filter.
-   **Is less than or equal to**: The property of the message is less than or equal to the number specified in the filter.
-   **Is greater than**: The property of the message is greater than the number n the filter.
-   **Is greater than or equal to**: The property of the message is greater than or equal to the number specified in the filter.
-   **Contains**: The property of the message contains the exact text specified in the filter. Unlike the Equals behavior, there can be other text surrounding the matching text.
-   **Does not contain**: The property of the message does not contain the exact text specified in the filter. Unlike the Equals behavior, there can be other text surrounding the matching text.
-   **Matches pattern**: Use regular expressions to specify a pattern that the text must match.
-   **Does not match pattern**: Use regular expressions to specify a pattern that the text must not match.
-   **Starts with**: The property of the message starts with the exact text specified in the filter.
-   **Ends with**: the property of the message starts with the exact text specified in the filter.
-   **After**: The property of the message is after the date/time specified in the filter.
-   **Before**: The property of the message is before the date/time specified in the filter.

## Run Behavior tab

This tab contains the properties that determine how the activity handles multi-value published data and what notifications will be sent if the activity fails or runs for an excessive period of time.

### Multi-Value Published Data behavior

Get activities retrieve information from another activity or outside source, and can return one or more values in the published data. For example, when you use the Get VM activity, the data output from that activity might be a list of computers that belong to the specified collection.

By default, the data from the Get activity will be passed on as multiple individual outputs. This invokes the next activity as many times as there are items in the output. Alternatively, you can provide a single output for the activity by enabling the **Flatten** option. When you enable this option, you also choose a formatting option:

-   **Separate with line breaks**. Each item is on a new line. This format is useful for creating human-readable text files for the output.
-   **Separate with**. Each item is separated by one or more characters of your choice.
-   **Use CSV format**. All the items are in a CSV (comma-separated value) format. This format is useful for importing data into spreadsheets or other applications.

The activity will produce a new set of data every time it runs. The **Flatten** feature doesn't flatten data across multiple instances of the same activity.

## Event notifications

Some activities are expected to take a limited amount of time to complete. If they don't complete within that time, they may be stalled or there may be another issue preventing them from completing. You can define the number of seconds to wait for completion of the action. After this period, a platform event will be sent and the issue will be reported. You can also choose whether to generate a platform event if the activity returns a failure.

To be notified when the activity takes longer than a specified time to run or fails to run:

1.  In the **Event Notifications** box, enter the **number of seconds** of run time before a notification is generated.

2.  Select **Report if activity fails to run** to generate run failure notifications.

## Published data

Published data is the foundation of a working runbook. It is the data produced as a result of the actions of an activity. This data is published to an internal data bus that is unique for each runbook. Subsequent activities in the runbook can subscribe to this data and use it in their configuration. Link conditions also use this information to add decision-making capabilities to runbooks.

An activity can only subscribe to data from the activities that are linked before it in the runbook. You can use published data to automatically populate the property values needed by activities.

To use published data:

1.  Right-click the property value box, select **Subscribe**, and select **Published Data**.

2.  Select the **Activity** dropdown box, and select the activity from which you want to obtain the data. To view additional data elements common to all runbooks, select **Show Common Published Data**.

3.  Select the published data element that you want to use, and select **OK**.

For a list of the data elements published by each activity, see the **Published Data** tables in the activity topic. For information about the common published data items, see [Common Published Data](/previous-versions/system-center/system-center-2012-R2/hh403821(v=sc.12)#CommonPublishedData).

## Activities

The VMM integration pack adds the Virtual Machine Manager category to the **Activities** pane in the Runbook Designer. This category contains the following activities:

- [Create Checkpoint](create-checkpoint.md)
- [Create New Disk from VHD](create-new-disk-from-vhd.md)
- [Create Network Adapter](create-network-adapter.md)
- [Create New Disk](create-new-disk.md)
- [Create User Role](create-user-role.md)
- [Create VM from Template](create-vm-from-template.md)
- [Create VM from VHD](create-vm-from-vhd.md)
- [Create VM from VM](create-vm-from-vm.md)
- [Remove User Role](remove-user-role.md)
- [Get Checkpoint](get-checkpoint.md)
- [Get Disk](get-disk.md)
- [Get Network Adapter](get-network-adapter.md)
- [Get User Role](get-user-role.md)
- [Get VM](get-vm.md)
- [Manage Checkpoint](manage-checkpoint.md)
- [Move VM](move-vm.md)
- [Remove VM](remove-vm.md)
- [Repair VM](repair-vm.md)
- [Resume VM](resume-vm.md)
- [Run VMM PowerShell Script](run-vmm-powershell-script.md)
- [Shut Down VM](shut-down-vm.md)
- [Start VM](start-vm.md)
- [Stop VM](stop-vm.md)
- [Suspend VM](suspend-vm.md)
- [Update Disk](update-disk.md)
- [Update Network Adapter](update-network-adapter.md)
- [Update VM](update-vm.md)
- [Update User Role Property](update-user-role-property.md)
- [Update User Role Quota](update-user-role-quota.md)
