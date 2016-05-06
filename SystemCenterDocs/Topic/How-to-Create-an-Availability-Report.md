---
title: How to Create an Availability Report
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed94a545-c245-4a52-a7fc-8f66b4ebbd67
---
# How to Create an Availability Report
The following procedure is an example of how you create an availability report for a managed computer. The procedure presented here is applicable to creating other types of availability reports. In this example procedure, you generate a report for the entire week.

> [!NOTE]
> Operations Manager Reporting must be installed before you can run an Availability report.

The availability report provides the following information about the selected computers:

-   **Down** – computer state is critical \(red\)

-   **Up** – computer state is healthy \(green\)

-   **Yellow** – computer state is warning \(yellow\)

-   **Unmonitored** – computer or monitor did not exist during reporting period

-   **Monitor disabled** – monitor has been disabled, such as by using an override

-   **Monitoring unavailable** – the System Center Management Health service monitoring the computer is unavailable

-   **Planned\/unplanned maintenance** – computer is in maintenance mode; overrides all other states

### To create an availability report

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Monitoring**.

3.  In the **Monitoring** workspace, expand **Monitoring**, and then click **Windows Computers**.

4.  In the **Windows Computers** pane, click the row, or rows, that represent the computer for which you want to run an availability report.

5.  In the **Tasks** pane, under **Report Tasks**, click **Availability**.

6.  In the **Report** view, in the **Parameter** area, click the down arrow in the **From** box, point to **This week**, and then click **Sunday**.

7.  Click the down arrow in the **To** box, point to **This week** and then click **Saturday**.

8.  Click **Use business hours**.

    > [!NOTE]
    > You can further specify the timeframe for the report in the additional options in the **Parameter** area.

9. When you have specified the timeframe for the report, click **Run** to display the Availability Report.

10. For a more detailed report, such as a report showing a graph for every day, click the horizontal bar graph under **Availability Tracker**.

11. In the tool bar, click **View**, point to **Go To**, and then click **Back to Parent Report** to return to the original report.

12. Click **Close** to close the report.

