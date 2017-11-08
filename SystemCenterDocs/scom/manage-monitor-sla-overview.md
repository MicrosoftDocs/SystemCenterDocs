---
title:  Monitoring Service Level Objectives by Using Operations Manager
description: This article describes how to create a service level objective in the Operations Manager console to measure service availability.
author: mgoedtel
ms.author: magoedte
ms.manager: carmonm
ms.date: 11/28/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid:  c7f7aac4-41b4-4094-bad6-3a509ff71bba
---

# Monitoring service level objectives by using Operations Manager

To ensure that resources, such as applications and systems, are available and performing at acceptable levels, companies set goals for their service availability and response times. System Center Operations Manager provides the capability to monitor these service goals by tracking service level objectives.

Service level objectives are measurements to ensure that you are meeting defined service level commitments. In Operations Manager, you define a service level objective - the set of monitors that you need to track (such as performance or availability) - and then run reports against that service level objective to ensure that you are meeting your goals.

Using the information from these reports, you can identify any shortfalls between your service level objectives and your actual performance. This means that you are not only aware of problems, but also can track the relative business effect of these problems.

For example, if you have a group of servers running instances of Microsoft Exchange Server, which are critical to your internal e-mail network, you can define a service level objective that states that 95% of the servers must be available at all times. Then, you can generate a report that compares the actual availability of those servers against the service level objective.

You can also create dashboard views to track service level objectives.

## Define a service level objective for an application

You can define a service level objective (SLO) to establish the availability and performance goals for an application. In the following procedure, you create a service level objective against a distributed application, define a monitor SLO that is based on availability (99.9% up-time), and define a collection rule SLO that is based on a performance rule (80% average processor time).  

1.  Open the Operations console with an account that is a member of the Operations Manager Administrators user role.

2.  Click **Authoring**.

3.  In the navigation pane, expand **Management Pack Objects**, and then click **Service Level Tracking**.

4.  In the **Tasks** pane, click **Create**.

5.  In the **Service Level Tracking** dialog box, type a name for the service level that you are defining. For example, type **LOB Application 1**. Optionally, you can provide a description. Click **Next**.

6.  On the **Objects to Track** page, under **Targeted class**, click **Select**.

7.  In the **Select a Target Class** dialog box, select a class for the service level, such as **Distributed Application**, from the list in the text box. You can search for a class by typing its name into the **Look For** text box. Click **OK** to close the **Select a Target** dialog box.

8.  You can use the **Scope** option to specify the scope for the service level. The default selection is to use all objects of the targeted class.

9. Select the management pack that this service level will be saved in. You can use an existing management pack or create a new one.

10. Click **Next**.

11. On the **Service Level Objectives** page, click **Add**, and then click **Monitor state SLO** to create a new monitor. This monitor will track the availability of the application.

12. Define the state monitor as follows:

    1.  In the **Service level objective name** text box, type a name for the service level objective. For this scenario, type **Availability**.

    2.  From the **Monitor** drop-down list, choose the specific monitor that you want to use to measure the objective. For this scenario, choose **Availability**.

    3.  Using the **Service level objective goal (%)** spin box, provide the numerical measure for your objective. For example, select **99.990** to indicate that your goal is 99.99% availability.

    4.  You can refine what the monitor tracks to determine availability by selecting or clearing any of the following state criteria:

        -   **Unplanned maintenance**

        -   **Unmonitored**

        -   **Monitoring unavailable**

        -   **Monitor disabled**

        -   **Planned maintenance**

        -   **Warning**

13. Click **OK**.

14. On the **Service Level Objectives** page, click **Add**, and then click **Collection rule SLO** to create a new collection rule. This rule will track the performance of the application

15. Define the performance collection rule as follows:

    1.  In the **Service level objective name:** text box, type a name for the service level objective. For this scenario, type **Performance**.

    2.  Under **Targeted class**, click **Select** to open the **Select a Target Class** dialog box. Specify the target class for the rule from the list of targets in the text box. Note that this class must be contained in the distributed application. For this scenario, select the specific class the rule is targeted to, such as Windows Server 2008 Operating System.

    3.  Under **Performance collection rule**, click **Select** to open the **Select a Rule** dialog box. Specify the performance collection rule to use. For this scenario, choose **Collect Processor\ % Processor Time performance counter**, and then click **OK**.

    4.  Using one of the **Aggregation method** options, choose one of the following:

        -   Average

        -   Min

        -   Max

    5.  Use the **Service level objective goal** drop-down list to specify either **Less than** or **More than**, and enter a value in the adjacent text box. For this scenario, choose **Less Than** and **80**. This indicates that the performance goal is to never exceed 80% processor time.

    6.  Click **OK**.

16. On the **Service Level Objectives** page, click **Next**.

17. On the **Summary** page, review the settings, and then click **Finish**.

18. When the **Completion** page appears, click **Close**.

## Defining a service level objective against a group

You can configure a service level objective (SLO) against a group of computers to ensure their availability. In the following scenario, you create a service level that consists of a group of servers (Exchange Servers) and then define a service level objective of 99.99% availability.  
  
1.  Open the Operations console with an account that is a member of the Operations Manager Administrators user role.  
  
2.  Click **Authoring**.  
  
3.  In the navigation pane, expand **Management Pack Objects**, and then click **Service Level Tracking**.  
  
4.  In the **Tasks** pane, click **Create**.  
  
5.  In the **Service Level Tracking** dialog box, type a name for the service level that you are defining. For example, type **Exchange Servers**. Optionally, you can provide a description. Click **Next**.  
  
6.  On the **Objects to Track** page, under **Targeted class**, click **Select**.  
  
7.  In the **Select a Target Class** dialog box, select a class for the service level, such as **Operations Management Group**, from the list in the text box. You can search for a class by typing its name into the **Look for** text box. Click **OK** to close the **Select a Target** dialog box.  
  
8.  You can use the **Scope** options to specify the scope of the service level. The default selection is to use all objects of the targeted class.  
  
9. Select the management pack that this service level will be saved in. You can use an existing management pack or create a new one.  
  
10. Click **Next**.  
  
11. On the **Service Level Objectives** page, click **Add**, and then click **Monitor state SLO** to create a new monitor. This monitor will track the availability of the application.  
  
12. Define the state monitor as follows:  
  
    1.  In the **Service level objective name** text box, type a name for the service level objective. For this scenario, type **Availability**.  
  
    2.  From the **Monitor** drop-down list, choose the specific monitor that you want to use to measure the objective. For this scenario, choose **Availability**.  
  
    3.  For the **Service level objective goal**, provide the numerical measure for your objective. For example, select **99.990** to indicate that your goal is 99.99% availability.  
  
    4.  You can refine what the monitor tracks to determine availability by selecting or clearing any of the following state criteria:  
  
        -   **Unplanned maintenance**  
  
        -   **Unmonitored**  
  
        -   **Monitoring unavailable**  
  
        -   **Monitor disabled**  
  
        -   **Planned maintenance**  
  
        -   **Warning**  
  
    5.  Click **OK** to close the **Service Level Tracking** dialog box.  
  
13. On the **Service Level Objectives** page, click **Next**.  
  
14. On the **Summary** page, review the settings, and then click **Finish**.  
  
15. When the **Completion** page appears, click **Close**.  


After you create a service level objective, you can monitor it by using a Service Level Tracking dashboard view and the Service Level Tracking Report.


## Next steps

- See [Running a Service Level Tracking Report](manage-monitor-sla-reports.md), to view the service level objective over time to verify the organization is delivering against availability targets defined in your SLAs.    

- [Create a Service Level Dashboard](manage-monitor-sla-create-dashboard.md) to view the service level objective and verify the organization is delivering against availability targets defined in your SLAs.