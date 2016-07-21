---
title: How to Suspend Monitoring Temporarily by Using Maintenance Mode
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c3f75892-10f6-4690-bb82-0180991005e4
author:mgoedtel
manager:cfreemanwa
---
# How to Suspend Monitoring Temporarily by Using Maintenance Mode
Maintenance mode, available from the **Monitoring** workspace of the Operations console in [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)], enables you to avoid any alerts or errors that might occur when a monitored object, such as a computer or distributed application, is taken offline for maintenance. Maintenance mode suspends the following features:  
  
-   Rules and monitors  
  
-   Notifications  
  
-   Automatic responses  
  
-   State changes  
  
-   New alerts  
  
Use the following procedure to place one or more monitored objects into maintenance mode.  
  
### To put a monitored object into maintenance mode  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Monitoring**.  
  
3.  In the **Monitoring** workspace, expand **Monitoring**, and then click **Windows Computers**.  
  
4.  In the **Windows Computers** pane, right\-click the computer that you want to place into maintenance mode, click **Maintenance Mode**, and then click **Start Maintenance Mode**. You can use ctrl\+click or shift\+click to select multiple computers to place into maintenance mode.  
  
5.  In the **Maintenance Mode Settings** dialog box, under **Apply to**, click **Selected objects only** if only the computer is to be placed into maintenance mode; otherwise, click **Selected objects and all their contained objects**.  
  
6.  Select **Planned** if this is a planned event; otherwise, leave it cleared.  
  
7.  In the **Category** list, click the appropriate maintenance category.  
  
8.  Under **Duration**, select and enter the **Number of minutes** or select and enter the **Specific end time**, and then click **OK**. A maintenance mode icon appears in the **Computers** pane, in the **Maintenance Mode** column for the computer you selected.  
  
    > [!NOTE]  
    > The minimum value for **Numberofminutes** is 5. The maximum value is 1,051,200 \(2 years\).  
  
### To edit maintenance mode settings for a monitored object  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Monitoring**.  
  
3.  In the **Monitoring** workspace, expand **Monitoring**, and then click **Windows Computers**.  
  
4.  Right\-click the computer in the **Windows Computers** pane whose settings you want to edit, click **Maintenance Mode**, and then click **Edit Maintenance Mode settings**.  
  
5.  In the **Maintenance Mode Settings** dialog box, edit the settings you want to change, and then click **OK**.  
  
### To stop maintenance mode on a monitored object  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Monitoring**.  
  
3.  In the **Monitoring** workspace, expand **Monitoring**, and then click **Windows Computers**.  
  
4.  In the **Windows Computers** pane, right\-click the computer that you want to take out of maintenance mode, click **Maintenance Mode**, and then click **Stop Maintenance Mode**.  
  
5.  In the **Maintenance Mode** dialog box, do the following:  
  
    -   If you selected **Selected objects and all their contained objects** when you placed the computer into maintenance mode, select **Remove contained objects** and then click **Yes**.  
  
    -   If you selected **Selected objects only**, clear **Remove contained objects** and then click **Yes**.  
  
6.  In the **Windows Computers** pane, the maintenance mode icon disappears from the **Maintenance Mode** column for the computer you selected.  
  
    > [!NOTE]  
    > Because [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] polls maintenance mode settings only once every&nbsp;5 minutes, there can be a delay in an object's scheduled removal from maintenance mode.  
  
## See Also  
[General Tasks in Operations Manager_1](../Topic/General%20Tasks%20in%20Operations%20Manager_1.md)  
[Managing Alerts](../../om/manage/Managing-Alerts.md)  
[Connecting Management Groups in Operations Manager](../../om/manage/Connecting-Management-Groups-in-Operations-Manager.md)  
[Creating and Managing Groups](../../om/manage/Creating-and-Managing-Groups.md)  
[Running Tasks in Operations Manager](../../om/manage/Running-Tasks-in-Operations-Manager.md)  
[How to Create a Resource Pool](../../om/manage/How-to-Create-a-Resource-Pool.md)  
[Managing Resource Pools for UNIX and Linux Computers](../../om/manage/Managing-Resource-Pools-for-UNIX-and-Linux-Computers.md)  
[Using Operations Manager Shell](../../om/manage/Using-Operations-Manager-Shell.md)  
  
