---
title: How to Create Reports in Operations Manager
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to Create Reports in Operations Manager

>Applies To: System Center 2016 - Operations Manager

Operations Manager includes a number of reports when you install a management group, to help you review the operational telemetry and configuration information to help troubleshoot issues or problems, review the day-to-day health of your IT services, and make decisions that drive changes in capacity planning or service operations of the service.  
  
## Operational Data report

The Microsoft Customer Experience Improvement Program (CEIP) collects information about how you use Microsoft programs and about some of the issues you might encounter. Microsoft uses this information to improve the products and features you use most often and to help solve issues. Participation in the program is strictly voluntary.  
  
During setup of Operations Manager Reporting, on the **Operational Data Reports** page, you had the option to join CEIP. If you elected to join CEIP, Operations Manager Reporting collects information about your installation and sends reports to Microsoft on a weekly basis. You can view the contents of these Operational Data Reports by creating a Microsoft ODR Report.  

### Create an Operational Data report
  
1.  Log on to the computer with an account that is a member of the Operations Manager Report Operators role.  
  
2.  In the Operations console, click **Reporting**.  
  
3.  In the **Reporting** workspace, expand **Reporting**, and then click **Microsoft ODR Report Library**.  
  
4.  In the **Reports** pane, right-click one of the reports (for example, **Management Packs**), and then click **Open**.  
  
5.  In the **Report** view, in the **Parameter** area, click the down arrow in the **From** box, point to **This week**, and then click **Sunday**.  
  
6.  Click the down arrow in the **To** box, point to **This week**, and then click **Saturday**.  
  
7.  Click **Run** to display the ODR Report.  
  
8.  Click **Close** to close the report.  

## Create an Event Analysis report

Use the following procedure to create an event analysis report.  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Monitoring**.  
  
3.  In the **Monitoring** workspace, expand **Monitoring**, and then click **Windows Computers**.  
  
4.  In the **Windows Computers** pane, click a row containing a Health Service instance.  
  
5.  In the **Tasks** pane, under **Report Tasks**, click **Event Analysis**.  
  
6.  In the **Reporting Parameter** area, click the down arrow in the **From** box, and then click **Yesterday**.  
  
    > [!NOTE]  
    > You can further specify the timeframe for the report in the additional options in the Reporting Parameter area.  
  
7.  In the **Reporting Parameter** area, under **Monitoring Object**, click **Add**.  
  
8.  In the **Add Object** dialog box, in the **Object Name** list, click the down arrow, and then click **Begins with**.  
  
9. In the **Object name** text box, type the computer name for the computer you selected in step 4, and then click **Search**.  
  
10. In the **Available items** list, click the computer with the **Type** of **Health Service**, click **Add**, and then click **OK**.  
  
11. In the **Reporting Parameter** area, in the **Monitoring Object** list, click the entry that is not of the type **Health Service**, and then click **Remove**.  
  
12. Click **Run** to display the **Event Analysis Report**.  
  
13. Click **Close** to close the report.  

## Availability report

The following procedure is an example of how you create an availability report for a managed computer. The procedure presented here is applicable to creating other types of availability reports. In this example procedure, you generate a report for the entire week.  
  
> [!NOTE]  
> Operations Manager Reporting must be installed before you can run an Availability report.  
  
The availability report provides the following information about the selected computers:  
  
-   **Down** - computer state is critical (red)  
  
-   **Up** - computer state is healthy (green)  
  
-   **Yellow** - computer state is warning (yellow)  
  
-   **Unmonitored** - computer or monitor did not exist during reporting period  
  
-   **Monitor disabled** - monitor has been disabled, such as by using an override  
  
-   **Monitoring unavailable** - the System Center Management Health service monitoring the computer is unavailable  
  
-   **Planned/unplanned maintenance** - computer is in maintenance mode; overrides all other states      

### Create an Availability report
  
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


## Alerts report

An alerts report summarizes alerts that have occurred on a managed entity. The following procedure is an example of how you create an alerts report for a managed computer. The procedure presented here is applicable to creating other types of alerts reports. In this example procedure, you generate a report for the previous 24-hour period.  
  
> [!NOTE]  
> Operations Manager Reporting must be installed before you can run an alerts report.  
  
### Create an Alerts report  
  
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

## Alert Logging Latency report

The following procedure is an example of how you create an alert logging latency report for a managed computer. An alert logging latency report shows you how much time it took from when an alert was generated until it was written into the Operations Manager database. An alert is not displayed in the Operations console until after it is written into the Operations Manager database. Alert latency can be a function of network delays in your environment.  
  
This information is useful when considering service level agreements (SLA). You might not want to commit to an SLA of 2 minutes if alerts take longer than that to get written into the Operations Manager database.  
  
> [!NOTE]  
> Operations Manager Reporting must be installed before you can run an alert logging latency report.  
  
### Create an Alert Logging Latency report  
  
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


## Next steps

- [How to Run, Save, and Export a Report](how-to-run-save-export-reports.md) walks you through how to preview your reports, save them with specific report parameters to minimize repeated entry of information or to simplify the experience for your report users, and how to export the report to different file formats.  

-  See [How to Configure and Modify Report Schedules](how-to-configure-modify-report-schedules.md) to learn how to schedule report delivery for reports available in Operations Manager.  