---
title: How to Enable Recovery and Diagnostic Tasks
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75de042b-04af-4947-ae8f-d4d77985cac9
---
# How to Enable Recovery and Diagnostic Tasks
Monitors in Operations Manager for System Center 2012 can do more than notify you of problems by sending an alert. Some monitors also provide diagnostic and recovery tasks to help investigate and resolve those problems.

A task is a script or other executable code that runs either on the computer running the Operations console or on the server, client, or device that is being managed. Tasks can potentially perform any kind of activity, including restarting a failed application and deleting files.

Monitors can have two kinds of tasks associated with them: diagnostic tasks that try to discover the cause of a problem or provide you with additional information to assist with that diagnosis, and recovery tasks that try to fix the problem.

Some monitors have diagnostic or recovery tasks that are disabled by default. You can enable any of these tasks that you want the monitor to run. For example, in the following image, you see that some recovery tasks for the **Health Service Heartbeat Failure** monitor are not configured to run automatically.

![](9c63e7e1-3af2-4c9a-8f33-eedba1d0501a)

### To enable a diagnostic or recovery task

1.  In the Operations console, in the **Authoring** workspace, right\-click a monitor and click **Properties**.

2.  Click the **Diagnostic and Recovery** tab.

3.  On the **Diagnostic and Recovery** tab, in the **Configure diagnostic tasks** or **Configure recovery tasks** section, ensure the desired task is selected and then click **Edit**.

4.  On the **Overrides** tab, click **Override**. You can choose to override this monitor for objects of a specific type or for all objects within a group. After you choose which group or object type to override, the **Override Properties** dialog box opens. For more information about applying an override, see [Using Classes and Groups for Overrides in Operations Manager](Using-Classes-and-Groups-for-Overrides-in-Operations-Manager.md).

5.  In the **Override\-controlled parameters** section, click **Enabled** and set the override value to **True**.

6.  Either select a management pack from the **Select destination management pack** list or create a new unsealed management pack by clicking **New**. For more information about selecting a destination management pack, see [Creating a Management Pack for Overrides](Creating-a-Management-Pack-for-Overrides.md).

7.  Click **OK**. Close the open properties windows.

## See Also
[Diagnostic and Recovery Tasks](Diagnostic-and-Recovery-Tasks.md)
[Using Classes and Groups for Overrides in Operations Manager](Using-Classes-and-Groups-for-Overrides-in-Operations-Manager.md)
[How to Override a Rule or Monitor](How-to-Override-a-Rule-or-Monitor.md)
[How to Enable or Disable a Rule or Monitor](How-to-Enable-or-Disable-a-Rule-or-Monitor.md)
[Using the Enforced Attribute in Overrides](Using-the-Enforced-Attribute-in-Overrides.md)


