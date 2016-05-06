---
title: Published Data
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e339c027-4c69-43e5-a59b-ac7ea0a676c8
---
# Published Data
Published Data lets an activity use information from another activity in the same runbook. Each activity has a specific set of Published Data items that it populates after it runs. Any other activity that runs after it in the workflow has access to this data. In addition to data specific to each activity, all activities publish a common set of data items that provide information such as the start and stop time of the activity and its completion status. Link conditions also use Published Data to add filtering and decision\-making capabilities to runbooks.

For example, the runbook might use a **Read Line** activity to get information from a text file. A **Send Email** activity later in the runbook has to use the information to include in the text of its mail. The **Send Email** activity could use the **Line Text** Published Data item from the **Read Line** activity to include in its mail message.

## Data Types
The following table describes the categories of Published Data value types.

|Published Data value type|Description|
|-----------------------------|---------------|
|String value|Text, for example, an error message description.|
|Date value|Date and time information. For example, the date and time that a specific error occurred.|
|Number value|Numeric information. For example, the number of rows returned by a database query.|
|Boolean value|true or false. For example, command completed.|

### Date and time characteristics
Activity Start Time and Activity End Time data is saved to the databus in two fields. These formats are local time and Coordinated Universal Time \(UTC\), both in ISO 8601 format. By using UTC, runbooks can run in either a non\-locale\-specific or a non\-time\-zone\-specific context. Only Published Data that is saved to the databus provide date and time information in UTC with ISO 8601 formatting.

The date and time values displayed in the Runbook Designer and the Orchestration console, including, but not limited to the Log History, Audit History, and Events respect the locale date and time format configured for your computer.

## Published Data with multi\-value types
When an activity in a runbook runs, it runs one time for each item of data that the previous activity produced. For example, the **Query Database** activity runs and retrieves three rows from the database. These three rows of data cause the next activity to run three times, one time for each row returned. This next activity does not have to subscribe to the data for this action to occur.

An activity can also retrieve information from an outside source. The **Get** activities and **Monitor** activities demonstrate this behavior. Data output from an activity might be a list of computers for example. Data can be passed on as multiple individual outputs, which invoke the next activity as many times as there are items in the output.

You also have the option of passing on data as a single output. For information about how to configure Published Data with multiple values, see [Common Activity Properties](Common-Activity-Properties.md).

## Adding Returned Data to Activity Configurations
When an activity has subscribed to Published Data, a placeholder is inserted where the value of the data will be added. An activity can only subscribe to Published Data from a previous activity in the workflow.

Use the following procedures to add Published Data to an activity, to change the Published Data subscription, and to copy and paste Published Data items.

#### To subscribe to Published Data of an earlier  activity in the workflow

1.  Right\-click an activity from your runbook to select **Properties**, and then click the **Details** tab to open the activity’s properties dialog box.

2.  To open a menu, in the text box, right\-click to  select **Subscribe**, and then click **Published Data** to open the **Published Data** dialog box.

3.  In the **Activity** list, select the activity that returns the data that you want to subscribe to. By default, the dialog box only displays Published Data that is specific to that activity. To include Published Data that is common to all activities, click **Show common Published Data**.

4.  Select the **Published Data** item that you want to use, and then click **OK**.

#### To change the Published Data subscription

1.  In the text box, click the data placeholder to open the **Published Data** dialog box.

2.  In the **Activity** list, click the activity that returns the data that you want to subscribe to. By default, the dialog box only displays Published Data that is specific to that activity. To include Published Data that is common to all activities, click **Show common Published Data**.

3.  Click the **Published Data** item that you want to use, and then click **OK**. The Published Data placeholder changes to reflect the new activity and Published Data that you selected.

#### To copy and paste Published Data items

1.  Find a Published Data item that has already been inserted into a box in the **Properties** dialog box of an activity.

2.  Select the Published Data item that you want to copy.

3.  Use the keyboard shortcut CTRL\+C, or right\-click the selected item, and then click **Copy**.

4.  Open the **Properties** dialog box to which you want to copy the Published Data item.

5.  Place your cursor where you want the Published Data item to appear and use the keyboard shortcut, CTRL\+V, or right\-click the insertion point, and then click **Paste**. The Published Data item appears.

## Transforming Published Data Items
You might have to modify text from a **Published Data** activity before you use it in another activity. For example, you might have to remove a portion of the text or replace it with another string. You can transform the existing Published Data content or variable items into new content according to rules that you specify by using the [Map Published Data](Map-Published-Data.md) activity.

## <a name="CommonPublishedData"></a>Common Published Data
The following table describes the Published Data items common to all activities.

|Name|Description|
|--------|---------------|
|Activity ID|The unique identifier of the activity. For example, {4BD3F27A\-8F1B\-4F60\-8245\-F69469075EF1}.|
|Activity name|The name of the activity as it appears in the workspace. If you customize the name of an activity in the workspace, the customized name appears here.|
|Activity Process ID|The process ID of the job process where the activity runs.|
|Activity status|The result status of running the activity, for example, Success.|
|Activity type|The default name of the activity. It does not change from the default even if you rename the activity in the workspace, and it can be useful in identifying an activity in runbooks where activity names and display icons have been changed.|
|Error summary text|A summary of the error information that the activity returns.|
|Runbook name|The name of the runbook.|
|Runbook Process ID|The process ID of the runbook module’s executable program that is running on the runbook server.<br /><br />The job process contains the logic for the activity. It is started when the runbook server starts the runbook, and it is stopped when the runbook is stopped. Each runbook runs in its own job process executable program.|
|Server name|The name of the runbook server where the runbook is running.|
|Activity duration|The total time that the activity was running.|
|Activity end time|The time when the activity finished.|
|Activity end time \(year\)|The year when the activity finished.|
|Activity end time \(month\)|The month when the activity finished.|
|Activity end time \(day\)|The day when the activity finished.|
|Activity end time \(weekday\)|The day of the week when the activity finished.|
|Activity end time \(hours\)|The hour when the activity finished.|
|Activity end time \(minutes\)|The number of minutes past the hour when the activity finished.|
|Activity end time \(seconds\)|The number of seconds past the minute when the activity finished.|
|Activity end time in UTC|The time when the activity finished in UTC format.|
|Activity end time in UTC \(year\)|The year when the activity finished in UTC format.|
|Activity end time in UTC \(month\)|The month when the activity finished in UTC format.|
|Activity end time in UTC \(day\)|The day when the activity finished in UTC format.|
|Activity end time in UTC \(weekday\)|The day of the week when the activity finished in UTC format.|
|Activity end time in UTC \(hours\)|The hour when the activity finished in UTC format.|
|Activity end time in UTC \(minutes\)|The number of minutes past the hour when the activity finished in UTC format.|
|Activity end time in UTC \(seconds\)|The number of seconds past the minute when the activity finished in UTC format.|
|Activity start time|The time when the activity started.|
|Activity start time in UTC|The time when the activity started in UTC format.|
|Loop: Delay between attempts|The amount of time \(in seconds\) between each loop attempt.|
|Loop: Enabled|The setting that determines whether per\-activity looping is enabled for the activity.|
|Loop: Loop error message|The error message if the loop is not successful.|
|Loop: Number of attempts|The number of iterations that the loop has been through.|
||The name of the runbook to which that the activity belongs.|
|Loop: Total duration|The total amount of time \(in seconds\) that the looped activity ran.|

## See Also
[Building a Runbook](Building-a-Runbook.md)


