---
title: How to Initiate the Deletion of a Configuration Item
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 05ccff66-55ac-4ea3-8334-c44d09fbadad
robots: noindex,nofollow
---
# How to Initiate the Deletion of a Configuration Item
You can use the following procedures to initiate the deletion of a configuration item in [!INCLUDE[smlong12](../Token/smlong12_md.md)] and validate the initiation of the deletion. Only users who are members of the Advanced Operators, Authors, or Administrators user role can initiate the deletion of a configuration item. Only users who are members of the Administrators user role can complete the deletion of a configuration item.

### To initiate the deletion of a configuration item

1.  Log on to a computer that hosts the [!INCLUDE[smcons](../Token/smcons_md.md)] by using a user account that is a member of the Advanced Operators, Authors, or Administrators user role.

2.  In the [!INCLUDE[smcons](../Token/smcons_md.md)], click **Configuration Items**.

3.  In the **Configuration Items** pane, expand **Configuration Items**, expand **Computers**, and then click **All Windows Computers**.

4.  In the **All Windows Computers** pane, click the computer to be deleted.

5.  In the **Tasks** pane, under the name of the computer that you selected in the previous step, click **Delete**.

6.  In the **Delete Item** dialog box, confirm your selection, and then click **Yes**.

### To validate that the deletion of a configuration item has been initiated

1.  In the [!INCLUDE[smcons](../Token/smcons_md.md)], click **View**, and then click **Refresh**. Or, press F5.

2.  Verify that the configuration item you selected is no longer displayed.

    > [!NOTE]
    > At this point, the configuration item has been moved to a **Deleted Item** view that is only available to members of the Administrator user role. An administrator must permanently delete the configuration item.

![](../Image/PSSymbol.gif)You can use Windows PowerShell commands to complete these tasks, as follows:

-   For information about how to use Windows PowerShell to initiate the deletion of a configuration item by updating the `PendingDelete` property value, see [Update\-SCSMClassInstance](http://go.microsoft.com/fwlink/p/?LinkID=225420).

-   For information about how to use Windows PowerShell to retrieve items that have been marked for deletion in Service Manager, see [Get\-SCSMDeleteditem](http://go.microsoft.com/fwlink/p/?LinkId=225322).

## See Also
[How to Delete or Restore a Configuration Item](../Topic/How-to-Delete-or-Restore-a-Configuration-Item.md)

