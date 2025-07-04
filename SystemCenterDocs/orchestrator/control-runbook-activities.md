---
title: Control runbook activities
description: This article describes how to manipulate data and control the sequence of operations in an Orchestrator runbook.
ms.service: system-center
ms.subservice: orchestrator
ms.topic: how-to
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: engagement-fy23
---
# Control runbook activities

You set the sequence of operations in runbooks by linking activities together in the **Runbook Designer**. These links are known as **smart links** because you can configure them to control the type of data passed from one activity to another. You can also control when the runbook completes activities by setting the logic for when those operations run with embedded loops. Finally, you can use text and numerical operations to manipulate data as it passes between activities, or to set conditions for the order of operations. This article describes how to control sequencing and manipulate data within your runbook.

## Control activity sequence with smart links

The activities in your runbook will complete according to the order you set by linking them together. You can control the data that flows between the activities by using the Include and Exclude tabs of the **Link Properties**. For example, you could only include data to be passed to the subsequent activity that meets a particular criteria.  

> [!IMPORTANT]  
> The rules of the smart link **Exclude** tab supersede the rules on the smart link **Include** tab.  

> [!IMPORTANT]  
> The rules on each tab are joined by using an **or** condition. Only one of the conditions defined on a tab must be true for the condition to be true.  

The type of data published by an activity determines the type of criteria you can set for controlling the runbook sequence. Some activities publish binary data, and others publish numeric or text data.

If the published data is text data, you can use any of the following to set the criteria for execution, inclusion, or exclusion.  

|Condition|Description|  
|-------------|---------------|  
|contains|The specified text appears somewhere in the value of the Published Data item.|  
|does not contain|The specified text does not appear somewhere in the value of the Published Data item.|  
|starts with|The value of the Published Data item starts with the specified text.|  
|ends with|The value of the Published Data item ends with the specified text.|  
|matches pattern|The value of the Published Data item matches the specific regular expression.|  
|does not match pattern|The value of the Published Data item matches the specific regular expression.|  
|equals|The value of the Published Data item exactly matches the specified text.|  
|does not equal|The value of the Published Data item does not match the specified text.|  

> [!NOTE]  
> Text values aren't case-sensitive.

You can also set criteria using regular expressions to perform pattern matching.

If the published data is numerical, you can use any of the following to set the criteria for execution, inclusion, or exclusion.

|Condition|Description|  
|-------------|---------------|  
|equals|The value of the Published Data item is exactly equal to the specified value.|  
|does not equal|The value of the Published Data item does not equal the specified value.|  
|is less than|The value of the Published Data item is less than the specified value.|  
|is greater than|The value of the Published Data item is greater than the specified value.|  
|is less than or equal to|The value of the Published Data item is less than or equal to the specified value.|  
|is greater than or equal to|The value of the Published Data item is greater than or equal to the specified value.|  
|is between|The value of the Published Data item is between two specified values.|

Select the required tab for steps to add or remove a smart link condition:

# [Add a smart link condition](#tab/AddSmartLink)

Follow these steps to add a smart link condition:

1. Right-click a smart link to select **Properties** to open the **Link Properties** dialog.  

    > [!IMPORTANT]  
    > To change the values that make up the rule, you have to select each underlined portion of the smart link condition.  

2. Select the listed activity in the condition to open the **Published Data** dialog.  

3. Select the **Show common Returned Data** box to display properties that are common to all activities.  

4. Select a property from the Published Data and select **OK**. The criteria expression is changed depending on the type of data that the property returns.  

5. To change the different parts of the expression, select the underlined text, and then either select or enter an appropriate value.

6. Select **Finish**.  

# [Remove a smart link condition](#tab/RemoveSmartLink)

Follow these steps to remove a smart link condition:

1. In the **Link Properties** dialog, select either the **Include** tab or **Exclude** tab.  

2. To select the condition that you want to remove, select to the right of the link condition on the word **or**, and then select **Remove**.  

3. Select **Finish**.

---

## Repeat activities with embedded loops

By using loops, you can build automatic retries and monitor at any location in a runbook.  

You can create a loop for any activity so that you can retry operations if they fail or test the output information of the activity for valid data. You can also use these mechanisms to build wait conditions into your workflows.  

When you configure a loop for an activity, it will continue to run with the same input data until a desired exit looping criteria is reached. You build the exit criteria for the loop in a similar way as smart link configurations. You can use any published data item from the activity as part of the exit or don't exit configuration. Included in the common published data are special data items, such as **Loop: Number of attempts** and **Loop: Total duration**, that let you use information from the loop itself in the looping conditions.  

Loops run one time for each incoming piece of data that is passed to the activity. For example, consider a runbook that uses a **Query Database** activity followed by **Append Line**. If the **Query Database** activity returned three rows, the **Append Line** activity would run three times. If you have a loop on the **Append Line** activity, it would run three separate loops. After the first data item has looped through the **Append Line** activity, the next item goes through **Append Line** and loops until it exits, and then the third begins. After all three items have been processed, the next activity in the runbook runs.  

### Configure looping  

1. Right-click an activity in the runbook to select **Looping**. The **Looping Properties** dialog opens.  

2. On the **General** tab, select **Enable**.  

3. In the **Delay between attempts** box, enter the number of seconds to pause between each attempt to run the activity.  

### Exit and Do Not Exit Conditions

The rules on the **Exit** tab specify the conditions that determine whether the loop exits. The rules on the **Do Not Exit** tab specify the conditions that cause the loop to continue.  

> [!IMPORTANT]  
> The rules on the **Do Not Exit** tab supersede the rules on the **Exit** tab.  

The rules within each tab are joined by using an **Or** condition. Only one of the conditions on a tab must be true for the entire tab to be true.  

Select the required tab for the procedure to add or remove an **Exit** condition:  

# [Add an exit condition](#tab/AddExitCondition)

Follow these steps to add an exit condition:

1. In the **Looping Properties** dialog, select either the **Exit** tab or **Do Not Exit** tab, and then select the condition listed in the box select **Add** to add a condition.  

    > [!IMPORTANT]  
    > To change the values that make up the rule, you have to select each underlined portion of the link condition.  

2. Select the listed activity in the condition to open the **Published Data** dialog.  

3. Check the **Show common Returned Data** box to display properties that are common to all activities.  

4. Select a property from the published data, and then select **OK**. The criteria expression is changed depending on the type of data that the property returns.  

5. To change the different parts of the expression, select the underlined text and either select or enter an appropriate value.  

6. Select **Finish**.  

# [Remove an exit condition](#tab/RemoveExitCondition)

Follow these steps to remove an exit condition:

1. In the **Looping Properties** dialog, select either the **Exit** tab or the **Do Not Exit** tab.  

2. To select the condition you want to remove, select **Or** to the right of the link condition, and then select **Remove**.  

3. Select **Finish**.  

---

## Set a schedule for a runbook

You can set a schedule to control when a runbook runs. For example, there are times when it's inappropriate to run some runbooks, such as backing up a runbook on a main server during regular business hours. You can create a schedule that runs according to a complex interval, such as the first and third Mondays and Thursdays of every month, except when these days fall on a holiday.  

Schedules use the system clock of the Runbook server that runs the runbook. This enables schedules to function in virtual machine environments, and to continue running even when the system clock is adjusted because of the move to or from daylight savings time.  

Runbooks that start before a prohibited time run until finished, even if they're still processing when the prohibited time arrives. They won't be interrupted after processing has started.  

> [!IMPORTANT]  
> The access permissions for schedules can be modified, but the runbook server doesn't enforce these permissions.  

> [!NOTE]  
> If you schedule a runbook to start during an hour that is skipped when the system clock is adjusted forward by one hour, that starting time is skipped, and the runbook starts at the next scheduled time. If you schedule a runbook to start during an hour that occurs two times because the system clock is adjusted backward by one hour, the runbook starts two times.  

> [!NOTE]  
> Orchestrator doesn't support moving multiple schedules with multiple\-selection. To move more than one schedule to another folder, you must move each schedule individually.

Select the required tab to create a schedule, assign a schedule to a runbook, or remove a schedule from a runbook:

# [Create a schedule](#tab/CreateASchedule)

Follow these steps to create a schedule:

1. In the **Connections** pane, right-click the **Schedules** folder or a subfolder of the **Schedules** folder, point to **New**, and then select **Schedule** to open the **New Schedule** dialog.  

2. On the **General** tab, in the **Name** box, enter a name for the schedule.  

3. In the **Description** box, enter a description that describes or explains the purpose of the schedule.  

4. Select the **Details** tab. Select the days that this schedule allows runbooks to run:  

    **Days of week**: Select this option and select the days of the week when this schedule allows runbooks to run.  

    **Occurrence**: Select the weeks of the month when the schedule allows runbooks to run.  

    **Days of month**: Select this option and select the days of the month when this schedule allows runbooks to run. Specify the days of the month by entering the number of the day. You can use hyphens to describe ranges and commas to separate entries. For example, typing **1,3** includes the first and third day of the month. Entering **1\-21** includes the first through to the twenty\-first day of the month. You can combine both to create complex descriptions of the days of the month. Enter **all** to specify all days of the month. Enter **last** to specify the last day of the month.  

    You can't use **all** and **last** as part of a range of days. Additionally, if you entered a range of 5\-31, this range works correctly for all the months, including those with 28, 29, 30, and 31 days.  

5. Select **Hours** to open the **Schedule Hours** dialog.  

6. Select and drag to select a group of hours in a week. The text at the bottom of the dialog shows the time period that you selected. Then select one of the following:  

    **Permit** \(blue\): assigns the time period that you selected as a time when runbooks are allowed to run.  

    **Denied** \(white\): assign the time period that you selected as a time when runbooks are not allowed to run.  

7. Select **OK**.  

8. Select the **Exceptions** tab. The list displays all the days that are exceptions to the rules defined in the **Details** tab.  

9. Select **Add** to open the **Date** dialog.  

10. Specify the date and select **Allow** or **Disallow** to allow or not allow the runbook to run on that day, and then select **OK**. The entry appears in the list.  

11. To modify an Exception entry, select it, and then select **Modify**. To remove the Exception entry, select it, and then select **Remove**.  

12. To modify a schedule, double\-click the **Schedule**.  

13. To remove a schedule, right-click the **Schedule**, and then select **Delete**.  

14. Select **Finish**.  

# [Assign a schedule to a runbook](#tab/AssignASchedule)

Follow these steps to assign a schedule to a runbook:

1. Right-click the runbook tab, and then select **Properties** to open the **Runbook Properties** dialog.  

2. On the **General** tab, select the ellipsis **\(...\)** button to open the **Select a Schedule** dialog.  

3. Select the schedule that you want to apply to the runbook, and then select **OK**.  

4. Select **Finish**.  

    Every time the runbook is started, it checks the schedule to verify that it's allowed to run. If it isn't allowed to run, it stops and doesn't restart until the next time it's started.  

# [Remove a schedule from a runbook](#tab/RemoveASchedule)

Follow these steps to remove a schedule from a runbook:

1. Right-click the runbook tab, and then select **Properties** to open the **Runbook Properties** dialog.  

2. On the **General** tab, select the ellipsis **\(...\)** button to open the **Select a Schedule** dialog.  

3. Don't select a schedule. Select **OK**.  

4. Select **Finish**. The schedule is removed from the runbook.

---

## Manipulate data with functions

You may need to manipulate string data from text files, returned data, or other sources, and convert it into a usable form for your runbook activities. In addition, you can perform simple arithmetic operations, such as calculating sums and differences and performing division and multiplication operations. For example, you can extract text from a text file by using a **Text File Management** activity, trim leading and trailing spaces from the text, and then retrieve specific parts of the text that you can pass to other activities as returned data items.  

You manipulate data in the runbook by inserting a function. Data manipulation functions must be enclosed in square brackets \('\[' and '\]'\). For example:  

`[Upper('this will be inserted in upper case')]`  

When the activity runs, the text 'this will be inserted in uppercase' in the example is replaced with 'THIS WILL BE INSERTED IN UPPERCASE'.

Functions are case\-sensitive. For example, Upper\('Text'\) will be processed, but upper\('Text'\) will not.  

The table below lists the functions supported for runbooks.

|Function and Definition|Usage|Parameters|Example|  
|---------------------------|---------|--------------|-----------|  
|Upper \- converts text to uppercase.|Upper\('Text'\)|Text \- the text that is being converted to uppercase.|Upper\('this will be converted to uppercase'\) returns 'THIS WILL BE CONVERTED TO UPPERCASE'|  
|Lower \- converts text to lowercase.|Lower\('Text'\)|Text \- the text that is being converted to lowercase.|Lower\('This Will Be Converted To Lowercase'\) returns 'this will be converted to lowercase'|  
|Field \- returns text in a specific position.|Field\('Text', 'Delimiter', Field Number\)|Text \- the text that is being searched.<br /><br />Delimiter \- the character that separates each field.<br /><br />Field Number \- the position of the field that is being returned \(starting at 1\).|Field\('John;Smith;9055552211', ';', 2\) returns 'Smith'|  
|Sum \- returns the sum of a set of numbers.|Sum\(firstNumber, secondNumber, thirdNumber, ...\)|Number \- the number that is being added. You can put any set of numbers, each separated by a comma \(,\).|Sum\(2,3,4,5\) returns '14'|  
|Diff \- returns the difference of two numbers.|Diff\(Number1, Number2, \<Precision\>\)|Number1 \- the number that will be subtracted from.<br /><br />Number2 \- the number that will be subtracted from Number1.<br /><br />Precision \<Optional\> \- the number of decimal places that the result will be rounded to.|Diff\(9, 7\) returns '2'<br /><br />Diff\(9.3, 2.1, 2\) returns '7.20'|  
|Mult \- returns the product of a set of numbers.|Mult\(firstNumber, secondNumber, thirdNumber, ...\)|Number \- the number being multiplied. You can put any set of numbers, each separated by a comma \(,\).|Mult\(2, 3, 4\) returns '24'|  
|Div \- returns the quotient of two numbers.|Div\(Number1, Number2, \<Precision\>\)|Number1 \- the number that will be divided.<br /><br />Number2 \- the number that will divide Number1.<br /><br />Precision \<Optional\> \- the number of decimal places that the result will be rounded to.|Div\(8, 4\) returns '2'<br /><br />Div\(9, 2, 2\) returns '4.50'|  
|Instr \- returns the position of first occurrence of text within another text.|Instr \('SearchText', 'TextToFind'\)|SearchText \- the text that is being searched.<br /><br />TextToFind \- the text that you are searching for.|Instr\('This is a string that is searched', 'string'\) returns 11|  
|Right \- returns a subset of the text from the right side of the full text.|Right\('Text', Length\)|Text \- the full text.<br /><br />Length \- the number of characters from the right side that will be returned.|Right\('Take from the right', 9\) returns 'the right'|  
|Left \- returns a subset of the text from the left side of the full text.|Left\('Text', Length\)|Text \- the full text.<br /><br />Length \- the number of characters from the left side that will be returned.|Left\('Take from the left', 4\) returns 'Take'|  
|Mid \- returns a subset of the text from the middle of the full text.|Mid\('Text', Start, Length\)|Text \- the full text.<br /><br />Start \- the starting position in the text where you want to begin returning characters.<br /><br />Length \- the number of characters starting from the Start position that will be returned.|Mid\('Take from the middle', 5, 4\) returns 'from'|  
|LTrim \- trims leading spaces from text.|LTrim\('Text'\)|Text \- the text that is being trimmed of leading spaces.|LTrim\(' Remove the leading spaces only. '\) returns 'Remove the leading spaces only. '|  
|RTrim \- trims the trailing spaces from text.|RTrim\('Text'\)|Text \- the text that is being trimmed of trailing spaces.|RTrim\(' Remove the trailing spaces only. '\) returns ' Remove the trailing spaces only.'|  
|Trim \- trims leading and trailing spaces from text.|Trim\('Text'\)|Text \- the text that is being trimmed.|Trim\(' Remove leading and trailing spaces. '\) returns 'Remove leading and trailing spaces.'|  
|Len \- returns the length of text.|Len\('Text'\)|Text \- the text that is being measured.|Len\('Measure this text'\) returns 17|

>[!Note]
>Functions are case\-sensitive. For example, Upper\('Text'\) will be processed, but upper\('Text'\) will not.

## Next Steps

To read a guided walkthrough of creating a sample runbook, see [Creating and testing a sample runbook](~/orchestrator/creating-and-testing-a-sample-runbook.md).
