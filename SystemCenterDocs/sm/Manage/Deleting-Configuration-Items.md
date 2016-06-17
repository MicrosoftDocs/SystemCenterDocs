---
title: Deleting Configuration Items
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8c69ac89-eb91-4a06-87f9-8e0c34120255
---
# Deleting Configuration Items
Deleting configuration items is a two\-step process, and only members of the Advanced Operators, Authors, and Administrators user roles can initiate the Delete process in Service Manager. The first step does not delete configuration items directly. Instead, this process changes the property values of a configuration item so that the item will only be displayed in a **Deleted Items** view. The state of the configuration item is changed from Active to Pending Delete. A [!INCLUDE[smshort](../../includes/smshort_md.md)] administrator can later log on and permanently delete the configuration item from the [!INCLUDE[smshort](../../includes/smshort_md.md)] database.

## How to Initiate the Deletion of a Configuration Item

You can use the following procedures to initiate the deletion of a configuration item in Serice Manager and validate the initiation of the deletion. Only users who are members of the Advanced Operators, Authors, or Administrators user role can initiate the deletion of a configuration item. Only users who are members of the Administrators user role can complete the deletion of a configuration item.

### To initiate the deletion of a configuration item

1.  Log on to a computer that hosts the [!INCLUDE[smcons](../../includes/smcons_md.md)] by using a user account that is a member of the Advanced Operators, Authors, or Administrators user role.

2.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Configuration Items**.

3.  In the **Configuration Items** pane, expand **Configuration Items**, expand **Computers**, and then click **All Windows Computers**.

4.  In the **All Windows Computers** pane, click the computer to be deleted.

5.  In the **Tasks** pane, under the name of the computer that you selected in the previous step, click **Delete**.

6.  In the **Delete Item** dialog box, confirm your selection, and then click **Yes**.

### To validate that the deletion of a configuration item has been initiated

1.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **View**, and then click **Refresh**. Or, press F5.

2.  Verify that the configuration item you selected is no longer displayed.

    > [!NOTE]
    > At this point, the configuration item has been moved to a **Deleted Item** view that is only available to members of the Administrator user role. An administrator must permanently delete the configuration item.

![PowerShell icon](../../media/pssymbol.png) You can use Windows PowerShell commands to complete these tasks, as follows:

-   For information about how to use Windows PowerShell to initiate the deletion of a configuration item by updating the `PendingDelete` property value, see [Update\-SCSMClassInstance](http://go.microsoft.com/fwlink/p/?LinkID=225420).

-   For information about how to use Windows PowerShell to retrieve items that have been marked for deletion in Service Manager, see [Get\-SCSMDeleteditem](http://go.microsoft.com/fwlink/p/?LinkId=225322).


## How to Delete or Restore a Configuration Item
After members of the Advanced Operators, Authors, or Administrators user roles have initiated the deletion of a configuration item, a Service Manager administrator can use the following procedures to either permanently delete the configuration item or to restore the original properties for this item. You may need to refresh the [!INCLUDE[smcons](../../includes/smcons_md.md)] to update the list of configuration items.

### To complete the deletion of a configuration item

1.  Log on to a computer that hosts the [!INCLUDE[smcons](../../includes/smcons_md.md)] by using a user account that is a member of the Administrators user role.

2.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Administration**.

3.  In the **Administration** pane, expand **Administration**, and then click **Deleted Items**.

4.  In the **Deleted Items** pane, click the configuration items that you want to permanently delete. You can use the CTRL or SHIFT keys to select multiple configuration items.

5.  In the **Tasks** pane, click **Remove Items**.

    > [!NOTE]
    > For this release, if you are logged in as an administrator, you will see three options in the **Tasks** pane under the name of the computer: **Delete**, **Remove Items**, and **Restore Items**. In the **Deleted Items** view, select only **Remove Items** or **Restore Items**.

6.  In the **System Center Service Manager** dialog box, make sure you selected the correct items, and then click **Yes**.

### To restore a configuration item

1.  Log on to a computer that hosts the [!INCLUDE[smcons](../../includes/smcons_md.md)] by using a user account that is a member of the Administrators user role.

2.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Administration**.

3.  In the **Administration** pane, expand **Administration**, and then click **Deleted Items**.

4.  In the **Deleted Items** pane, click the configuration items that you want to restore to the [!INCLUDE[smshort](../../includes/smshort_md.md)] database. You can use the CTRL or SHIFT keys to select multiple configuration items.

5.  In the **Tasks** pane, click **Restore Items**.

    > [!NOTE]
    > For this release, if you are logged in as an administrator, you will see three options in the **Tasks** pane under the name of the computer: **Delete**, **Remove Items**, and **Restore Items**. In the **Deleted Items** view, select only **Remove Items** or **Restore Items**.

6.  In the **Delete Item** dialog box, make sure that you selected the correct items, and then click **Yes**.

![PowerShell icon](../../media/pssymbol.png) You can use Windows PowerShell commands to complete these tasks, as follows:

-   For information about how to use Windows PowerShell to permanently remove an instance of a configuration item object, see [Remove\-SCSMClassInstance](http://go.microsoft.com/fwlink/p/?LinkID=225414).

-   For information about how to use Windows PowerShell to restore items that were previously marked for deletion in Service Manager, see [Restore\-SCSMDeleteItem](http://go.microsoft.com/fwlink/p/?LinkID=225374).
