---
title: Map Published Data
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9ddc895-bc37-4139-bf6d-87f21e064ade
---
# Map Published Data
The Map Published Data activity transforms the existing Published Data items or variable values into new values according to the rules that you specify. You can use this activity to convert numeric values to word values, simplify multiple versions of software program names into one name, or perform other string conversion activities within a runbook.

When you place this activity in a runbook, you must place it after the activities that create the Published Data items that you want to transform, and you must place it before activities that will use the new transformed items. . If you use the Map Published Data activity to transform variable items, you can place it at the beginning of the runbook.

## Configure the Map Published Data Activity
Before you configure the Map Published Data activity, you need to determine the following:

-   The names of the Published Data or variables that you want to transform.

-   The method you want to use to transform the Published Data or variable.

Use the following procedure to configure the Map Published Data activity.

#### To configure the Map Published Data activity

1.  From the **Activity pane**, drag a **Map Published Data** activity to the runbook.

2.  Double\-click the **Map Published Data** activity icon to open the **Properties** dialog box.

3.  Configure the settings on the **Mapping rules** tab. Configuration instructions are listed in the following table.

### Mapping rules

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Add**|Click **Add** to open the **Add Mapping** dialog box.|
|**Output Published Data**|Type the name that you want to assign to the new Published Data item that you are creating.|
|**Source data**|Insert Published Data or variable items to map to the new Published Data item. To insert items, right\-click the edit box and select **Subscribe**,   select **Published Data** or **Subscribe**, and then select **Variable**.  You can insert as many items as you want.<br /><br />You can also type text to transform to a new Published Data item.|
|**Pattern**|Type the existing pattern that you want to transform.|
|**Map To**|Type the new text that replaces the text of those items that match Pattern.<br /><br />Click **OK** to return to the **Map Published Data Properties** dialog box.|
|**Add**, **Edit**, **Remove**|If you want to add more rules, click **Add** and repeat the **Pattern** and **Map To** configuration instructions. On the **Mapping rules** tab, you will see a list of all transformations you created.<br /><br />To remove items from the rules list, click **Remove**. To edit an item in the rules list, click **Edit**.|

### Examples
The following examples describe how to use the Map Published Data activity.

-   Single Published Data or variable item

    The [Read Line](../Topic/Read-Line.md) activity creates a Published Data item called File and path name. If the path in this item is expressed as a drive letter, you can create a mapping to convert it to a UNC path.

    ##### To map a drive letter to a UNC path

    1.  In the **Source data** field, insert the File and path name Published Data item from the [Read Line](../Topic/Read-Line.md) activity.

    2.  In the **Pattern** field, type the drive letter and a colon, such as **Y:**

    3.  In the **Map to** field, type the UNC path that will replace Y:, such as **\\\\servername\\folder**.

    4.  Click **Add**, then **OK**.

-   Convert output of one system to be compatible with another system’s formatting

    You use two software programs that express severity levels with the following methods:

    -   Numerically: 0, 1, 2, and so on.

    -   Descriptions: High, Medium, or Low

    ##### To convert the numbers expressed by one software program to the words used by another

    1.  In the **Source data** field, insert the Published Data item for the severity level from the software program that expresses severity levels in numbers.

    2.  In the **Pattern** field, type **1**.

    3.  In the **Map to** field, type **High**.

    4.  Click **Add**.

    5.  Repeat for each severity level, such as 2, 3, and 4, match the appropriate word to each numeric value.

    6.  Click **OK**.

    To transfer severity levels to the software program that expresses them in words, insert the Published Data item that you created in the field. Items from the originating software program with a severity level of 1 are placed into the receiving software program with a severity level of High.

-   Wildcards

    You can replace strings of words with wildcards combined with words. For example, a Published Data item can describe Windows Server 2008 R2 inconsistently, as either Win2K8R2, or W2K8R2.

    There are two wildcards available:

    \* \- use the asterisk to search for any number of characters after your alpha\-numeric search character. For example, a\* will produce aa, aaa, aaaa, aaabbb, and so on.

    ? \- use the question mark to find a specified number of characters after your alpha\-numeric search character. For example, a?? will produce aaa, abb, abc, aac, but not aaaa or aaabbb, and so on.

    ##### To change variations in the data to a single value

    1.  In the **Source data** field, insert the Published Data item that represents the inconsistent names.

    2.  In the **Pattern** field, type **W\*K8**.

    3.  In the **Map to** field, type **Windows Server 2008**

    4.  Click **Add**, and then click **OK**.

-   Multiple Published Data or Variable Items

    Operating system names are usually composed of multiple parts, such as manufacturer, platform, version year, and release. In Orchestrator, each part of a name can be represented by an individual Published Data item. You can combine multiple Published Data items into one new item, such as Windows Server.

    ##### To map multiple values to a single value

    1.  In the **Source data** field, insert each Published Data item that you want to combine into the new item, separated by spaces.

    2.  In the **Pattern** field, type **Windows Server\***.

    3.  In the **Map to** field, type **Windows Server**.

    4.  Click **Add**, then **OK**. All references are changed to Windows Server.

### Published Data
This activity only generates Published Data that you specify.

