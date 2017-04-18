---
title: Windows Azure Activities
description: The following configuration instructions apply to all runbook activities that are available in the Windows Azure integration pack.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 69fc38af-c6bf-43bd-85c6-06875a321561
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Windows Azure Activities

Applies To: System Center 2016 - Orchestrator

The following configuration instructions apply to all runbook activities that are available in the Windows Azure integration pack.

## Activity properties

Each activity contains a set of required or optional properties. These define how the activity connects to other activities or how the activity performs its actions. When an activity has been placed in the runbook window, you can view or modify its properties.

#### To view and configure the properties for an activity

1.  Double-click the activity. Alternatively, you can right-click the activity, and then click **Properties**.

2.  View and configure activity properties as needed.

3.  To save your configuration entries, click **Finish**.

In the activity properties dialog box, various tabs provide access to general and specific settings for the activity. The number of available tabs for object properties will vary according to the activity.

## General tab

The **General** tab contains the **Name** and **Description** properties for the activity. By default, the **Name** of the activity is the same as its activity type and the **Description** is blank. You can modify these properties to provide a more specific name or to add a description as necessary.

## Properties tab

The **Properties** tab contains properties that are specific to the activity. All activities in this integration pack have the **Configuration Name** property on the **Properties** or **Filters** tab. The **Configuration Name** property is used to specify the connection to Windows Azure.

#### To configure the Configuration Name property

1.  Click the ellipsis **(...)** button next to the **Name** box.

2.  Select the applicable connection name. Connections displayed in the list have been previously configured as described in Windows Azure Integration Pack for System Center 2016 - Orchestrator.

### Criteria for filters

Some activities use filters to determine the values that will invoke a runbook or retrieve activities. Property values of potential candidates are compared to the values of the filters to determine if they meet the criteria. When you specify filter criteria, you can select one of the available methods of comparison. The system provides an option to either match or not match the filter using each method. For example, the "Does not" version of a method finds items that do not match the filter to trigger the runbook.

-   **Equals**: The property of the item exactly matches the text or number specified in the filter.
-   **Does not equal**: The property of the item does not exactly match the text or number specified in the filter.
-   **Is less than**: The numeric property of the item is less than the number specified in the filter.
-   **Is less than or equal to**: The numeric property of the item is less than or equal to the number specified in the filter.
-   **Is greater than**: The property of the item is greater than the number specified in the filter.
-   **Is greater than or equal to**: The numeric property of the item is greater than or equal to the number specified in the filter.
-   **Contains**: The property of the item contains the exact text specified in the filter. There can be other text surrounding the matching text.
-   **Does not contain**: The property of the item does not contain the exact text specified in the filter.
-   **Matches pattern**: This comparison method uses regular expressions to specify a pattern that the text must match.
-   **Does not match pattern**: This comparison method uses regular expressions to specify a pattern that the text must not match.
-   **Starts with**: The property of the item starts with the exact text specified in the filter.
-   **Ends with**: The property of the item ends with the exact text specified in the filter.
-   **After**: The property of the item is after the date and time specified in the filter.
-   **Before**: The property of the item is before the date and time specified in the filter.

## The Run Behavior tab

The **Run Behavior** tab contains the properties that determine how the activity handles multi-value published data and which notifications will be sent if the activity fails or runs for an excessive period of time.

### Multiple values in published data

A **Get** activity retrieves information from another activity or outside source and can then return one or more values in the **Get** activity's published data. For example, the data output from **Azure Hosted Services** activity could be a list of hosted services that belong to the specified collection.

By default, the data from a **Get** activity will be passed on as multiple individual outputs. These multiple outpus invoke the next activity as many times as there are items in the output. Alternatively, to request a single combined output, you can enable the **Flatten** option. When you enable the **Flatten** option, you must specify the output format:

-   **Separate with line breaks**. Each item is on a new line. This format is useful for creating human-readable text files.
-   **Separate with**. Each item is separated by one or more characters of your choice.
-   **Use CSV format**. All items are in CSV (comma-separated value) format. This format is useful for importing data into spreadsheets or other applications.

A **Get** activity will produce a new set of data every time it runs. The **Flatten** feature does not flatten data across multiple instances of the same activity.

## Time-out and failure event notifications

Some activities are expected to take only a limited amount of time to complete. If they do not complete within an expected tine frame, they may be stalled or there may be another issue preventing completion. You can define the number of seconds to wait for completion of the action. If the processing of the activity exceeds this time-out threshold, a platform event will be sent and the issue will be reported. You can also choose whether to generate a platform event if the activity returns a failure.

#### To be notified when the activity takes longer than a specified time to run or fails to run

1.  In the **Event Notifications** box, enter the **number of seconds** of run time before a notification is generated.

2.  Select **Report if activity fails to run** to generate run failure notifications.

## Published data
Published data is the data produced as a result of the actions of an activity. This data is published to an internal data bus that is unique for each runbook. Published data is the foundation of a working runbook. Subsequent activities in the runbook can subscribe to this data and use it in their configuration. Link conditions also use this information to add decision-making capabilities to runbooks.

An activity can only subscribe to data from the activities that occur before it in the runbook. You can use published data to automatically populate the property values needed by activities.

#### To use published data

1.  Right-click the property value box, click **Subscribe**, and then click **Published Data**.

2.  Click the **Activity** drop-down box and select the activity from which you want to obtain the data. To view additional data elements common to all runbooks, select **Show Common Published Data**.

3.  Click the published data element that you want to use, and then click **OK**.

For a list of the data elements published by each activity, see the **Published Data** tables in the activity topic. For information about the common published data items, see [Common Published Data](https://technet.microsoft.com/en-us/library/e339c027-4c69-43e5-a59b-ac7ea0a676c8#CommonPublishedData).

## Activities


This integration pack adds the **Windows Azure** category to the **Activity** pane in the Runbook Designer. This category contains the following activities:

[Add Management Certificate](add-management-certificate.md)

[Add OS Image](../orch/manage/add-os-image.md)

[Add Service Certificate](add-service-certificate.md)

[Add VM Data Disk](add-vm-data-disk.md)

[Add VM Disk](add-vm-disk.md)

[Add VM Endpoint](add-vm-endpoint.md)

[Add VM Instance](add-vm-instance.md)

[Capture VM Instance](capture-vm-instance.md)

[Change Deployment Configuration](change-deployment-configuration.md)

[Change Deployment OS](change-deployment-os.md)

[Check Cloud Service Name Availability](check-cloud-service-name-availability.md)

[Copy Blob](copy-blob.md)

[Create Affinity Group](create-affinity-group.md)

[Create Cloud Service](create-cloud-service.md)

[Create Container](create-container.md)

[Create Deployment](create-deployment.md)

[Create Storage Account](create-storage-account.md)

[Create VM Deployment](create-vm-deployment.md)

[Delete Blob](delete-blob.md)

[Delete Cloud Service](delete-cloud-service.md)

[Delete Container](delete-container.md)

[Delete Deployment](delete-deployment.md)

[Delete Management Certificate](delete-management-certificate.md)

[Delete OS Image](../orch/manage/delete-os-image.md)

[Delete Service Certificate](../orch/manage/delete-service-certificate.md)

[Delete Storage Account](../orch/manage/delete-storage-account.md)

[Delete VM Data Disk](../orch/manage/delete-vm-data-disk.md)

[Delete VM Disk](../orch/manage/delete-vm-disk.md)

[Delete VM Instance](../orch/manage/delete-vm-instance.md)

[Download Blob](../orch/manage/download-blob.md)

[Get Deployment](../orch/manage/get-deployment.md)

[Get Operating Systems](../orch/manage/get-operating-systems.md)

[Get Operation Status](../orch/manage/get-operation-status.md)

[Get Storage Account Keys](../orch/manage/get-storage-account-keys.md)

[Get Storage Account Properties](../orch/manage/get-storage-account-properties.md)

[Get VM Data Disk](../orch/manage/get-vm-data-disk.md)

[Get VM RDP File](../orch/manage/get-vm-rdp-file.md)

[Get VM instance](../orch/manage/get-vm-instance.md)

[List Blob](../orch/manage/list-blob.md)

[List Cloud Service](../orch/manage/list-cloud-service.md)

[List Container](../orch/manage/list-container.md)

[List Management Certificate](../orch/manage/list-management-certificate.md)

[List OS Images](../orch/manage/list-os-images.md)

[List Service Certificate](../orch/manage/list-service-certificate.md)

[List Storage Account](../orch/manage/list-storage-account.md)

[List VM Disks](../orch/manage/list-vm-disks.md)

[Put Blob](../orch/manage/put-blob.md)

[Reboot Role Instance](../orch/manage/reboot-role-instance.md)

[Regenerate Storage Account Key](../orch/manage/regenerate-storage-account-key.md)

[Reimage VM Instance](../orch/manage/reimage-vm-instance.md)

[Remove VM Endpoint](../orch/manage/remove-vm-endpoint.md)

[Restart VM Instance](../orch/manage/re../orch/manage/start-vm-instance.md)

[Rollback Update or Upgrade](../orch/manage/rollback-update-or-upgrade.md)

[Shutdown VM Instance](../orch/manage/shutdown-vm-instance.md)

[Snapshot Blob](../orch/manage/snapshot-blob.md)

[Start VM Instance](../orch/manage/start-vm-instance.md)

[Swap Deployment](../orch/manage/swap-deployment.md)

[Upgrade Deployment](../orch/manage/upgrade-deployment.md)

[Update Deployment Status](../orch/manage/update-deployment-status.md)

[Update OS Image](../orch/manage/update-os-image.md)

[Update Storage Account](../orch/manage/update-storage-account.md)

[Update VM Instance](../orch/manage/update-vm-instance.md)

[Walk Upgrade Domain](../orch/manage/walk-upgrade-domain.md)

## See Also


#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

