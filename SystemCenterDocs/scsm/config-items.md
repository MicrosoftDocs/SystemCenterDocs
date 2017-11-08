---
title: Configuration items in Service Manager
description: Lean about configuration items in Service Manager.
manager: carmonm
ms.topic: article
author: bandersmsft
ms.author: banders
ms.prod: system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology: service-manager
ms.assetid: 7e6ab64c-c752-4cee-9057-e4b4413e571d
---

# Configuration items in System Center 2016 - Service Manager

Configuration items are a way to store information about services, computers, software, software updates, users and other undefined imported objects in the Service Manager database in Service Manager. You can then select configuration items when you submit forms, such as an incident form, a change request form, or a work item form.

A service is a special kind of configuration item that includes both technical and business data. It supports troubleshooting and impact analysis by showing critical dependencies, settings, and areas of responsibility to other configuration items. The key benefit of using services is that you can easily see when incidents affect configuration items because services are viewed as a map, or hierarchy, of items. A service also identifies service owners, key customers, and users. Because a service maps the relationships between configuration items and work items, you should use services to help manage work items.

You can use connectors to import a large number of configuration items from Active Directory Domain Services (AD DS), Configuration Manager, and Operations Manager, or you can manually create single CIs. You can also use the Operations Manager CI connector to import distributed applications in Operations Manager as a service.
> [!NOTE]
> When you open a view to display a large number of items - typically, more than 5,000 - the view can take a few minutes to display complete results.

## Manually create configuration items

You might have to create a configuration item to add computers that do not exist in Active Directory Domain Services (AD DS) and that are not managed by Configuration Manager to the Service Manager database.

Additionally, you might have to manually create a new user configuration item to be used in the **Affected User** box in incidents created by Operations Manager.

You can use the following procedures to manually create two computer configuration items. However, you can also use the same procedures to add software, printers, or software updates in Service Manager. After you add the two computers, you can identify them as a service.

### To manually create a computer configuration item

1.  In the Service Manager console, click **Configuration Items**.
2.  In the **Configuration Items** pane, expand **Configuration Items**, and then expand **Computers**.
3.  Click **All Windows Computers**. In the **Tasks** pane, under **Computers**, click **Create Computer**.
4.  In the form that appears, create a configuration item for a computer, such as **Exchange01.woodgrove.com**. On the **General**, **Software**, and **Related Items** tabs, enter information about the computer.
5.  Click **OK** to save the new configuration item.
6.  Repeat step 3 through step 5 to create a second computer, such as **Exchange02.woodgrove.com**.

### To manually create a user configuration item

1.  In the Service Manager console, click **Configuration Items**.
2.  In the **Configuration Items** pane, expand **Configuration Items**, and then click **Users**.
3.  In the **Tasks** pane, under **Users**, click **Create User**.
4.  On the **General** tab in the form, follow these steps:
    1.  In the **First Name** box, type a first name. For example, for the user account that will be used to populate the **Affected User** box for all incidents created by Operations Manager, type **OMAlert**.
    2.  In the **Last Name** box, type a last name. For example, for the user account that will be used to populate the **Affected User** box for all incidents created by Operations Manager, type **User**.
5.  On the **Notification** tab, click **Add**, and perform the following for each notification address that you want to add:
    1.  In the **User Notification** dialog box, in the **Notification address name** box, type a name you want to use for this notification.
    2.  In the **Notification address description** box, type a description you want to use for this notification.
    3.  In the **Delivery address for this notification channel** box, type the address you would use to deliver a notification. Typically, this would be an email address.
    4.  Click **OK**.

### To validate the manually created configuration item

-   Verify that the computer you added appears in the **Computers** pane.
-   Verify that the user you added appears in the **Users** pane.

## Create a service

You can use the following procedures to create a service in Service Manager. You should create and define business services that are critical to your enterprise. When you create a service, you create service configuration items, you define their business data, and you define relationships to other configuration items.

In the first procedure, you manually create a service from configuration items that are already present in Service Manager. This is a simple example and requires little other than a few existing configuration items.

In the second procedure, you view an edit a distributed application that was imported from Operations Manager. The prerequisites for this example can be very complex, depending on the distributed applications that you have created in Operations Manager. The following are high-level steps needed to import distributed applications from Operations Manager into Service Manager as services:

1.  In Operations Manager, export each management pack that contains a component for your distributed application. Ensure that you export all management pack dependencies.

    > [!NOTE]
    > You might need to download management packs or install them from the installation folder of your Operations Manager Root Management Server.

2.  In Service Manager, import the management pack that contains the distributed application and its dependences. A new, empty, business service should appear in Business Services in the Configuration Items workspace.
3.  Browse to **Administration** and then **Connectors** and ensure that you refresh the list of management packs. Then, synchronize the Operations Manager configuration items connector. When synchronization is complete, the service components appear in the **Configuration Items** workspace under the business service.

Generally, you should construct service maps that are 3-5 levels deep. Components of a service map should vary from 5-20 at each level. However, the total number of components should not exceed few hundred. This recommendation depends on the complexity of the service map, but keeping the number of components lower that a few hundred still provides reasonable response times, as you navigate throughout service map tree view. While the service map tree view expansion is still in progress, even for larger tree structures, the Service Manager console remains responsive. Service maps are not designed to handle a large number of components; as a result, we recommend that you keep your service map tree structures small.

### To manually create a service for an IT messaging application

1.  In the Service Manager console, click **Configuration Items**.
2.  In the **Configuration Items** pane, expand **Configuration Items**, and then expand **Business Services**.
3.  Click **All Business Services**, and then in the **Tasks** pane, under **Business Services**, click **Create Service**.
4.  In the form that appears, click the **General** tab. In the **Display Name** box, type the name of the service to create. For example, type **IT Messaging Service**.
5.  In the **Classification** list, select **E-mail and Communication**. In the **Owned By Organization** box, type the person or organization that provides the service. For example, type **Exchange Team**.
6.  In the **Priority** list, select **Medium**. In the **Status** list, select **In Service**.
7.  Next to the **Service owner** box, click the ellipsis button (**...**). Select the user who owns the service.
8.  Next to the **Service contacts** box, click **Add** to select and add users who are contacts for the service.
9. Next to the **Service customers** box, click **Add** to select and add users who are business unit customers of the service.
10. Next to the **Affected users** box, click **Add** to select and add users or groups who use the service.
11. Click the **Service Components** tab to define the items on which the service depends.
12. Click **Add Category**. In the **Choose Class** dialog box, select **Computers Group**, and then click **OK**.
13. Under **Service Components**, select **ComputersGroup**, and then click **Add Item**.
14. In the **Select Objects** dialog box, under **Filter by class**, select **Computer**. Next, select individual computers to add to the group, and then click **OK**. For example, add **Exchange01.woodgrove.com** and **Exchange02.woodgrove.com**.

    > [!NOTE]
    > You can select only one object at a time. Do not attempt to add multiple objects.

15. In the tree, click **Service Components**, and then click **Add Category**. In the **Choose Class** dialog box, select **Other Components Group**, and then click **OK**.
16. In the tree, select **OtherComponentsGroup**, and then click **Add Item**. In the **Select Objects** dialog box under **Filter by Class List**, select **Services**, and then select **Active Directory Topology Root**. Next, click **OK**.
17. Click the **Service Dependents** tab to define the items that use the service or that are external to the service. For example, define other configuration items or services that use the new service.
18. Click **OK** to save the new configuration item.

### To view and edit a distributed application that was imported from Operations Manager

1.  In the Service Manager console, click **Configuration Items**.
2.  In the **Configuration Items** pane, expand **Configuration Items**, expand **Business Services**, and then click **All Business Services**.
3.  In the **All Business Services** pane, click the distributed application that you created in Operations Manager.
4.  In the **Tasks** pane, under the title of the distributed application, click **Edit**.
5.  In the *Service Maps - DistributedApplicationName* dialog box, click the **Service Components** tab to view the items defined in the Operations Manager distributed application. Then, expand the **Service Components** tree three levels.
6.  Select any configuration item, and then click **Open** to view or edit its properties.

### To view dependent services

1.  In the Service Manager console, click **Configuration Items**.
2.  In the **Configuration Items** pane, expand **Configuration Items**, expand **Business Services**, and then click **All Business Services**.
3.  Select the **DistributedApplicationName**. In the **Tasks** pane, under **DistributedApplicationName**, click **Edit**.
4.  In the form that appears, click the **Service Dependents** tab. Services that use the new service are listed. For example, **IT Messaging Service** appears in the list.
5.  Click **OK**.

## Create a view for imported configuration items

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

![PowerShell symbol](./media/config-items/pssymbol.png)You can use Windows PowerShell commands to display views that are defined in Service Manager. For more information, see [Get-SCSMView](https://go.microsoft.com/fwlink/p/?LinkID=225344).

## Delete configuration items

Deleting configuration items is a two-step process, and only members of the Advanced Operators, Authors, and Administrators user roles can initiate the Delete process in Service Manager. The first step does not delete configuration items directly. Instead, this process changes the property values of a configuration item so that the item will only be displayed in a **Deleted Items** view. The state of the configuration item is changed from Active to Pending Delete. A Service Manager administrator can later log on and permanently delete the configuration item from the Service Manager database.


You can use the following procedures to initiate the deletion of a configuration item in Service Manager and validate the initiation of the deletion. Only users who are members of the Advanced Operators, Authors, or Administrators user role can initiate the deletion of a configuration item. Only users who are members of the Administrators user role can complete the deletion of a configuration item.

### To initiate the deletion of a configuration item

1.  Log on to a computer that hosts the Service Manager console by using a user account that is a member of the Advanced Operators, Authors, or Administrators user role.
2.  In the Service Manager console, click **Configuration Items**.
3.  In the **Configuration Items** pane, expand **Configuration Items**, expand **Computers**, and then click **All Windows Computers**.
4.  In the **All Windows Computers** pane, click the computer to be deleted.
5.  In the **Tasks** pane, under the name of the computer that you selected in the previous step, click **Delete**.
6.  In the **Delete Item** dialog box, confirm your selection, and then click **Yes**.

### To validate that the deletion of a configuration item has been initiated

1.  In the Service Manager console, click **View**, and then click **Refresh**. Or, press F5.
2.  Verify that the configuration item you selected is no longer displayed.

    > [!NOTE]
    > At this point, the configuration item has been moved to a **Deleted Item** view that is only available to members of the Administrator user role. An administrator must permanently delete the configuration item.

![PowerShell icon](./media/config-items/pssymbol.png) You can use Windows PowerShell commands to complete these tasks, as follows:

-   For information about how to use Windows PowerShell to initiate the deletion of a configuration item by updating the `PendingDelete` property value, see [Update-SCSMClassInstance](https://go.microsoft.com/fwlink/p/?LinkID=225420).
-   For information about how to use Windows PowerShell to retrieve items that have been marked for deletion in Service Manager, see [Get-SCSMDeleteditem](https://go.microsoft.com/fwlink/p/?LinkId=225322).


### Delete or restore a configuration item

After members of the Advanced Operators, Authors, or Administrators user roles have initiated the deletion of a configuration item, a Service Manager administrator can use the following procedures to either permanently delete the configuration item or to restore the original properties for this item. You may need to refresh the Service Manager console to update the list of configuration items.

#### To complete the deletion of a configuration item

1.  Log on to a computer that hosts the Service Manager console by using a user account that is a member of the Administrators user role.
2.  In the Service Manager console, click **Administration**.
3.  In the **Administration** pane, expand **Administration**, and then click **Deleted Items**.
4.  In the **Deleted Items** pane, click the configuration items that you want to permanently delete. You can use the CTRL or SHIFT keys to select multiple configuration items.
5.  In the **Tasks** pane, click **Remove Items**.

    > [!NOTE]
    > For this release, if you are logged in as an administrator, you will see three options in the **Tasks** pane under the name of the computer: **Delete**, **Remove Items**, and **Restore Items**. In the **Deleted Items** view, select only **Remove Items** or **Restore Items**.

6.  In the **System Center Service Manager** dialog box, make sure you selected the correct items, and then click **Yes**.

### To restore a configuration item

1.  Log on to a computer that hosts the Service Manager console by using a user account that is a member of the Administrators user role.
2.  In the Service Manager console, click **Administration**.
3.  In the **Administration** pane, expand **Administration**, and then click **Deleted Items**.
4.  In the **Deleted Items** pane, click the configuration items that you want to restore to the Service Manager database. You can use the CTRL or SHIFT keys to select multiple configuration items.
5.  In the **Tasks** pane, click **Restore Items**.

    > [!NOTE]
    > For this release, if you are logged in as an administrator, you will see three options in the **Tasks** pane under the name of the computer: **Delete**, **Remove Items**, and **Restore Items**. In the **Deleted Items** view, select only **Remove Items** or **Restore Items**.

6.  In the **Delete Item** dialog box, make sure that you selected the correct items, and then click **Yes**.

![PowerShell icon](./media/config-items/pssymbol.png) You can use Windows PowerShell commands to complete these tasks, as follows:

-   For information about how to use Windows PowerShell to permanently remove an instance of a configuration item object, see [Remove-SCSMClassInstance](https://go.microsoft.com/fwlink/p/?LinkID=225414).
-   For information about how to use Windows PowerShell to restore items that were previously marked for deletion in Service Manager, see [Restore-SCSMDeleteItem](https://go.microsoft.com/fwlink/p/?LinkID=225374).

## Update configuration items


You might want to associate a work item to apply a Microsoft Exchange Server service pack update to the service that represents the computers that are affected by the email incident. To accomplish this, you can update the service configuration item and then add the respective work item as a related item.

You can use the following procedures to add information, such as related work items or files, to configuration items in Service Manager. The procedures in this topic describe only how to add items, but you can follow similar steps to view or remove items.

For example, when you are troubleshooting an incident, you might discover that a relationship exists between two or more objects. A work item to apply an application service pack might be related to more than one configuration item. You might need to update the configuration items to reflect that relationship.

Similarly, work items such as incidents, problems, and change requests are often interrelated. Related work items share some commonality with each other or with a configuration item. When a work item affects a particular configuration item, they are linked.

### To add information to configuration items

1.  In the Service Manager console, click **Configuration Items**.
2.  In the **Configuration Items** pane, expand **Configuration Items**, and then expand **Computers**.
3.  Click **All Windows Computers**. In the **All Windows Computers** pane, double-click the computer to which you want to add information.
4.  In the computer form, click the **Related Items** tab.

##### To add related services, people, and configuration items

1.  In the **Configuration Items: Computers, Services, and People** area, click **Add**.
2.  In the **Select Objects** dialog box, select a class from the **Filter by class** list to narrow the choices available in the **Available objects** list.
3.  In the **Available objects** list, select the items that you want to add, and then click **Add**.
4.  Click **OK** to close the dialog box and to add the selected items.

##### To add related work items

1.  In the **Related work items** area, click **Add**.
2.  In the **Select Objects** dialog box, select a class from the **Filter by class** list to narrow the choices available in the **Available objects** list.
3.  In the **Available objects** list, select the work items that you want to add, and then click **Add**.
4.  Click **OK** to close the dialog box and to add the selected work items.

##### To attach files

1.  In the **Attached files** area, click **Add**.
2.  In the **Open** dialog box, select the file that you want to add, and then click **Open**.
3.  Do not attempt to open an attached file before you submit the form.

## Next steps

- [Configure incident management](incident-mgt.md) for configuration scenarios, incident settings, email incident support, and to create an incident template.
