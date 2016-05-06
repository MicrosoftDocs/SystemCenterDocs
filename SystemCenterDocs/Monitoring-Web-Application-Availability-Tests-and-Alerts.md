---
title: Monitoring Web Application Availability Tests and Alerts
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d786ccb2-6b49-4121-9f1b-21414f29dc95
---
# Monitoring Web Application Availability Tests and Alerts

### To view overall web application health

1.  To get a view of the general health of each application you are monitoring, in the [!INCLUDE[om12short](./Token/om12short_md.md)] console, in the navigation pane, click the **Monitoring** button, and then click **Application Monitoring**.

2.  Click **Web Application Availability Monitoring**, and then click **Web Applications State**. This is the best view to see the overall health of each application.

    The alert state for each application is displayed according to the alert configurations used when you set up the tests:

    -   Green\=Healthy

    -   Yellow\=Error

    -   Red\=Warning

3.  To see details about a particular application, double\-click the test to open the **Health Explorer**.

    The Health Explorer allows you to see the health states for each criterion, so you can pinpoint what caused the application to show an error or warning.

### To view alerts and alert details

1.  To see active alerts for the applications you are monitoring, in the [!INCLUDE[om12short](./Token/om12short_md.md)] console, in the navigation pane, click the **Monitoring** button, and then click **Application Monitoring**.

2.  Click **Web Application Availability Monitoring**, and then click **Active Alerts**. If there are alerts, you will see them listed in the **Active Alerts** pane. As with the application health, the alert state is displayed in the color according to your alert configurations.

3.  To see alert details, click the alert to see the **Alert Details** pane.

4.  To see more details about an alert, double\-click the alert to open the **Alert Properties** page.

    On the **Alert Properties** page **General** tab, you can reassign the alert, see the alert description, and change the alert status to **New** or, if you have resolved the issue, **Closed**. Use the **Previous** and **Next** buttons to scroll through the alerts for easy review. When you are finished viewing or changing properties, click **OK** to save your changes.

### To view data for individual URLs and locations

1.  To get a view of each test you configured in the Web Application Availability Monitoring template, in the [!INCLUDE[om12short](./Token/om12short_md.md)] console, in the navigation pane, click the **Monitoring** button, and then click **Application Monitoring**.

2.  Click **Web Application Availability Monitoring**, and then click **Test State**. If there are alerts, you will see them listed in the **Active Alerts** pane. As with the application health, the alert state is displayed in the color according to your alert configurations.

    > [!NOTE]
    > A test is one URL and one location.

3.  To see the details of a particular test, double\-click the test to open the **Health Explorer**.

    The Health Explorer allows you to see the health states for each criterion, so you can see in detail what caused the test to show an error or warning.


