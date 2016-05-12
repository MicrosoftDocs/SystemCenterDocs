---
title: Running a Service Level Tracking Report
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b55aeec-869a-4072-89f5-0ae8e5a860ea
---
# Running a Service Level Tracking Report
You can create a report that shows how your application or group is performing in relation to the defined service level objectives. The report that is generated provides both high\-level information to give you a picture of the overall status at a glance, and detailed low\-level information to provide specific information on availability and performance metrics.

The Service Level Tracking Summary report shows the results for one or more service levels in comparison to the defined target objectives. From this report, you can examine a more detailed report, the State view, or the Service Level Agreement view.

Use the following steps to generate a Service Level Tracking Summary report.

### To generate a Service Level Tracking Summary report

1.  Open the Operations console with an account that is a member of the Operations Manager Administrators user role.

2.  In the Reporting workspace, click **Microsoft Service Level Report Library**.

3.  In the results pane, right\-click **Service Level Tracking Summary Report**, and then click **Open**.

4.  Click **Add SLA**.

5.  In **SLA Name**, type the name of the defined service level and then click **Search**.

6.  Select the service level, and then click **Add**.

7.  Click **OK** to close the **Add SLA** window.

8.  Define the data period for the report. You can select the following options:

    -   **Data aggregation**

    -   **Day range**

    -   **Time range**

9. Under **Report Fields**, select the fields that you want to include in the report. The fields that are available depend on the day and time range selection. For example, if you have specified a day range of Thursday to Wednesday, you do not have the option to include the **Last 30 Days** field.

10. Click **Run** to generate the report.

## See Also
[Defining a Service Level Objective Against a Group](Defining-a-Service-Level-Objective-Against-a-Group.md)
[Defining a Service Level Objective Against an Application](Defining-a-Service-Level-Objective-Against-an-Application.md)
[Monitoring Service Level Objectives by Using Operations Manager](Monitoring-Service-Level-Objectives-by-Using-Operations-Manager.md)


