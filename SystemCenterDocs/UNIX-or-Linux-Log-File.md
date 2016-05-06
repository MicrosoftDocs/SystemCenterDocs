---
title: UNIX or Linux Log File
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9859313b-9105-44bc-9a50-d48814bcb28f
---
# UNIX or Linux Log File
The **UNIX\/Linux Log File Monitoring** template lets you create an alert when a particular text is detected in a log file.

## Scenarios
Use the **UNIX\/Linux Log File Monitoring** template for any application that writes to a log file when a particular error occurs. You provide the path to the log file and the text that indicates an error, and an alert is created for you anytime that text is detected.

## Monitoring Performed by the UNIX\/Linux Log File Monitoring Template
The following table shows the monitoring activity that the **UNIX\/Linux Log FileMonitoring**  template performs.

|Type|Description|When Enabled|
|--------|---------------|----------------|
|Rule|Creates an alert when a specified text is detected.|Enabled|

## <a name="Options"></a>Wizard Options
When you run the **UNIX\/Linux Log File Monitoring** template, you have to provide values for the options in the following tables. Each table represents a single page in the wizard.

### General Options
The following options are available on the **General Options** page of the wizard.

|Option|Description|
|----------|---------------|
|Name|The name used for the template. This name is displayed in the Operations console.|
|Description|Optional description of the template.|
|Management Pack|Management pack file to store the rule that the template creates.<br /><br />For more information about management packs, see [Selecting a Management Pack File](../Topic/Selecting-a-Management-Pack-File.md).|

### Log File Details
The following options are available on the **Log File Details** page of the wizard.

|Option|Description|
|----------|---------------|
|Computer|If you want to monitor a single computer, enter the name of the agent\-managed UNIX or Linux computer with the log file to monitor. Click the **Select a Computer** button to select one of the agent\-managed UNIX or Linux computers that are installed in your management group.|
|Computer group name|If you are going to monitor a group of computers, enter the name of the group of agent\-managed UNIX or Linux computers with the log file to monitor. Click the **Computer Group** button to select from the group in your management group.|
|Log file path|Complete path and name of the log file.|
|Expression|Regular expression of the text to detect. If you want to detect a simple string of characters, type the string of characters.|

### Creating and Modifying UNIX\/Linux Log File Templates

##### To create a UNIX\/Linux Log File template

1.  If you want to monitor the log file on a group of computers, determine the target group for the monitor by using the following logic:

    -   If you want to monitor the log file on all UNIX and Linux computers in the management group, you do not have to create a group. You can use the existing group **UNIX\/Linux Computer Group**.

    -   If you only want the log file to be monitored on a certain group of computers, either ensure that an appropriate group exists or create a new computer group by using the procedure in [How to Create Groups in Operations Manager](../Topic/How-to-Create-Groups-in-Operations-Manager.md).

2.  Start the **Add Monitoring** wizard.

3.  On the **Select Monitoring Type** page, select **UNIX\/Linux Log File Monitoring**, and then click **Next**.

4.  On the **General Properties** page, in the **Name** and **Description** boxes, type a name and description for this new template.

5.  Select a management pack in which to save the template or click **New** to create a new management pack. For more information, see [Selecting a Management Pack File](../Topic/Selecting-a-Management-Pack-File.md).

6.  If you want to monitor the log file on a single computer, do the following:

    1.  Click the **Select a Computer** button next to the **Computer name** box.

    2.  Select the computer to monitor, and then click **OK**.

7.  If you want to monitor the log file on a group of computers, do the following:

    1.  Click the **Select a Group** button next to the **Computer group name** box.

    2.  Select the computer to monitor, and then click **OK**.

8.  In the **Log file path** box, type the path and name of the log file to monitor.

9. In the **Expression** box, type the text to watch for, such as **error**. You can type a regular expression for more complex logic.

10. Optionally, click **Test** to open a new dialog to test Regular expression matching against sample text that you input.

11. Select a **Run As Profile** to use. The account associated with the target computer in this profile will be used to read the log file.

12. Select an **Alert Severity**.

13. Click **Next**.

14. Verify the summary information for the template, and then click **Create**.

##### To modify an existing UNIX\/Linux Log File template

1.  Open the Operations console with a user account that has Author credentials.

2.  Open the **Authoring** workspace.

3.  In the **Authoring** navigation pane, expand **Management Pack Templates**, and then select **UNIX\/Linux Log File**.

4.  In the **UNIX\/Linux Log File Monitoring** pane, locate the template to change.

5.  Right\-click the template, and then select **Properties**.

6.  Enter the changes that you want, and then click **OK**.

### Viewing UNIX\/Linux Log File Data
There is no monitor or collected data for the **UNIX\/Linux Log File Monitoring** template. If a match is found in the specified log file, an alert is generated. You can view this alert in the **Active Alerts** view with the other alerts.

## See Also
[Creating Management Pack Templates](../Topic/Creating-Management-Pack-Templates.md)
[Watcher Nodes](../Topic/Watcher-Nodes.md)

