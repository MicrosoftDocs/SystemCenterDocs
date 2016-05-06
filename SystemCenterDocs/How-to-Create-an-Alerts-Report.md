---
title: How to Create an Alerts Report
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f3803b7-2e75-44f0-9767-f081674771ab
---
# How to Create an Alerts Report
An alerts report summarizes alerts that have occurred on a managed entity. The following procedure is an example of how you create an alerts report for a managed computer. The procedure presented here is applicable to creating other types of alerts reports. In this example procedure, you generate a report for the previous 24\-hour period.

> [!NOTE]
> Operations Manager Reporting must be installed before you can run an alerts report.

### To create an alerts report

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Monitoring**.

3.  In the **Monitoring** workspace, expand **Monitoring**, and then click **Wndows Computers**.

4.  In the **Windows Computers** pane, click a row with a Health Service instance.

5.  In the **Tasks** pane, under **Report Tasks**, click **Alerts**.

6.  In the **Reporting Parameter** area, click the down arrow in the **From** box and then click **Yesterday**.

    > [!NOTE]
    > You can further specify the timeframe for the report in the additional options in the **Reporting Parameter** area.

7.  Click **Run** to display the **Alert Report**.

8.  Click **Close** to close the report.

