---
title: SharePoint Activities
description: The following configuration instructions apply to all activities in this integration pack.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 998dfa81-2129-4879-b4cf-743b4e3ca609
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
SharePoint Activities
=====================

Applies To: System Center 2016 - Orchestrator

The following configuration instructions apply to all activities in this integration pack. Links to this section are included in the configuration instructions for each activity.

The procedures in this topic are performed on an activity that has been placed in the Runbook Designer workspace.

Activity Properties
-------------------

Each activity has a set of required or optional properties that define the configuration of that activity. The configuration includes how the activity connects to other activities or how the activity performs its actions. You can view or modify activity properties when the activity is placed in the Runbook Designer workspace.

#### To view and configure the properties for an activity

1.  Double-click the activity. Alternatively, you can right-click the activity, and then click **Properties**.

2.  View or configure activity properties as needed.

3.  To save your configuration entries, click **Finish**.

In the activity's **Properties** dialog box, various tabs provide access to general and specific settings for the activity. The number of available tabs for activity properties varies according to the activity.

### General tab

This tab contains the **Name** and **Description** properties for the activity. By default, the **Name** of the activity is the same as its activity type, and the **Description** is blank. You can modify these properties to create a more descriptive name or to provide detailed descriptions of the actions of the activity.

### Properties tab

This tab contains properties that are specific to the activity. All activities in this integration pack have the **Configuration Name** property at the top of the **Properties** or **Filters** tab. This property is used to specify the connection to Microsoft Exchange Server.

#### To configure the Configuration Name property

1.  Click the ellipsis **(...)** button next to the **Name** box.

2.  Select the applicable connection name. Connections that are displayed in the list have been previously configured as described in [System Center Integration Pack for Microsoft SharePoint](system-center-integration-pack-for-microsoft-sharepoint.md).

### Filter Behavior

The Get activities use filters to determine the values that invoke a runbook or retrieve activities. Property values of potential candidates are compared to the values of the filters to determine if they meet the criteria. When you match property values against filter values, you can select one of the available methods of comparison. An option is provided to either match or not match the filter by using each method. For example, the "Does not equal" version of a method finds messages that do not match the filter to start the activity. All text filters are case sensitive.

-   **Equals**: the list item matches the text or number that is specified in the filter.
-   **Does not equal**: the list item does not match the text or number that is specified in the filter.
-   **Is less than**: the list item is less than the number that is specified in the filter.
-   **Is less than or equal to**: the list item is less than or equal to the number that is specified in the filter.
-   **Is greater than**: the list item is greater than the number in the filter.
-   **Is greater than or equal to**: the list item is greater than or equal to the number that is specified in the filter.
-   **Contains**: the list item contains the exact text that is specified in the filter. Unlike the Equals behavior, other text can surround the matching text.
-   **Starts with**: the list item starts with the exact text that is specified in the filter. Unlike the Equals behavior, other text can follow the matching text.

### The Run Behavior tab

This tab contains the properties that determine how the activity handles multi-valued Published Data and what notifications are sent if the activity fails or runs for an excessive period of time.

### Multiple values in Published Data

The Get activities retrieve information from Microsoft SharePoint and can publish data for multiple items. For example, when you use the Get List Items activity, the data output publishes the Title for each list item that was retrieved.

By default, the data from the Get activity is passed on as multiple individual outputs. This process invokes the next activity as many times as there are items in the output. Alternatively, to provide a single output for the activity, by enabling click **Flatten**. When you click this option, you must select one of the following formatting options:

-   **Separate with line breaks**. Each item is on a new line. This format is used to create human-readable text files for the output.
-   **Separate with**. Each item is separated by one or more characters of your choice.
-   **Use CSV format**. All items are in comma-separated value (CSV) format. This format is used to import data into spreadsheets or other applications.

The activity produces a new set of data every time it runs. The **Flatten** feature does not flatten data across multiple instances of the same activity.

Time-out and failure event notifications
----------------------------------------

Some activities are expected to finish in a limited amount of time. If they do not finish within that time, they might be stalled, or another issue might prevent them from finishing. You can define the number of seconds to wait to complete the action. After this period, a platform event is sent, and the issue is reported. You can also choose whether to generate a platform event if the activity returns a failure.

#### To be notified when the activity takes longer than a specified time to run or when it fails to run

1.  In the **Event Notifications** box, enter the **number of seconds** of run time before a notification is generated.

2.  Select **Report if activity fails to run** to generate run failure notifications.

Published Data
--------------

Published Data is the data that is produced as a result of the actions of an activity. This data is published to an internal data bus that is unique for each runbook. Published Data is the foundation of a working runbook. Subsequent activities in the runbook can subscribe to this data and use it in their configuration. Link conditions also use this information to add decision-making capabilities to runbooks.

An activity can subscribe only to data from the activities that are linked before it in the runbook. You can use Published Data to automatically populate the property values that are required by activities.

#### To use Published Data

1.  Right-click the property value box, click **Subscribe**, and then click **Published Data**.

2.  Click the **Activity** list and select the activity from which you want to obtain the data. To view additional data elements that are common to all runbooks, select **Show Common Published Data**.

3.  Click the Published Data element that you want to use, and then click **OK**.

For a list of the data elements that are published by each activity, see the **Published Data** table in the topic that describes that activity. For information about the common Published Data items, see [Common Published Data](https://technet.microsoft.com/en-us/library/e339c027-4c69-43e5-a59b-ac7ea0a676c8)<https://technet.microsoft.com/en-us/library/e339c027-4c69-43e5-a59b-ac7ea0a676c8#CommonPublishedData>.

Activities
----------

This integration pack adds the **Microsoft SharePoint** category to the **Activities** pane in the Runbook Designer. This category contains the following activities:

[Create List Item](create-list-item.md)

[Delete Attachment](delete-attachment.md)

[Delete Document](delete-document.md)

[Delete List Item](delete-list-item.md)

[Download Attachment](download-attachment.md)

[Download Document](download-document.md)

[Get Attachments](get-attachments.md)

[Get Documents](get-documents.md)

[Get List Items](get-list-items.md)

[Get View Items](get-view-items.md)

[Monitor List Items](monitor-list-items.md)

[Query List](query-list.md)

[Update List Item](update-list-item.md)

[Upload Attachment](upload-attachment.md)

[Upload Document](upload-document.md)
