---
title: Troubleshoot computer problems with tasks
description: You can troubleshoot computer problems with Service Manager tasks.
ms.topic: article
author: jyothisuri
ms.author: jsuri
ms.service: system-center
keywords:
ms.date: 11/01/2024
ms.subservice: service-manager
ms.assetid: 7814be87-cbc7-42fe-a5c8-5a8720e3921c
ms.custom: UpdateFrequency2, engagement-fy24
---

# Troubleshoot computer problems with Service Manager tasks



If you want to view the logs on a remote computer that is exhibiting problems, you must first create a task that opens Event Viewer. Event Viewer reads logs from remote computers.

In Service Manager, administrators can create and use tasks to automate and simplify lengthy, complex, or repetitive processes. Operators typically use tasks to help troubleshoot user incidents. After creating a task, operators can run the task directly from the Service Manager console.

> [!IMPORTANT]
> To create a task, the logged-on user must have administrative credentials.

The Event Viewer task that you create will display logs from the computer that is identified as a configuration item in the incident. The help desk analyst can then select an incident in the Service Manager console and run this task for the computers that are related to the incident.

## Create a task

Use the following procedures in Service Manager to create a task—for example, a task that you can use to open Event Viewer and view logs on a computer—and then validate the new task. Event Viewer displays the logs from the remote computer that is listed as a Configuration Item in the incident.

To create a task, follow these steps:

1. In the Service Manager console, select **Library**.

2. On the **Library** pane, expand **Library**, and select **Tasks.**

3. On the **Tasks** pane, select **Create Task**.

4. On the **Before You Begin** page, select **Next**.

5. On the **General** page, do the following:

    1. In the **Task name** box, enter a name for the task. For example, enter **Event Viewer**.

        > [!NOTE]
        > In this release, if you edit and change any of the properties of a task, you've to close and reopen the console before you can view the task.

    2. Next to the **Target class** area, select the ellipsis button (**...**).

    3. In the **Choose Class** dialog, in the **Class** list, select **Incident**, and select **OK**.

    4. In the **Management pack** list, ensure that **Service Manager Incident Management Configuration Library** is selected, and select **Next**.

        > [!NOTE]
        > In this release, if you select the option to create a new management pack, you've to close and reopen the console before you can view this task.

6. On the **Display Task by Category** page, select the category where the task will be displayed. For example, select **Incident Management Folder Tasks**, and select **Next**.

7. On the **Command Line** page, do the following:

    1. In the **Full path to command** box, enter the full path of the command you want to run with this task. For example, enter **%windir%\system32\eventvwr.exe**.

    2. In the **Parameters** area, select **Insert Property**.

    3. In the **Select Property** dialog, in the **Related classes** list, expand **Incident**, and select **Is Related to Configuration Item**.

    4. In the **Available Properties** box, enter **Computer Name**.

    5. Under **Windows Computer**, select **NetBIOS Computer Name**, and select **Add**.

    6. Optionally, select **Log in action log when this task is run** to add information to the incident action log when the task runs, and select **Next**.

8. On the **Summary** page, select **Create**.

9. On the **Completion** page, observe that **The new task was created successfully** appears, and select **Close**.

### Validate a new task

1. In the Service Manager console, select **Work Items**.

2. In the **Work Items** pane, expand **Work Items**, expand **Incident Management**, and select **All Incidents**.

3. In the **All Incidents** pane, select an incident for which a computer name has been entered as a configuration item.

4. In the **Tasks** pane, under the name of the incident you selected in the previous step, select **Event Viewer**.

5. Notice that Event Viewer starts, and the events from the computer that are associated with the incident are displayed.

![Screenshot of the PowerShell symbol.](./media/troubleshoot-with-tasks/pssymbol.png)You can use the Get-SCSMTask Windows PowerShell command to view Service Manager tasks.

## Run a task from an incident view

Use the following procedure to run a task, such as the Ping task, from an Incident view in Service Manager.

To run a task from an Incident view, follow these steps:

1. In the Service Manager console, select **Work Items**, and then select any Incident Management view. Select an incident in the view, and notice that in the **Tasks** pane, under *Incident Name*, the **Ping Related Computer** task appears.

2. In the **Tasks** pane, select the task to run it. For example, **Ping Related Computer**. If a computer isn't associated with the incident, you must specify the name of the computer to run the task on. If more than one computer is associated with an incident, choose one computer to run the task on.

3. If the task logs actions into the action log, you can open the incident and view the action log to see the output that the task generated.

4. If the **Console Task Output - *Task Name*** box appears, verify the output generated by the task, and select **Close**.

## Next steps

- [Configure your preference for sharing diagnostic and usage data](ceip-settings.md).
