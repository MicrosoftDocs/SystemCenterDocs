---
title: How to Delete or Restore a Configuration Item
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 50aaadf6-5a73-42a8-9882-5cb5f6adc247
robots: noindex,nofollow
---
# How to Delete or Restore a Configuration Item
After members of the Advanced Operators, Authors, or Administrators user roles have initiated the deletion of a configuration item, a [!INCLUDE[smlong12](Token/smlong12_md.md)] administrator can use the following procedures to either permanently delete the configuration item or to restore the original properties for this item. You may need to refresh the [!INCLUDE[smcons](Token/smcons_md.md)] to update the list of configuration items.

### To complete the deletion of a configuration item

1.  Log on to a computer that hosts the [!INCLUDE[smcons](Token/smcons_md.md)] by using a user account that is a member of the Administrators user role.

2.  In the [!INCLUDE[smcons](Token/smcons_md.md)], click **Administration**.

3.  In the **Administration** pane, expand **Administration**, and then click **Deleted Items**.

4.  In the **Deleted Items** pane, click the configuration items that you want to permanently delete. You can use the CTRL or SHIFT keys to select multiple configuration items.

5.  In the **Tasks** pane, click **Remove Items**.

    > [!NOTE]
    > For this release, if you are logged in as an administrator, you will see three options in the **Tasks** pane under the name of the computer: **Delete**, **Remove Items**, and **Restore Items**. In the **Deleted Items** view, select only **Remove Items** or **Restore Items**.

6.  In the **System Center Service Manager** dialog box, make sure you selected the correct items, and then click **Yes**.

### To restore a configuration item

1.  Log on to a computer that hosts the [!INCLUDE[smcons](Token/smcons_md.md)] by using a user account that is a member of the Administrators user role.

2.  In the [!INCLUDE[smcons](Token/smcons_md.md)], click **Administration**.

3.  In the **Administration** pane, expand **Administration**, and then click **Deleted Items**.

4.  In the **Deleted Items** pane, click the configuration items that you want to restore to the [!INCLUDE[smshort](Token/smshort_md.md)] database. You can use the CTRL or SHIFT keys to select multiple configuration items.

5.  In the **Tasks** pane, click **Restore Items**.

    > [!NOTE]
    > For this release, if you are logged in as an administrator, you will see three options in the **Tasks** pane under the name of the computer: **Delete**, **Remove Items**, and **Restore Items**. In the **Deleted Items** view, select only **Remove Items** or **Restore Items**.

6.  In the **Delete Item** dialog box, make sure that you selected the correct items, and then click **Yes**.

![](Image/PSSymbol.gif)You can use Windows PowerShell commands to complete these tasks, as follows:

-   For information about how to use Windows PowerShell to permanently remove an instance of a configuration item object, see [Remove\-SCSMClassInstance](http://go.microsoft.com/fwlink/p/?LinkID=225414).

-   For information about how to use Windows PowerShell to restore items that were previously marked for deletion in Service Manager, see [Restore\-SCSMDeleteItem](http://go.microsoft.com/fwlink/p/?LinkID=225374).

## See Also
[How to Initiate the Deletion of a Configuration Item](How-to-Initiate-the-Deletion-of-a-Configuration-Item.md)


