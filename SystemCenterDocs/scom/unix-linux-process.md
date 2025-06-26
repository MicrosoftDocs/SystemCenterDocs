---
ms.assetid: d12f1b76-178f-4f30-a452-d47eb7fd5e3c
title: UNIX or Linux Process in Operations Manager Management Pack
description: This article provides an overview of UNIX or Linux process.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# UNIX or Linux process


The _UNIX/Linux Process Monitoring_ template lets you monitor that a particular process installed on an UNIX or Linux computer runs.

## Scenarios

The  **UNIX/Linux Process Monitoring**  template is useful for monitoring any application as monitoring processes is typically critical to the health of the application.

## Monitoring performed by the UNIX/Linux process monitoring template

The following table shows the monitoring activity that the  **UNIX/Linux Process Monitoring** template performs:

| Type | Description | When Enabled |
| --- | --- | --- |
| Monitors | Process Count is Outside of Range | Always enabled. |

## Wizard options

When you run the  **UNIX/Linux Process Monitoring**  template, you have to provide values for options in the following tables. Each table represents a single page in the wizard.

## General Options

The following options are available on the  **General Options**  page of the wizard:

| Option | Description |
| --- | --- |
| Name | The name used for the template. This is the name that is displayed in the Operations console. |
| Description | Optional description of the template. |
| Management Pack | Management pack to store the class and monitors that the template creates. If you create any additional monitors or rules that are using the process as a targeted process, you must store them in the same management pack. For more information about management packs, see [Select a Management Pack File](select-management-pack-file.md). |

## Process Monitoring Details

The following options are available on the  **Process Monitoring Details**  page of the wizard:

| Option | Description |
| --- | --- |
| Process name | The name of the process. You can use the  **Select a Process**  button to connect to a monitored UNIX/Linux computer and list current running processes in order to select a process by name. If you wish to target the monitor to only a single computer, you must use the  **Select a Process**  button to select a computer and process. |
| Computer Group | The name of the group of UNIX or Linux computers for the process to monitor. Select the  **Select a group**  button to select a group that is installed in your management group. If you have used the  **Select a Process**  button to select a running process from a computer, the monitor will be targeted to that computer. After using the  **Select a Process**  button to select a process, you can use the  **Select a Group**  button to target a group with the monitor for the selected process. |
| Alert Severity | The severity for the alert: Error, Warning, or Information. |
| Regular Expression to filter process arguments | An optional Regular expression to use in filtering processes by arguments. If this option is used, processes that match the provided process name will be additionally filtered by their arguments. Only processes with arguments that match the Regular expression will be evaluated by the monitor. This is useful to identify a process for a specific application when other applications on the system might use a process with the same name. The Regular expression is evaluated against a concatenated list of process arguments. |
| Expression Matching Results | If you use the  **Select a Process**  button to connect to a monitored computer and select a process by name, the list of all processes with the selected process name for that computer are shown in this field. When you provide a  **Regular expression to filter process arguments** the processes listed in this field are filtered so that you can preview the filtering by argument. |

## Process Template Settings

The following options are available on the  **Process Template Settings**  page of the wizard:

| Option | Description |
| --- | --- |
| Minimum number of instances | The minimum number of running instances of the monitored process. To alert if no instances of the process are running, check the box  **Generate an alert when the number of process instances is less than the specified value**, and input a value of 1. The number of process instances is calculated after filtering by process name and the optional Regular expression to filter process arguments. If the number of running instances is less than the provided value, an alert is generated. |
| Maximum number of instances | The maximum number of running instances of the monitored process. To alert if more than a specific number of instances of the process are running, check the box  **Generate an alert when the number of process instances is greater than the specified value**, and input the maximum threshold value. The number of process instances is calculated after filtering by process name and the optional Regular expression to filter process arguments. If the number of running instances is greater than the provided value, an alert is generated. |

## Additional monitoring

In addition to performing the specified monitoring, the  **UNIX/Linux Process Monitoring**  template creates a target class that you can use for additional monitors and rules. Any monitor or rule that uses this class as a target runs on any agent where the process is installed.

## Create and modify UNIX/Linux process monitoring templates

### Create an existing UNIX/Linux process monitoring template

To create a UNIX/Linux process monitoring template, follow these steps:

1. If you want to monitor a process on a group of computers, determine the targeted group for the monitor by using the following logic:

    - If you want to discover the process on all UNIX and Linux computers in the management group, you don't have to create a group. You can use the existing group **UNIX/Linux Computer Group**.

    - If you only want the process to be discovered on a certain group of computers, then either ensure that an appropriate group exists or create a one by using the procedure in [How to Create Groups in Operations Manager](/previous-versions/system-center/system-center-2012-R2/hh298605(v=sc.12)).

2. Start the  **Add Monitoring**  wizard.
3. On the  **Select Monitoring Type**  page, select  **UNIX/Linux Process Monitoring**, and select  **Next**.
4. On the  **General Properties**  page, in the  **Name**  and  **Description**  boxes, enter a name and optional description for this new template.
5. Select a management pack in which to save the monitor or select  **New**  to create a new management pack. For more information, see [Select a Management Pack File](select-management-pack-file.md).
6. Select  **Next**.
7. Select the  **Select a Process**  button.
8. Select the  **Browse**  button and select a computer that has the process installed, and select  **OK**.
9. In the  **Processes**  box, select the process to monitor.
10. Select an  **Alert Severity**.
11. Optionally, provide a Regular expression to filter the matched process list by process arguments, in the field  **Regular expression to filter process arguments**.
12. If you want to monitor the process on a group of computers, do the following:
    1. Select the  **Select a Group**  button.
    2. Select a group that contains the computers with the process, and select  **OK**.
13. Select  **Next**.
14. Check the appropriate boxes for  **Generate an alert when the number of process instances is less than the specified value**  and  **Generate an alert when the number of process instances is greater than the specified value**.
15. Provide values for  **Minimum number of instances**  and  **Maximum number of instances**, if appropriate.
16. Select  **Next**.
17. Select  **Create**.

### Modify an existing UNIX/Linux process monitoring template

To modify an existing UNIX/Linux process monitoring template, follow these steps:

1. Open the Operations console with a user account that has Author credentials.
2. Open the  **Authoring**  workspace.
3. In the  **Authoring**  navigation pane, expand  **Management Pack Templates**, and then select  **UNIX/Linux Process Monitoring**.
4. In the  **UNIX/Linux Process Monitoring**  pane, locate the template to change.
5. Right-click the template, and then select  **Properties**.
6. Enter the changes that you want, and select  **OK**.



## View UNIX/Linux process monitors and collected data

### View the state of each monitor

To view the state of each monitor, follow these steps:

1. Select the  **UNIX/Linux Computers**  view.
2. In the  **UNIX/Linux Computers**  pane, right-click an object, select  **Open**, and select  **Health Explorer**.
3. Expand the  **Availability**  node, and select the  **Application/Service Availability Rollup**  node to view the individual process monitor.

## Related content

[Create Management Pack Templates](create-management-pack-templates.md).
