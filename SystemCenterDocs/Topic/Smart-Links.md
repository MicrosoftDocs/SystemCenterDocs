---
title: Smart Links
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 21b60698-13ee-48bc-8575-1c1534fbb981
---
# Smart Links
The links that connect individual activities in a runbook are called smart links. Smart links in [!INCLUDE[orchlong](../Token/orchlong_md.md)] support precedence between two activities. Smart links invoke the next activity in the runbook as soon as the previous activity finishes successfully. Smart links also provide filtering capabilities for the data so you can limit the data passed to subsequent activities in the workflow.

## Creating and configuring smart links
You can modify the smart link condition properties by double\-clicking the smart link.

Use the following procedure to enable or disable smart links.

#### To create a smart link

1.  In the **Runbook Designer** Design workspace, click and drag two activities from the **Activities** pane to the **Runbook Designer** Design workspace.

2.  In the **Runbook Designer** Design workspace, hover the mouse cursor over one of the activities, click the Right Arrow, and then drag it to the destination activity.

    A line is created between the two activities indicating a smart link is created.

#### To disable a smart link connection while preserving configured properties

-   To disable the smart link, right\-click the smart link to toggle **Enable**.

    The smart link changes to a dashed line indicating that it is disabled.

#### To enable a smart link connection

-   To enable the smart link, right\-click a disabled smart link to toggle **Enable**.

    The smart link changes to a solid line to indicate that it is enabled.

## General Tab
In the **Link Properties** dialog box, on the **General** tab, you can add Name and Description values to the smart link. These properties are not required, but are useful in identifying the purpose of the smart link. These properties are not displayed unless you configure the runbook option to show link labels.

#### To add a smart link label from the Runbook Designer

-   To view the smart link name, right\-click a smart link to select **Properties**.

-   In the **Properties** dialog box, on the **General** tab, in the **Name** box, enter a descriptive name.

-   Click **Finish**.

#### To display smart link names in the runbook

1.  On the **Runbook Designer** menu, click **Options**, and then click **Configure** to open the **Configuration** dialog box.

2.  Select **Show link labels**.

3.  Click **Finish**.

## Include and Exclude Tabs
[!INCLUDE[orchshort](../Token/orchshort_md.md)] lets you configure conditions for passing data to the following tasks in the runbook. By using link conditions, you can build branching capabilities into your runbooks. For example, a runbook must stop a database server before backing it up. If the database server stops correctly, the runbook starts the backup application. If the database does not stop correctly, an email is sent to the administrator to escalate the issue.

On the **Include** tab, you can specify the conditions that enable data to flow to the next activity in the runbook. The **Exclude** tab specifies the conditions that cause data to be excluded from the next activity in the runbook.

> [!IMPORTANT]
> The rules of the smart link **Exclude** tab supersede the rules on the smart link **Include** tab.

> [!IMPORTANT]
> The rules on each tab are joined by using an **or** condition. Only one of the conditions defined on a tab must be true for the condition to be true.

Use the following procedure to add or remove a condition to a smart link.

#### To add a smart link condition

1.  Right\-click a smart link to select **Properties** to open the **Link Properties** dialog box.

    > [!IMPORTANT]
    > To change the values that make up the rule, you have to select each underlined portion of the smart link condition.

2.  Click the listed activity in the condition to open the **Published Data** dialog box.

3.  Select the **Show common Returned Data** box to display properties that are common to all activities.

4.  Select a property from the Published Data and click **OK**. The criteria expression is changed depending on the type of data that the property returns.

5.  To change the different parts of the expression, select the underlined text, and then either select or type in an appropriate value. For more information about criteria, see [Smart link criteria](../Topic/Smart-Links.md#BMK_Smartlinkcriteria).

6.  Click **Finish**.

#### To remove a smart link condition

1.  In the **Link Properties** dialog box, click either the **Include** tab or **Exclude** tab.

2.  To select the condition that you want to remove, click to the right of the link condition on the word **or**, and then click **Remove**.

3.  Click **Finish**.

## Options Tab
In the **Link Properties** dialog box, on the **Options** tab, you can specify different link colors on your branches to make them easier to read. For example, you can select green for the **Pass** branch and red for the **Fail** branch to identify the difference logic paths.

On this tab, you can also specify a delay before the activity runs.

Use the following procedure to configure these settings.

#### To configure smart link colors

1.  Click **Color**, and then click the color of the smart link that you want.

2.  Click **Width** of the smart link line in pixels to specify the width.

3.  Click **Finish**.

#### To configure smart link activity delay

1.  In the **Trigger delay** box, type the number of seconds that you want the smart link to wait before invoking the next step in the runbook.

2.  Click **Finish**.

## <a name="BMK_Smartlinkcriteria"></a>Smart Link Criteria
Link criteria can be created for any data published from the activity that initiates the link. The type of criteria depends on the type of data returned from the particular property. The following sections provide details on the different types of data that activities can return.

### Activity Completion Status
When you add a new criteria to the link, it will default to the completion status of the activity. This status returns one of the following values:

-   success

-   warning

-   failed

Each time you create a new link, it creates a default criteria specifying that the activity’s completion status must return **success**. If you want the next activity to run regardless of whether the first activity successfully finished, you should delete or change criteria.

### Binary Values
Some properties return a value of **true** or **false**. You can set a criteria of equals or does not equal, and the value prompts you for the two possible values.

### Text Values
Certain published data properties return text that you can compare to an expected value or pattern. The following table shows the different criteria that can be used.

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
> Text values are not case\-sensitive.

> [!IMPORTANT]
> The regular expression criteria have a slightly different behavior than other regular expressions when using the ^ character specifying the starting position in the text and the $ character specifying the ending position in the text. You must specify a wildcard in addition to these operators. For example, with the string “This is some sample text”, **text$** returns a false, but **.\*text$** returns true. Similarly, **^This** returns false, but **^This.\*** returns **true**.

### Numeric Values
Certain published data properties return numeric data that you can compare to an expected value. The following table shows the different criteria that can be used.

|Condition|Description|
|-------------|---------------|
|equals|The value of the Published Data item is exactly equal to the specified value.|
|does not equal|The value of the Published Data item does not equal the specified value.|
|is less then|The value of the Published Data item is less than the specified value.|
|is greater then|The value of the Published Data item is greater than the specified value.|
|is less than or equal to|The value of the Published Data item is less than or equal to the specified value.|
|is greater than or equal to|The value of the Published Data item is greater than or equal to the specified value.|
|is between|The value of the Published Data item is between two specified values.|

## See Also
[Workflow Control](../Topic/Workflow-Control.md)

