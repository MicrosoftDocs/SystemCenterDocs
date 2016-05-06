---
title: Defining a Service Level Objective Against a Group
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6fc3df4-50fc-4514-b54b-1257ebc4c0e6
---
# Defining a Service Level Objective Against a Group
You can configure a service level objective \(SLO\) against a group of computers to ensure their availability. In the following scenario, you create a service level that consists of a group of servers \(Exchange Servers\) and then define a service level objective of 99.99% availability.

### To define a service level objective against a group

1.  Open the Operations console with an account that is a member of the Operations Manager Administrators user role.

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

    2.  From the **Monitor** drop\-down list, choose the specific monitor that you want to use to measure the objective. For this scenario, choose **Availability**.

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

## See Also
[Running a Service Level Tracking Report](./Running-a-Service-Level-Tracking-Report.md)
[Defining a Service Level Objective Against an Application](./Defining-a-Service-Level-Objective-Against-an-Application.md)
[Creating a Service Level Dashboard](./Creating-a-Service-Level-Dashboard.md)
[Monitoring Service Level Objectives by Using Operations Manager](./Monitoring-Service-Level-Objectives-by-Using-Operations-Manager.md)


