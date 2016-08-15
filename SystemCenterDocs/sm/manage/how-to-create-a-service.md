---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to Create a Service
ms.technology:  service-manager
ms.assetid:  8715ed07-5eea-41cb-b5a8-4134b047b91b
---

# How to Create a Service

>Applies To: System Center 2016 Technical Preview - Service Manager

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
