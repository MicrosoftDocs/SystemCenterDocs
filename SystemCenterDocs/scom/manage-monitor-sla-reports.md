---
title: Running a Service Level Tracking Report
description: This article describes how to use the Service Level Tracking report in Operations Manager to evaluate service levels against defined targets.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
ms.assetid: 4b55aeec-869a-4072-89f5-0ae8e5a860ea
---

# Running a service level tracking report



You can create a report that shows how your application or group is performing in relation to the defined service level objectives. The report that's generated provides both high-level information to give you a picture of the overall status at a glance, and detailed low-level information to provide specific information on the availability and performance metrics.  

The Service Level Tracking Summary report shows the results for one or more service levels in comparison to the defined target objectives. From this report, you can examine a more detailed report, the State view, or the Service Level Agreement view.  

Use the following steps to generate a Service Level Tracking Summary report.  

## To generate a Service Level Tracking Summary report  

1.  Open the Operations console with an account that is a member of the Operations Manager Administrators user role.  

2.  In the Reporting workspace, select **Microsoft Service Level Report Library**.  

3.  In the results pane, right-click **Service Level Tracking Summary Report**, and select **Open**.  

4.  Select **Add SLA**.  

5.  In **SLA Name**, enter the name of the defined service level and select **Search**.  

6.  Select the service level, and select **Add**.  

7.  Select **OK** to close the **Add SLA** window.  

8.  Define the data period for the report. You can select the following options:  

    -   **Data aggregation**  

    -   **Day range**  

    -   **Time range**  

9. Under **Report Fields**, select the fields that you want to include in the report. The fields that are available depend on the day and time range selection. For example, if you've specified a day range of Thursday to Wednesday, you don't have the option to include the **Last 30 Days** field.  

10. Select **Run** to generate the report.  

## Next steps

- Learn how to create a service level objective to measure service availability of an application or a set of grouped computers for your service level dashboard by reviewing [Monitoring Service Level Objectives by Using Operations Manager](manage-monitor-sla-overview.md).

- To view the service level objective and verify the organization is delivering against availability targets defined in your SLAs, see [Create a Service Level Dashboard](manage-monitor-sla-create-dashboard.md).
