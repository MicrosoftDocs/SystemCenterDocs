---
title: Defining a Service Level Objective Against an Application_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f81bcf09-8f38-4957-aa35-5db681cba79c
---
# Defining a Service Level Objective Against an Application_1
You can define a service level objective \(SLO\) to establish the availability and performance goals for an application. In the following procedure, you create a service level objective against a distributed application, define a monitor SLO that is based on availability \(99.9% up\-time\), and define a collection rule SLO that is based on a performance rule \(80% average processor time\).

### To define a service level objective for an application

1.  Open the Operations console with an account that is a member of the Operations Manager Administrators user role.

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

    2.  From the **Monitor** drop\-down list, choose the specific monitor that you want to use to measure the objective. For this scenario, choose **Availability**.

    3.  Using the **Service level objective goal \(%\)** spin box, provide the numerical measure for your objective. For example, select **99.990** to indicate that your goal is 99.99% availability.

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

    3.  Under **Performance collection rule**, click **Select** to open the **Select a Rule** dialog box. Specify the performance collection rule to use. For this scenario, choose **Collect Processor\\ % Processor Time performance counter**, and then click **OK**.

    4.  Using one of the **Aggregation method** options, choose one of the following:

        -   Average

        -   Min

        -   Max

    5.  Use the **Service level objective goal** drop\-down list to specify either **Less than** or **More than**, and enter a value in the adjacent text box. For this scenario, choose **Less Than** and **80**. This indicates that the performance goal is to never exceed 80% processor time.

    6.  Click **OK**.

16. On the **Service Level Objectives** page, click **Next**.

17. On the **Summary** page, review the settings, and then click **Finish**.

18. When the **Completion** page appears, click **Close**.

After you create a service level objective, you can monitor it by using a Service Level Tracking dashboard view and the Service Level Tracking Report.

## See Also
[Running a Service Level Tracking Report](./Running-a-Service-Level-Tracking-Report.md)
[Defining a Service Level Objective Against a Group](./Defining-a-Service-Level-Objective-Against-a-Group.md)
[Creating a Service Level Dashboard](./Creating-a-Service-Level-Dashboard.md)
[Monitoring Service Level Objectives by Using Operations Manager](./Monitoring-Service-Level-Objectives-by-Using-Operations-Manager.md)


