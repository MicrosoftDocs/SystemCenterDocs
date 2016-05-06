---
title: Creating and Testing a Sample Runbook_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02e5bf0f-625d-4396-8588-1d0979d59570
---
# Creating and Testing a Sample Runbook_1
The following topic describes how to create and test a simple runbook. The purpose of this runbook is to detect when a text file is added to a particular folder, copy that file to another folder, read the contents of the file, append a line from the copied file to another file, and then delete the original file.

The runbook starts with a **Monitor File** activity to wait for the text file to be created. It then uses the **Copy File**, **Read Line**, **Append Line**, and **Delete File** activities to perform the other functions. A **Junction** activity is used to coordinate the activities so that the **Copy File** and **Append Line** activities are both completed before the source file is deleted.

## Creating the runbook
Use the following procedures to create the runbook by using the required activities.

#### To create a runbook

1.  Click **Start**, point to  **All Programs**, click **Microsoft System Center 2012**, click **Orchestrator**, and then click **Runbook Designer**.

2.  In the **Connections** pane, right\-click **Runbooks** to select **New**, and then click **Runbook**.

    A **New Runbook** tab appears at the top of the **Runbook Designer** Design workspace with the name **New Runbook**.

3.  Right\-click the **New Runbook** tab to select **Rename**.

    In the **Confirm Check out** dialog box, click **Yes**.

4.  Type **Append and Copy Workflow** in the **Input** box, and then press Enter.

You have created a new runbook and are ready to begin adding and configuring activities.

#### To add and configure a Monitor File activity

1.  With the newly created **Append and Copy Workflow** runbook open, in the **Activities** pane, expand the **File Management** category.

2.  Click and drag the **Monitor File** activity to the **Runbook Designer** Design workspace.

3.  Double\-click the **Monitor File** activity to open its **Properties** dialog box.

4.  In the **In folder** box, type **C:\\Drop**.

5.  In the **Filters** section, click the **Add** button.

6.  In the **Filter Settings** dialog box, in the **Name** list, select **File Name**.

7.  In the **Relation** list, select **Matches Pattern**.

8.  In the **Value** box, type **\*.txt**.

9. Click **OK**.

10. Click the **Triggers** tab.

11. In the **Trigger if one of the files was** section, select the **Created** check box, and then click **Finish**.

The **Monitor File** activity is created and configured to watch for any new text files that are created in the C:\\Drop folder.

#### To add additional activities to the runbook

1.  In the **Activities** pane, expand the **File Management** category.

2.  Click and drag the **Copy File** activity to the **Runbook Designer** Design workspace.

3.  Expand the **Text File Management** category.

4.  Click and drag the **Read Line** activity to the **Runbook Designer** Design workspace.

5.  To create a link between the **Monitor File** activity and the **Copy File** activity, click and drag the right arrow of the **Monitor File** activity to the **Copy File** activity.

6.  To create a link between the **Monitor File** activity and the **Read Line** activity, click and drag the right arrow of the **Monitor File** activity to the **Read Line** activity.

By adding both the **Read Line** activity and the **Copy File** activity, you have created a workflow.

#### To configure the Copy File activity

1.  In the **Append and Copy Workflow** runbook, right\-click the **Copy File** activity to  select **Properties**.

2.  On the **Details** tab, right\-click the **File** box to select **Subscribe**, and then click **Published Data** to open the **Published Data** dialog box.

    The **Monitor File** activity is listed at the top of the **Published Data** dialog box because this is the activity just before to the selected activity.

3.  In the **Name** column, select **Name and path of the file**, and then click **OK**. This populates the **File** property of the **Copy File** activity with the name of and path to the file from the **Monitor File** activity.

4.  In the destination **Folder** box, type **C:\\Copy**.

5.  Click **Finish**.

The **Copy File** activity is now configured to copy files from the source folder to the destination folder.

#### To configure the Read Line activity

1.  In the **Append and Copy Workflow** runbook, right\-click the **Read Line** activity to select **Properties**.

2.  On the **Details** tab, right\-click the **File** box to select **Subscribe**, and then click **Published Data** to open the **Published Data** dialog box.

3.  In the **Activities** list, select **Monitor File**.

4.  In the **Name** column, select **Name and path of the file**, and then click **OK**.

5.  Click the ellipse \(**…**\) button to the right of the **File encoding** box, and then select **auto**.

6.  In the **Line numbers** box, type **1\-END**, and then click **OK**.

7.  Click **Finish**.

The Read Line activity is now configured.

#### To add an Append Line activity

1.  In the **Activities** pane, expand the **Text File Management** category.

2.  Click and drag the **Append Line** activity to the **Runbook Designer** Design workspace to the right of the **Read Line** activity.

3.  To create a link from the **Read Line** activity to the **Append Line** activity, click and drag the right arrow of the **Read Line** activity to the **Append Line** activity.

4.  Right\-click the **Append Line** activity to select **Properties**.

5.  On the **Details** tab in the **File** box, type **C:\\Copy\\Masterlog.txt**.

6.  Click the ellipse \(**…**\) button to the right of the **File encoding** box, and then select **auto**.

7.  Right\-click the **Text** box to select **Subscribe**, and then click **Published Data** to open the **Published Data** dialog box.

8.  In the **Name** column for the **Read Line** activity, select **Line text**, and then click **OK**.

9. Click **Finish**.

The **Append File** activity is now configured to append files to the **Masterlog.txt** file.

#### To synchronize branches of a runbook

1.  In the **Activities** pane, expand the **Runbook Control** category.

2.  Click and drag the **Junction** icon to the **Runbook Designer** Design workspace.

3.  To create a link from the **Append Line** activity to the **Junction** activity, click and drag the right arrow of the **Append Line** activity to the **Junction** activity.

4.  To create a link from the **Copy File** activity to the **Junction** activity, click and drag the right arrow of the **Copy File** activity to the **Junction** activity.

5.  Right\-click the **Junction** activity to select **Properties**.

6.  Click the ellipse \(**…**\) button next to the **Return data from** box, and then select **Copy File**. Click **OK**. This action configures the activity to return the same Published Data as the **Copy File** activity.

7.  Click **Finish**.

The **Junction** activity is configured to coordinate the workflow so that no further activities run until both the **Copy File** activity and **Append Line** activity finish.

#### To add and configure the Delete File activity

1.  In the **Activities** pane, expand the **File Management** category.

2.  Click and drag the **Delete File** icon to the **Runbook Designer** Design workspace.

3.  To create a link from the **Junction** activity to the **Delete File** activity, click and drag the right arrow of the **Junction** activity to the **Delete File** activity.

4.  Right\-click the **Delete File** activity to select **Properties**.

5.  Right\-click the **Path** box to select **Subscribe**, and then click **Published Data** to open the **Published Data** dialog box.

    In the **Activity** list, select **Copy File**.

6.  In the **Name** column, select **Name and path of the original file**, and then click **OK**.

7.  Click **Finish**.

The **Append and Copy Workflow** runbook is now completed. It should look similar to the following illustration.

![](../Image/SampleRunbook1.jpg)

## Testing the runbook
You can test the runbook by using the Runbook Tester. This tool lets you run the entire runbook and inspect the completion status and output of each activity. The Runbook Tester runs the activities, so you must first create the folders specified for the runbook.

#### To test the runbook

1.  Create a folder on the runbook server called C:\\Drop.

2.  Create a folder on the runbook server called C:\\Copy.

3.  With the **Append and Copy Workflow** runbook selected in the Runbook Designer, on the toolbar, click **Runbook Tester**.

4.  Click **Run To Breakpoint**. The **Monitor File** activity is loaded and waits for a text file to be created in the C:\\Drop folder.

5.  Open **Notepad** and type a few lines of text. Save the file as C:\\Drop\\File1.txt.

6.  Wait a few moments for the other activities to run. Ensure that each of the activities is completed successfully.

7.  To view the Published Data and other details of an activity, click **Show Details** for the activity.

8.  Open the C:\\Drop folder and ensure that the file has been removed.

9. Open the C:\\Copy folder and ensure that the file has been copied. Also verify that the MasterLog.txt file has the contents of the original file.

## See Also
[Runbook Samples](../Topic/Runbook-Samples.md)

