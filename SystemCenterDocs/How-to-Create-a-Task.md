---
title: How to Create a Task
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2634afdf-480f-45ee-8ef4-a491ce2add9f
robots: noindex,nofollow
---
# How to Create a Task
Use the following procedures in [!INCLUDE[smlong12](./Token/smlong12_md.md)] to create a task—for example, a task that you can use to open Event Viewer and view logs on a computer—and then validate the new task. Event Viewer displays the logs from the remote computer that is listed as a Configuration Item in the incident.

### To create a task

1.  In the [!INCLUDE[smcons](./Token/smcons_md.md)], click **Library**.

2.  On the **Library** pane, expand **Library**, and then select **Tasks.**

3.  On the **Tasks** pane, select **Create Task**.

4.  On the **Before You Begin** page, click **Next**.

5.  On the **General** page, do the following:

    1.  In the **Task name** box, type a name for the task. For example, type **Event Viewer**.

        > [!NOTE]
        > In this release, if you edit and change any of the properties of a task, you have to close and reopen the console before you can view the task.

    2.  Next to the **Target class** area, click the ellipsis button \(**…**\).

    3.  In the **Choose Class** dialog box, in the **Class** list, click **Incident**, and then click **OK**.

    4.  In the **Management pack** list, make sure that **Service Manager Incident Management Configuration Library** is selected, and then click **Next**.

        > [!NOTE]
        > In this release, if you select the option to create a new management pack, you have to close and reopen the console before you can view this task.

6.  On the **Display Task by Category** page, select the category where the task will be displayed. For example, select **Incident Management Folder Tasks**, and then click **Next**.

7.  On the **Command Line** page, do the following:

    1.  In the **Full path to command** box, type the full path of the command you want to run with this task. For example, type **%windir%\\system32\\eventvwr.exe**.

    2.  In the **Parameters** area, click **Insert Property**.

    3.  In the **Select Property** dialog box, in the **Related classes** list, expand **Incident**, and then click **Is Related to Configuration Item**.

    4.  In the **Available Properties** box, type **Computer Name**.

    5.  Under **Windows Computer**, click **NetBIOS Computer Name**, and then click **Add**.

    6.  Optionally, select **Log in action log when this task is run** to add information to the incident action log when the task runs, and then click **Next**.

8.  On the **Summary** page, click **Create**.

9. On the **Completion** page, observe that **The new task was created successfully** appears, and then click **Close**.

### To validate a new task

1.  In the [!INCLUDE[smcons](./Token/smcons_md.md)], click **Work Items**.

2.  In the **Work Items** pane, expand **Work Items**, expand **Incident Management**, and then click **All Incidents**.

3.  In the **All Incidents** pane, click an incident for which a computer name has been entered as a configuration item.

4.  In the **Tasks** pane, under the name of the incident you selected in the previous step, click **Event Viewer**.

5.  Notice that Event Viewer starts, and the events from the computer that are associated with the incident are displayed.

![](/Image/PSSymbol.gif)You can use the Get\-SCSMTask Windows PowerShell command to view [!INCLUDE[smshort](./Token/smshort_md.md)] tasks.

## See Also
[Using Service Manager Tasks to Troubleshoot Computer Problems](./Using-Service-Manager-Tasks-to-Troubleshoot-Computer-Problems.md)


