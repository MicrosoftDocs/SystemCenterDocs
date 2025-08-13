---
ms.assetid: 7a8a492c-fede-4952-952a-6dec5b7be382
title: UNIX or Linux Log File in Operations Manager management pack
description: This article provides an overview of UNIX or Linux log file
author: jyothisuri
ms.author: jsuri
ms.date: 04/16/2025
ms.custom: engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# UNIX or Linux log file



The  **UNIX/Linux Log File Monitoring**  template lets you create an alert when a particular text is detected in a log file. This article provides an overview of UNIX or Linux log file.

## Scenarios

Use the  **UNIX/Linux Log File Monitoring**  template for any application that writes to a log file when a particular error occurs. You provide the path to the log file and the text that indicates an error, and an alert is created for you anytime that text is detected.

## Monitoring Performed by the UNIX/Linux Log File Monitoring Template

The following table shows the monitoring activity that the  **UNIX/Linux Log FileMonitoring** template performs.

| Type | Description | When Enabled |
| --- | --- | --- |
| Rule | Creates an alert when a specified text is detected. | Enabled |

## Wizard options

When you run the  **UNIX/Linux Log File Monitoring**  template, you have to provide values for the options in the following tables. Each table represents a single page in the wizard.

## General options

The following options are available on the  **General Options**  page of the wizard.

| Option | Description |
| --- | --- |
| Name | The name used for the template. This name is displayed in the Operations console. |
| Description | Optional description of the template. |
| Management Pack | Management pack file to store the rule that the template creates. For more information about management packs, see [Selecting a Management Pack File](select-management-pack-file.md). |

## Log File Details

The following options are available on the  **Log File Details**  page of the wizard.

| Option | Description |
| --- | --- |
| Computer | If you want to monitor a single computer, enter the name of the agent-managed UNIX or Linux computer with the log file to monitor. Select the  **Select a Computer**  button to select one of the agent-managed UNIX or Linux computers that are installed in your management group. |
| Computer group name | If you're going to monitor a group of computers, enter the name of the group of agent-managed UNIX or Linux computers with the log file to monitor. Select the  **Computer Group** button to select from the group in your management group. |
| Log file path | Complete path and name of the log file. |
| Expression | Regular expression of the text to detect. If you want to detect a simple string of characters, enter the string of characters. |

## Create and modify UNIX/Linux log file templates

To create a UNIX/Linux log file template, follow these steps:

1. If you want to monitor the log file on a group of computers, determine the target group for the monitor by using the following logic:

   - If you want to monitor the log file on all UNIX and Linux computers in the management group, you don't have to create a group. You can use the existing group **UNIX/Linux Computer Group**.

   - If you only want the log file to be monitored on a certain group of computers, either ensure that an appropriate group exists or create a new computer group by using the procedure in [How to Create Groups in Operations Manager](/previous-versions/system-center/system-center-2012-R2/hh298605(v=sc.12)).

2. Start the  **Add Monitoring**  wizard.
3. On the  **Select Monitoring Type**  page, select  **UNIX/Linux Log File Monitoring**, and select  **Next**.
4. On the  **General Properties**  page, in the  **Name**  and  **Description**  boxes, enter a name and description for this new template.
5. Select a management pack in which you want to save the template or select  **New**  to create a new management pack. For more information, see [Select a Management Pack File](select-management-pack-file.md).
6. If you want to monitor the log file on a single computer, do the following:
   - Click the  **Select a Computer**  button next to the  **Computer name**  box.
   - Select the computer to monitor, and select  **OK**.
7. If you want to monitor the log file on a group of computers, do the following:
   - Click the  **Select a Group**  button next to the  **Computer group name**  box.
   - Select the computer to monitor, and select  **OK**.
8. In the  **Log file path**  box, enter the path and name of the log file to monitor.
9. In the  **Expression**  box, enter the text to watch for, such as  **error**. You can enter a regular expression for more complex logic.
10. Optionally, select  **Test**  to open a new dialog to test Regular expression matching against sample text that you input.
11. Select a  **Run As Profile**  to use. The account associated with the target computer in this profile will be used to read the log file.
12. Select an  **Alert Severity**.
13. Select  **Next**.
14. Verify the summary information for the template, and select  **Create**.

### Modify an existing UNIX/Linux Log File template

To modify a UNIX/Linux log file template, follow these steps:

1. Open the Operations console with a user account that has Author credentials.
2. Open the  **Authoring**  workspace.
3. In the  **Authoring**  navigation pane, expand  **Management Pack Templates** , and then select  **UNIX/Linux Log File**.
4. In the  **UNIX/Linux Log File Monitoring**  pane, locate the template to change.
5. Right-click the template, and then select  **Properties**.
6. Enter the changes that you want, and select  **OK**.

## View UNIX/Linux log file data

There's no monitor or collected data for the  **UNIX/Linux Log File Monitoring**  template. If a match is found in the specified log file, an alert is generated. You can view this alert in the  **Active Alerts** view with the other alerts.

## Related content

- [Create Management Pack Templates](/previous-versions/system-center/system-center-2012-R2/hh563869%28v%3dsc.12%29).
- [Watcher Nodes](/previous-versions/system-center/system-center-2012-R2/hh457584%28v%3dsc.12%29).
