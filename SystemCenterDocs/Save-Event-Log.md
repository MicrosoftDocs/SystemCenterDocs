---
title: Save Event Log
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c3409b18-a952-48fd-8fbd-7d9d4ef44173
---
# Save Event Log
The Save Event Log activity is used to save entries from an event log so that they can be used later. The Save Event Log activity saves the event log entries to a delimited text file in a format that you specify. The activity allows you to choose which fields will be saved and allows you to filter against the fields to only allow particular event log entries to be saved. This activity uses a satellite license.

The Save Event Log activity can be used to create audit trails of problems that occur with a particular application or specific categories of event log entries. These saved files can later be used to track the performance of servers and applications in your network.

## Configuring the Save Event Log Activity
Before you configure the Save Event Log activity, you need to determine the following:

-   The event log that you are saving from

-   The computer where it is located

-   The fields that you want to include

-   The format of the file

> [!NOTE]
> If you require only specific entries to be saved and not the entire event log, you will need to know what fields to filter against as well as what values to filter.

Use the following information to configure the Save Event Log activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Computer**|Type the computer where the event log is located. Type **localhost** to specify the runbook server where the runbook is being processed. You can also use the ellipsis **\( ... \)** button to browse for the computer.|
|**Event log**|Type the name of the Windows Event Log where the entries that you are saving are located. You can also use the ellipsis **\( ... \)** button to browse for the event log name. Browsing is only available if you have specified a valid **Computer**.|
|**Include**|Select all the event Log fields that you want to save to the file. You have the option to select **Event ID**, **Source**, **Category**, **Description**, **Type**, **Computer**, and **Date\/time**.|

### Filters Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Event ID**|Select and type the specific event ID of the event log entry that you want to save.|
|**Source**|Select and type the value that the Source field of the event log entries will need to match.|
|**Category**|Select and type the value that the Category field of the event log entries will need to match.|
|**Description**|Select and type the value that the Description field of the event log entries will need to match.|
|**Type**|Select and specify the value that the Type field of the event log entries will need to match.|
|**Computer**|Select and specify the value that the Computer field of the event log entries will need to match.|
|**Date from**|Select and specify the ranges of dates that the events will need to be from to be included.|

### Output Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**File name**|Type the name of the file where the event log entries will be saved. This file will be saved on the computer where the event log resides.|
|**If the file exists**|Select the action that you want to take if a file with the same name already exists:<br /><br />-   **Create a file with a unique name**: Select to append a value to the filename to create a unique name that does not conflict with an existing name.<br />-   **Append**: Select to append the entries that are being saved to the file.<br />-   **Overwrite**: Select to overwrite the existing file with the file that is being created.<br />-   **Fail**: Select to cause the Save Event Log activity to fail if the filename already exists.|
|**File format**|Select the format that will be used to save the event log entries to the file:<br /><br />-   **CSV Delimited**: Select to use the CSV format to write each log entry.<br />-   **TAB Delimited**: Select to separate fields in each entry using the TAB character.<br />-   **Custom Delimited**: Select to separate fields in each entry using a custom character that you specify in the **Delimiter** box.|
|**Delimiter**|Type the delimiter that you want to use to separate the fields of each entry.|
|**Create column headings**|Select to save the column header information when saving a set of entries to a file. The header information contains meta data such as the field names.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Event log name|The name of the event log that was saved.|
|Computer|The computer where the event log that was saved resides.|
|Name and path of the file where entries are saved|The full path of the file where the event log was saved.|
|Number of Entries|The number of entries that were saved.|


