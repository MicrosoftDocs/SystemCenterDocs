---
title: FTP Integration Pack Activities
description: The following configuration instructions apply to all activities in this integration pack.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5d82cba-a523-41e8-b7f6-165662bc5d8a
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# FTP Integration Pack Activities

Applies To: System Center 2016 - Orchestrator

The following configuration instructions apply to all activities in this integration pack. Links to this section are included in the configuration instructions for each activity.

The procedures in this topic are performed on an activity that has been placed in the runbook window of the Orchestrator Runbook Designer.

## Activity Properties

Each activity has a set of required or optional properties that define the configuration of that activity. This includes how it connects to other activities or how the activity performs its actions. You can view or modify activity properties when the activity is placed in the runbook window.

#### To view and configure the properties for an activity

1.  Double-click the activity. Alternatively, you can right-click the activity, and then click **Properties**.

2.  To save your configuration entries, click **Finish**.

In the activity properties dialog box, several tabs along the left side provide access to general and specific settings for the activity. The number of available tabs for object properties differs between different activities.

### General Tab

This tab contains the **Name** and **Description** properties for the activity. By default, the **Name** of the activity is the same as its activity type, and the **Description** is blank. You can modify these properties to create more descriptive names or provide detailed descriptions of the actions of the activity.

### Properties Tab

This tab contains properties that are specific to the activity. All activities in this integration pack have the **Configuration Name** property at the top of the **Properties** or **Filters** tab. This property is used to specify the connection to the FTP server.

#### To configure the Configuration Name property

1.  Click the ellipsis **(...)** button next to the **Name** field.

2.  Select the applicable connection name.

### Filter Behavior

The activities List Folders/Files and Synchronize Folder/File use filters to determine the items that will be listed or synchronized. Property values of potential candidates are compared to the values of the filters to determine if they meet the criteria. When matching against values, you can select one of the available methods of comparison. An option is provided to either match or not match the filter using each method. For example, the "Does not" version of a method finds items that do not match the filter to start the activity. All text filters are case sensitive.

-   **Equals**: the property of the message matches the text or number specified in the filter.
-   **Does not equal**: the property of the message does not match the text or number specified in the filter.

### Run Behavior Tab

This tab contains the properties that determine how the activity handles multi-value published data and what notifications will be sent if the activity fails or runs for an excessive period of time.

### Multi-Value Published Data Behavior

The Get activities retrieve information from another activity or outside source, and can return one or more values in the published data. For example, when you use the List Folders/Files activity, the data output from that activity could be a list of computers that belong to the specified collection.

By default, the data from the List Folders/Files activity will be passed on as multiple individual outputs. This invokes the next activity as many times as there are items in the output. Alternatively, you can provide a single output for the activity by enabling the **Flatten** option. When you enable this option, you must choose a formatting option:

-   **Separate with line breaks**. Each item is on a new line. This format is useful for creating human-readable text files for the output.
-   **Separate with**. Each item is separated by one or more characters of your choice.
-   **Use CSV format**. All items are in CSV (comma-separated value) format. This format is useful for importing data into spreadsheets or other applications.

The activity will produce a new set of data every time it runs. The **Flatten** feature does not flatten data across multiple instances of the same activity.

## Event Notifications

Some activities are expected to take a limited amount of time to complete. If they do not complete within that time they may be stalled or there may be another issue preventing them from completing. You can define the number of seconds to wait for completion of the action. After this period a platform event will be sent and the issue will be reported. You can also choose whether to generate a platform event if the activity returns a failure.

#### To be notified when the activity takes longer than a specified time to run or fails to run

1.  In the **Event Notifications** box, enter the **number of seconds** of run time before a notification is generated.

2.  Select **Report if activity fails to run** to generate run failure notifications.

## Published Data

Published data is the foundation of a working runbook. It is the data produced as a result of the actions of an activity. This data is published to an internal data bus that is unique for each runbook. Subsequent activities in the runbook can subscribe to this data and use it in their configuration. Link conditions also use this information to add decision-making capabilities to runbooks.

An activity can subscribe only to data from the activities that are linked before it in the runbook. You can use published data to automatically populate the property values needed by activities.

#### To use published data

1.  Right-click the property value box, click **Subscribe**, and then click **Published Data**.

2.  Click the **Activity** drop-down box and select the activity from which you want to obtain the data. To view additional data elements common to all runbooks, select **Show Common Published Data**.

3.  Click the published data element that you want to use, and then click **OK**.

For a list of the data elements published by each activity, see the **Published Data** table in the activity topic. For information about the common published data items, see [Common Published Data](https://technet.microsoft.com/en-us/library/e339c027-4c69-43e5-a59b-ac7ea0a676c8#CommonPublishedData).

## Activities

This integration pack adds the **FTP** category to the **Activity** pane in the Runbook Designer. This category contains the following activities:

[Create Folder](../../orchestrator/create-folder.md)

[Delete File](delete-file.md)

[Delete Folder](delete-folder.md)

[Download File](download-file.md)

[List Folders/Files](list-folders-or-files.md)

[Rename File/Folder](rename-file-or-folder.md)

[Resume File Download](resume-file-download.md)

[Synchronize Folder/File](synchronize-folder-or-file.md)

[Upload File](upload-file.md)
