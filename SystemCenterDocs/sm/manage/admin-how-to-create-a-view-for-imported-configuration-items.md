---
title: Create a view for imported configuration items
description: Describes how you can create a view for imported configuration items in Service Manager.
manager: carmonm
ms.topic: article
author: bandersmsft
ms.author: banders
ms.prod: system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology: service-manager
ms.assetid: 9507e47e-16d7-4621-a724-39aea32d847c
---

# Create a view for imported configuration items in Service Manager

>Applies To: System Center 2016 - Service Manager

You can use the following procedures in Service Manager to create a view for imported Microsoft SQL Server database configuration items and then view the items in a dynamically generated form.

You can view and edit items that were imported from a System Center Operations Manager configuration item (CI) connector. However, Service Manager does not have system-defined views or forms for some items. For example, Service Manager does not have a defined view for SQL Server databases, so you must manually create a view to see these configuration items. Although Service Manager does not have a predefined form for SQL Server databases or for many other objects that you might have imported, you can still view any configuration item in a dynamically generated form (if you created a view for those items).

Before you use these procedures, make sure that you import the SQL Server management packs for Operations Manager and for Service Manager. Although these procedures rely on SQL Server databases imported from Operations Manager, you can use the same steps to view other imported configuration items that do not have system-defined views or forms.

### To create a view for imported SQL Server database configuration items

1.  In the Service Manager console, click **Configuration Items**.

2.  In the **Configuration Items** pane, expand **Configuration Items**, and then click **All Windows Computers**.

3.  In the **Tasks** pane, under **Computers**, click **Create View**.

4.  In the **Create View** dialog box, on the **General** page, in the **Name** box, type a name for the new view. For example, type **SQL Server Databases**.

5.  In the **Description** box, enter a description of the view you are creating. For example, type **This view displays SQL Server databases from Operations Manager**.

6.  Expand the **Criteria** area. Next to **Search for objects of a specific class**, click **Browse**.

7.  In the **Select a Class** dialog box, in the **View** list, select **All basic classes**.

8.  In the **Search** box, type **SQL**, and then click the search button (blue magnifying glass).

9. In the **Class** list, select **SQL DB**, and then click **OK**.

10. Click the **Display** tab. In the **Columns to display** list, select **Database Name** and **Database Size (MB) String**, and then click **OK**.

11. Select the **SQL Server Databases** view to see the list of the imported SQL Server databases.

### To view and edit imported SQL Server database configuration items

1.  Select the **SQL Server Databases** view that you created, and then select any item in the list. Notice that the **Preview** pane shows detailed information about the selected item.

2.  Double-click any item in the list to view the item in a dynamically generated form.

3.  Optionally, you can edit various fields for the item in the same manner as you do for other configuration items.

4.  Optionally, you can perform actions in the **Tasks** list, in the same manner as you do for other configuration items.

5.  If you have made any changes to the item, click **OK**; otherwise, click **Cancel** to close the form.

![PowerShell symbol](../media/pssymbol.png)You can use Windows PowerShell commands to display views that are defined in Service Manager. For more information, see [Get-SCSMView](http://go.microsoft.com/fwlink/p/?LinkID=225344).
