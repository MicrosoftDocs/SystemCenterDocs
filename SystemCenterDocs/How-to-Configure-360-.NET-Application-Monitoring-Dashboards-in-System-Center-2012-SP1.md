---
title: How to Configure 360 .NET Application Monitoring Dashboards in System Center 2012 SP1
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 04b25f28-302e-46b3-8948-f34656918764
---
# How to Configure 360 .NET Application Monitoring Dashboards in System Center 2012 SP1
[!INCLUDE[sc2012sp1notetopic](./Token/sc2012sp1notetopic_md.md)]

### To configure 360 .NET Application Monitoring Dashboards

1.  In [!INCLUDE[om12short](./Token/om12short_md.md)], click the **Authoring** button.

2.  Right\-click **Distributed Applications** and select **Create a new distributed application**. The **Distributed Application Designer** opens.

3.  In the **Distributed Application Designer**, choose a name for your distributed application and enter a description \(optional\). In the **Choose Distributed Application Template**, select the **.NET 3 Tier Application** template. In the **Save to a Management Pack** section, select an existing management pack or create a new management pack where your distributed application and its components will be saved. Click **OK**.

4.  In the **Distributed Application Designer**, you can drag and drop the discovered application instances and components you want to monitor and view on the Application Summary Dashboard. Headings in the **Objects** pane map to the boxes. The items you drag in should be in the context of what you previously configured for.NET Application Performance Monitoring, Web Application Availability, and Global Service Monitor.

    ![](/Image/360Dash_DistributedAppDesigner.jpg)

    To select components and instances of the distributed application that you want to view in the Application Summary Dashboard, in **Object Types**, click an object type, select the instances you want display in the Application Summary Dashboard, and then drag them to the matching component group in the main flow.

    > [!NOTE]
    > If you configured applications to monitor using 360 .NET Application Monitoring Dashboards, but do not see them in the Distributed Application Designer, you might need to allow more time for all of the applications you want to monitor to be discovered.

5.  For more information about distributed applications and the Distributed Application Designer, see [Distributed Applications](./Distributed-Applications.md).

### To change thresholds for SLAs

1.  To change thresholds for SLAs, in [!INCLUDE[om12short](./Token/om12short_md.md)] click the **Authoring** button, click **Management Pack Objects**, click **Service Level Tracking**, and then double\-click **Application Health SLA**.

2.  In the **Service Level Tracking** wizard, on the **Service Level Objectives** page, you can add, edit, or remove service level objectives, which define the performance thresholds or the states that you want to track for the selected targeted class, objects, or group. When you are done, click **Finish**.

    > [!NOTE]
    > You can also add SLAs and SLOs and they will display in the Application Dashboard automatically.

### To set the time range for data displayed in the dashboards

1.  To set a time range for the data displayed in the Applications Dashboard, click the round icon in the upper right corner and click **Personalize**. Set the time range for data collections and then click **Finish**.

2.  To set a time range for the data displayed in the Applications Summary Dashboard, click the round icon in the upper right corner and click **Personalize**. Set the time range for data collections and then click **Finish**.

### To personalize the Application Summary Dashboard

1.  To personalize the Application Summary Dashboard, hover over the section you want to modify, click the round icon above its upper right corner, and then click **Personalize**.

    > [!NOTE]
    > You can personalize the **Average Response Time\(s\) for Externals Tests**, **Average Response Time\(s\) for Component**, **Monitored Requests per Second for Component**, and the **Active Alerts** sections. The **Distributed Application**, **Components**, and **Instances** sections cannot be personalized.

2.  Select the display or chart preferences for the information you want the dashboard to display, and then click **Finish**.

### To select locations to display on the Average Response Time\(s\) for External Tests dashboard

1.  On the **Application Summary Dashboard**, in the **Average Response Time\(s\) for External Tests** section, the application components and locations you have configured to monitor from are listed and displayed on the chart. To change which application component and locations are displayed on the chart, select only the application component locations you want to see.

2.  The chart will update automatically.

### To synchronize active alerts in the Application Summary Dashboard with Team Foundation Server \(TFS\) work items

1.  Import the Team Foundation Server \(TFS\) Work Item Management Pack into [!INCLUDE[om12short](./Token/om12short_md.md)]. This management pack synchronizes [!INCLUDE[om12short](./Token/om12short_md.md)] alerts with TFS work items so alerts from [!INCLUDE[om12short](./Token/om12short_md.md)] can be sent directly to development where they can view and track it in Visual Studio and remain synchronized with the alert you see in [!INCLUDE[om12short](./Token/om12short_md.md)].

2.  When the management pack is imported, assign an alert to engineering and this will synchronize the alert with TFS automatically.


