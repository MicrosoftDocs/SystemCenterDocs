---
title: How to create and assign a servicing window in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 977826e7-4a33-4dba-8666-6b66bc751280
---
# How to create and assign a servicing window in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

Servicing windows provide a method for scheduling servicing outside Virtual Machine Manager (VMM). In VMM, you can associate a servicing window with individual hosts, virtual machines, or services. Before using other applications to schedule maintenance tasks, you can use Windows PowerShell scripts or custom applications to query the object and determines if it is currently in a servicing window. Servicing windows do not interfere with the regular use and functionality of VMM.

### To create a servicing window

1.  In the **Settings** workspace, on the **Home** tab, in the **Create** group, click **Create Servicing Window**.

2.  In the **New Servicing Window** dialog box, enter a name and optional description for the servicing window.

3.  In **Category**, enter or select the category of servicing window.

4.  In **Start time**, enter the date, time of day, and time zone for the maintenance window.

5.  In **Duration**, specify the number of hours or minutes in the servicing window.

6.  Under **Recurrence pattern**, select the frequency (**Daily**, **Weekly**, or **Monthly**), and then schedule the occurrences within that frequency.

    -   To configure a daily servicing window, click **Daily**. Then, either click **Every** and enter the number of days between servicing, or click **Every weekday** to configure daily servicing.

    -   To configure a weekly servicing window, click **Weekly**. In **Recur every**, enter a number to specify the number of weeks between servicing. For example, enter 2 to configure servicing every other week. Finally, in **weeks on**, select each day on which to perform servicing.

    -   To configure a monthly servicing window, click **Monthly**, and then use one of the following methods to configure the monthly servicing window.

        Click **Day**, enter a number to indicate which day of the month, and in **of every**, enter a number to indicate the number of months between servicing. For example, you might configure a servicing window to be performed on the first day (day 1) of each quarter (every 3 months).

        Click second option (beginning with **The**). Select the week of the month (**first**, **second**, **third**, **fourth**, or **last**). Select a day of the week. Then, in **of every**, specify the number of months between servicing. For example, you might specify the second Tuesday of every month (every 1 months).

7.  Click **OK** to save your servicing window.

    > [!NOTE]
    > On the **Home** tab, in the **Properties** group, click **Properties** to modify a servicing window.

After you save the new servicing window, you can view it by clicking the **Servicing Windows** node on the **Settings** pane.

Use the following procedure to add a servicing window to a host. You can perform the same procedure on a virtual.

### To add a servicing window to a host

1.  In the **Fabric** workspace, on the **Fabric** pane, expand **Servers**, expand **All Hosts**, and optionally navigate to the host group that contains the host.

2.  On the **Hosts** pane, click the host.

3.  On the **Host** tab, in the **Properties** group, click **Properties**.

    The host properties dialog box opens.

4.  On the **Servicing Windows** page, click **Manage**.

    The **Manage the list of Servicing Windows** dialog box opens.

5.  Under **Available servicing windows**, click the servicing window that you want to add to the host, and then click **Add**.

    The selected servicing window moves to the **Selected servicing windows** list.

6.  Click **OK** to add the servicing window and click **OK** again to save the updated host properties.

## See Also
[Performing maintenance tasks in VMM](Performing-maintenance-tasks-in-VMM.md)
[Managing fabric updates in VMM](Managing-fabric-updates-in-VMM.md)
[Maintaining resources with VMM](Maintaining-resources-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



