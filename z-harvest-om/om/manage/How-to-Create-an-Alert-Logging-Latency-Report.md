---
title: How to Create an Alert Logging Latency Report
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 735265d1-d19a-45ef-a8b5-50c4ed724c9c
author:mgoedtel
manager:cfreemanwa
---
# How to Create an Alert Logging Latency Report
The following procedure is an example of how you create an alert logging latency report for a managed computer. An alert logging latency report shows you how much time it took from when an alert was generated until it was written into the Operations Manager database. An alert is not displayed in the Operations console until after it is written into the Operations Manager database. Alert latency can be a function of network delays in your environment.  
  
This information is useful when considering service level agreements \(SLA\). You might not want to commit to an SLA of 2 minutes if alerts take longer than that to get written into the Operations Manager database.  
  
> [!NOTE]  
> Operations Manager&nbsp;Reporting must be installed before you can run an alert logging latency report.  
  
### To create an alert logging latency report  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Monitoring**.  
  
3.  In the **Monitoring** workspace, expand **Monitoring** and then click **Windows Computers**.  
  
4.  In the **Windows Computers** pane, click a row with a Health Service instance.  
  
5.  In the **Tasks** pane, under **Report Tasks**, click **Alert Logging Latency**.  
  
6.  In the **Parameter Area**, click the down arrow in the **From** box and then click **Yesterday**.  
  
    > [!NOTE]  
    > You can further specify the timeframe for the report in the additional options in the **Parameter Area**.  
  
7.  Click the down arrow on the **Threshold** list, and select the latency threshold you want to measure.  
  
8.  Click the down arrow on the **Aggregation Type** list, and click the value you want for this report.  
  
9. Click **Run** to display the **Alert Logging Latency Report**.  
  
10. Click **Close** to close the report.  
  
