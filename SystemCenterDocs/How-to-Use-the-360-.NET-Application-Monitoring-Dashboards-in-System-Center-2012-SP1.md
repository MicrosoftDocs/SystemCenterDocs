---
title: How to Use the 360 .NET Application Monitoring Dashboards in System Center 2012 SP1
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 640a17c9-2645-4992-aa2c-38619bbdc57d
---
# How to Use the 360 .NET Application Monitoring Dashboards in System Center 2012 SP1
[!INCLUDE[sc2012sp1notetopic](Token/sc2012sp1notetopic_md.md)]

### To open and use the Application Dashboard

1.  In [!INCLUDE[om12short](Token/om12short_md.md)], click the **Monitoring** button, click **Application Monitoring**, and then click **Applications**.

2.  To open the Application Dashboard, click the application you want to see details about.

    The 360 .NET Application Monitoring Dashboards show:

    -   A list of all applications configured to appear in the 360 .NET Application Monitoring Dashboards

    -   The current state of each 360 distributed application

    -   Aggregated Average Transaction Response Time \(in seconds\) Performance Data from Global Service Monitor

    -   Availability percentage for the last 24 hours represented as a score

    -   Aggregated % Performance events for the last 24 hours represented as a score. \(100 is a perfect score with no performance exceptions. This will be reduced as the % performance events are increased.\)

    -   Aggregated % Exception events represented as a score. \(100 is a perfect score with no exception events. This number will be reduced as the % exception events are increased.\)

    -   The history of these counters, each in a performance graph, for the selected interval

    -   SLA information. The default SLA thresholds can be changed. You can also add your own SLAs as long as they are targeted at the distributed application. These SLAs will also appear in the dashboard.

    You can also change the interval shown in the dashboard by clicking **Personalize**. The default is 24 hours.

    > [!NOTE]
    > Information, such as average response, availability, performance, and reliability in the Applications Dashboard is aggregated. Aggregate performance counters provide value since the application owner typically wants to know how their website is performing, not how the individual instances of the website are performing. Instance\-level detail is not required until troubleshooting begins.

### To open and use the Application Summary Dashboard

1.  The Application Summary Dashboard shows components and instances of applications, performance data, and active alerts. The data are not aggregated, so the Application Summary Dashboard is a useful tool for troubleshooting.

    To view an Application Summary Dashboard, click an application in the Applications Dashboard. **Application Summary Dashboard** appears in the right pane.

2.  To open the Application Summary Dashboard, click **Application Summary Dashboard**.


