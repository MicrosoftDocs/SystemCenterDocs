---
ms.assetid: 15cffea3-2fac-4c35-b7a6-8a95634eaf18
title: How to Create Reports in Operations Manager
description: This article describes how to create a linked report in Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
ms.update-cycle: 1095-days
---

# How to create reports in Operations Manager



Operations Manager includes many reports when you install a management group, to help you review the operational telemetry and configuration information to help troubleshoot issues or problems, review the day-to-day health of your IT services, and make decisions that drive changes in capacity planning or service operations of the service.  

## Operational Data report

The Microsoft Customer Experience Improvement Program (CEIP) collects information about how you use Microsoft programs and about some of the issues you might encounter. Microsoft uses this information to improve the products and features you use most often and to help solve issues. Participation in the program is strictly voluntary.  

During setup of Operations Manager Reporting, on the **Operational Data Reports** page, you had the option to join CEIP. If you elected to join CEIP, Operations Manager Reporting collects information about your installation and sends reports to Microsoft on a weekly basis. You can view the contents of these Operational Data Reports by creating a Microsoft ODR Report.  

### Create an Operational Data report

1.  Sign in to the computer with an account that is a member of the Operations Manager Report Operators role.  

2.  In the Operations console, select **Reporting**.  

3.  In the **Reporting** workspace, expand **Reporting**, and select **Microsoft ODR Report Library**.  

4.  In the **Reports** pane, right-click one of the reports (for example, **Management Packs**), and select **Open**.  

5.  In the **Report** view, in the **Parameter** area, select the down arrow in the **From** box, point to **This week**, and select **Sunday**.  

6.  Select the down arrow in the **To** box, point to **This week**, and select **Saturday**.  

7.  Select **Run** to display the ODR Report.  

8.  Select **Close** to close the report.  

## Create an Event Analysis report

Use the following procedure to create an event analysis report.  

1.  Sign in to the computer with an account that is a member of the Operations Manager Administrators role.  

2.  In the Operations console, select **Monitoring**.  

3.  In the **Monitoring** workspace, expand **Monitoring**, and select **Windows Computers**.  

4.  In the **Windows Computers** pane, select a row containing a Health Service instance.  

5.  In the **Tasks** pane, under **Report Tasks**, select **Event Analysis**.  

6.  In the **Reporting Parameter** area, select the down arrow in the **From** box, and then select **Yesterday**.  

    > [!NOTE]  
    > You can further specify the time frame for the report in the additional options in the Reporting Parameter area.  

7.  In the **Reporting Parameter** area, under **Monitoring Object**, select **Add**.  

8.  In the **Add Object** dialog, in the **Object Name** list, select the down arrow, and select **Begins with**.  

9. In the **Object name** text box, enter the computer name for the computer you selected in step 4, and select **Search**.  

10. In the **Available items** list, click the computer with the **Type** of **Health Service**, select **Add**, and select **OK**.  

11. In the **Reporting Parameter** area, in the **Monitoring Object** list, select the entry that isn't of the type **Health Service**, and select **Remove**.  

12. Select **Run** to display the **Event Analysis Report**.  

13. Select **Close** to close the report.  

## Availability report

The following procedure is an example of how you create an availability report for a managed computer. The procedure presented here's applicable to creating other types of availability reports. In this example procedure, you generate a report for the entire week.  

> [!NOTE]  
> Operations Manager Reporting must be installed before you can run an Availability report.  

The availability report provides the following information about the selected computers:  

-   **Down** - computer state is critical (red)  

-   **Up** - computer state is healthy (green)  

-   **Yellow** - computer state is warning (yellow)  

-   **Unmonitored** - computer or monitor didn't exist during the reporting period  

-   **Monitor disabled** - monitor has been disabled, such as by using an override  

-   **Monitoring unavailable** - the System Center Management Health service monitoring the computer is unavailable  

-   **Planned/unplanned maintenance** - computer is in maintenance mode; overrides all other states

### Create an Availability report

1.  Sign in to the computer with an account that is a member of the Operations Manager Administrators role.  

2.  In the Operations console, select **Monitoring**.  

3.  In the **Monitoring** workspace, expand **Monitoring**, and select **Windows Computers**.  

4.  In the **Windows Computers** pane, select the row, or rows, that represents the computer for which you want to run an availability report.  

5.  In the **Tasks** pane, under **Report Tasks**, select **Availability**.  

6.  In the **Report** view, in the **Parameter** area, select the down arrow in the **From** box, point to **This week**, and select **Sunday**.  

7.  Select the down arrow in the **To** box, point to **This week** and select **Saturday**.  

8.  Select **Use business hours**.  

    > [!NOTE]  
    > You can further specify the time frame for the report in the additional options in the **Parameter** area.  

9. When you've specified the time frame for the report, select **Run** to display the Availability Report.  

10. For a more detailed report, such as a report showing a graph for every day, select the horizontal bar graph under **Availability Tracker**.  

11. In the tool bar, select **View**, point to **Go To**, and select **Back to Parent Report** to return to the original report.  

12. Select **Close** to close the report.


## Alerts report

An alerts report summarizes alerts that have occurred on a managed entity. The following procedure is an example of how you create an alerts report for a managed computer. The procedure presented here's applicable to creating other types of alerts reports. In this example procedure, you generate a report for the previous 24-hour period.  

> [!NOTE]  
> Operations Manager Reporting must be installed before you can run an alerts report.  

### Create an Alerts report  

1.  Sign in to the computer with an account that is a member of the Operations Manager Administrators role.  

2.  In the Operations console, select **Monitoring**.  

3.  In the **Monitoring** workspace, expand **Monitoring**, and select **Windows Computers**.  

4.  In the **Windows Computers** pane, select a row with a Health Service instance.  

5.  In the **Tasks** pane, under **Report Tasks**, select **Alerts**.  

6.  In the **Reporting Parameter** area, select the down arrow in the **From** box and then select **Yesterday**.  

    > [!NOTE]  
    > You can further specify the time frame for the report in the additional options in the **Reporting Parameter** area.  

7.  Select **Run** to display the **Alert Report**.  

8.  Select **Close** to close the report.  

## Alert Logging Latency report

The following procedure is an example of how you create an alert logging latency report for a managed computer. An alert logging latency report shows you how much time it took from when an alert was generated until it was written into the Operations Manager database. An alert isn't displayed in the Operations console until after it's written into the Operations Manager database. Alert latency can be a function of network delays in your environment.  

This information is useful when considering service level agreements (SLAs). You might not want to commit to an SLA of 2 minutes if alerts take longer than that to get written into the Operations Manager database.  

> [!NOTE]  
> Operations Manager Reporting must be installed before you can run an alert logging latency report.  

### Create an Alert Logging Latency report  

1.  Sign in to the computer with an account that is a member of the Operations Manager Administrators role.  

2.  In the Operations console, select **Monitoring**.  

3.  In the **Monitoring** workspace, expand **Monitoring** and select **Windows Computers**.  

4.  In the **Windows Computers** pane, select a row with a Health Service instance.  

5.  In the **Tasks** pane, under **Report Tasks**, select **Alert Logging Latency**.  

6.  In the **Parameter Area**, select the down arrow in the **From** box and then select **Yesterday**.  

    > [!NOTE]  
    > You can further specify the time frame for the report in the additional options in the **Parameter Area**.  

7.  Select the down arrow on the **Threshold** list, and select the latency threshold you want to measure.  

8.  Select the down arrow on the **Aggregation Type** list, and select the value you want for this report.  

9. Select **Run** to display the **Alert Logging Latency Report**.  

10. Select **Close** to close the report.  


## Next steps

- [How to Run, Save, and Export a Report](manage-reports-run-save-export.md) walks you through how to preview your reports, save them with specific report parameters to minimize repeated entry of information or to simplify the experience for your report users, and how to export the report to different file formats.  

-  See [How to Configure and Modify Report Schedules](manage-reports-config-modify-schedules.md) to learn how to schedule report delivery for reports available in Operations Manager.  
