---
title: Example Runbook Monitoring a folder with a runbook
description: This article describes how you can use a sample to create a simple monitoring runbook that monitors a folder for new text files.
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 9be981fc-6708-4d00-a42a-2a15f0addbf0
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/05/2025
ms.custom: engagement-fy23
---

# Example Runbook: Monitor a folder with a runbook

This article shows you how to create a simple runbook that monitors a folder for new text files. When a file is detected, the runbook sends an event log message, and then starts another runbook.  

![Screenshot of Monitor Folder.](./media/monitor-a-folder-within-a-runbook/orch-2016-sample-monitor-folder.png)

## Create and test a monitor runbook

The procedures to create, configure, and test a simple runbook that monitors a folder are described below.  

### Create the workflow

Follow these steps to create a workflow:

1.  In the Runbook Designer **Connections** pane, right-click the **Runbooks** folder to select **New**, and then select **Runbook**.  

2.  Right-click the **New Runbook** tab to select **Rename**.  

3.  In the **Confirm Check out** dialog, select **Yes**.  

4.  Enter a name for the runbook, such as **Monitor Runbook**, and then press Enter.  

5. In the **Activities** pane, select **File Management** to expand the category, and then drag the **Monitor Folder** activity into the **Runbook Designer** Design workspace.  

6. In the **Activities** pane, select **Notification** to expand the category, and then drag the **Send Event Log Message** activity into the **Runbook Designer** Design workspace, to the right of the **Monitor Folder** activity.  

7. In the **Runbook Designer** Design workspace, move your pointer over the right side of the **Monitor Folder** activity to display the smart link arrow.  

8. Select the smart link arrow, and then drag it to the **Send Event Log Message** activity.  

9. In the **Activities** pane, select **Runbook Control** to expand the category, and then drag the **Invoke Runbook** activity into the **Runbook Designer** Design workspace, to the right of the **Send Event Log Message** activity.  

10. In the **Runbook Designer** Design workspace, move your pointer over the right side of the **Send Event Log Message** activity to display the smart link arrow.  

11. Select the smart link arrow, and then drag it to the **Invoke Runbook** activity.  

## Configure the workflow  

Follow these steps to configure the workflow:

1.  In the **Runbook Designer** Design workspace, double\-click the **Monitor Folder** activity.  

2.  In the **Monitor Folder Properties** dialog box, select the **General** tab.  

3.  In the **Name** box, change the name of the activity to something informative. For example, **Monitor C:\\Monitor Folder**.  

4.  Select the **Details** tab.  

5.  On the **Details** tab, in the **Path** box, enter the path of the folder you want to monitor. For example, **C:\\Monitor**.  

6.  Below the **File Filters** list, select **Add**.  

7.  In the **Filter Settings** dialog, set the following:  

    1.  In the **Name** list box, select **File Name**.  

    2.  In the **Relation** list box, select **Matches pattern**.  

    3.  In the **Value** box, enter **\*.txt**.  

        This setting directs the monitor to look for files with the **txt** extension. This field accepts regular expression syntax.  

8.  Select **OK**.  

9. Select the **Triggers** tab.  

10. Select the **Number of files is** option, set the value in the list to **greater than**, and then enter **0** in the edit box.  

11. Select **Finish**.  

12. In the **Runbook Designer** Design workspace, double-click the **Send Event Log Message**.  

13. In the **Send Event Log Message Properties** dialog, on the **Details** tab, in the **Properties** section, set the following:  

    1.  In the **Computer** box, enter the name of the computer to receive the Event message.  

        This is typically the computer where you're running Runbook Designer.  

    2.  In the **Message** box, enter the message to display in the Event log. For example, **File Detected**.  

    3.  Leave the **Severity** level at **Information**.

14. Select **Finish**.  

    > [!NOTE]  
    > In this sample, the **Invoke Runbook** activity isn't configured.  

## Modify runbook settings  

Follow these steps to modify the runbook settings:

1.  Above the **Runbook Designer** Design workspace, right-click the **Monitor Runbook** tab to select **Properties**.  

2.  In the **Monitor Runbook Properties** dialog, select the **Logging** tab, and then select both **Store Activity-specific Returned Data** and **Store Common Returned Data**.  

3.  Select **Finish**.  

4.  Right-click the **Monitor Runbook** tab to select **Check In**.  

## Test the runbook

In the Runbook Tester, you can test runbooks in a simulated runtime and debugging environment. You can run an entire runbook, step through it one activity at a time, or add breakpoints to stop the simulation at any activity that you select.  

Use the following steps to test your runbook in the **Runbook Tester**.  

### Prepare your computer  

Follow these steps to prepare your computer:

1.  Right-click **Start** to select **Open Windows Explorer**.  

2.  Create a **C:\\Monitor** folder on your computer.  

3.  Create a **C:\\Source** folder on your computer.  

4.  In the **C:\\Source** folder, create a file with a **txt** extension. For example, **text.txt**.  

### Test the runbook

Follow these steps to test the runbook:

1.  In the **Runbook Designer** Design workspace, select the **Monitor Runbook** tab.  

2.  On the toolbar above the **Runbook Designer** Design workspace, select **Runbook Tester**.  

3.  In the **Confirm Check out** dialog, select **Yes**.  

4.  In **Runbook Tester**, on the toolbar, select **Step Over** to start stepping through the runbook.  

    > [!TIP]  
    > To increase the size of the **Log** pane, remove the **Resource Browser** pane by selecting **View** on the menu, and then clearing the **Resource Browser** option.  

5.  In Windows Explorer, browse to the **C:\\Source** folder.  

6.  Copy **test.txt** to **C:\\Monitor**.  

7.  Close Windows Explorer.  

8.  On the Runbook Tester toolbar, select **Next**.  

    After a few moments, the **Log** pane entry updates and shows an event for the **Monitor Folder** activity.  

9. On the **Log** pane, select the **Show Details** link to see the contents of the data bus for that runbook.  

10. Scroll down the list of properties. If the activity status is **success**, it indicates that the **Monitor Folder** activity detected the change in the folder.  

11. On the Runbook Tester toolbar, select **Next**.  

    Notice that the **Log** pane changes and shows an event for the **Send Event Log Message** activity.  

12. Select the **Show Details** link. If the activity status is **success**, it indicates that the **Send Event Log Message** activity detected the change in the folder.  

13. Close **Runbook Tester**.  

14. On the **Runbook Designer** toolbar, select **Check In**.  

To access the published data, right-click in the text input box and select **Subscribe** > **Published Data**.

:::image type="content" source="./media/monitor-a-folder-within-a-runbook/send-event-log-message-properties.png" alt-text="Screenshot of send event log message properties page.":::

## Next steps

- Read [Design and build runbooks](design-and-build-runbooks.md) to learn more about building runbooks and get best practice guidance for designing runbooks.
- Read [Control runbook activities](control-runbook-activities.md) to learn more about the options for controlling runbook execution.
