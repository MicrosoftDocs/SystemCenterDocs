---
ms.assetid: 113f2b4e-8f48-43da-9f31-2a2bf1d78ec5
title: How to Run, Save, and Export a Report
description: This article describes how to run, save and export a report in Operations Manager 2016.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to run, save, and export a report

>Applies To: System Center 2016 - Operations Manager

You can view reports in Operations Manager by selecting it, entering the required parameters and executing it.  Once you run it, you can also choose to save the configuration to a linked report, which deploys that report with different settings.  You can export a report to another file format, such as PowerPoint, Image, PDF, Microsoft Word, or Microsoft Excel for your reporting users.  

Before exporting or saving the report parameters, you must first run the report.


## To run a report from the Reporting pane  

Use the following procedure to run a report from the Reporting workspace. In this example, you will run an availability report.  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Report Operators role.  
  
2.  In the Operations console, click **Reporting**.  
  
3.  In the **Reporting** workspace, expand **Reporting** and then click **Microsoft Generic Report Library**.  
  
4.  In the **Reports** pane, right\-click one of the reports \(for example, **Availability**\) and then click **Open**.  
  
5.  In the **Report** view, in the **Parameter** area, click the down arrow in the **From** box, point to **This week**, and then click **Sunday**.  
  
6.  Click the down arrow in the **To** box, point to **Thisweek** and then click **Saturday**.  
  
7.  Click **Use business hours**.  
  
    > [!NOTE]  
    > You can further specify the timeframe for the report in the additional options in the **Parameter** area.  
  
8.  Click **Add Object**.  
  
9. In the **AddObject** dialog box, in the **ObjectName** text box, type the computer name for a computer that you want to report availability, and then click **Search**.  
  
10. In the **Availableitems** list, click the computer you want to run a report for, click **Add**, and then click **OK**.  
  
11. Click **Run** to display the Availability Report.  
  
12. For a more detailed report, such as a report showing a graph for every day, click the horizontal bar graph under **Availability Tracker**.  
  
13. In the toolbar, click **View**, point to **GoTo**, and then click **Back to Parent Report** to return to the original report.  
  
14. Click **Close** to close the report.  

## How to save a report   

When you run a report, you can save the report to **Favorite Reports** or you can save a report into an existing management pack. A report saved to **Favorite Reports** is only visible to you. Saving a report to an unsealed management pack is useful if you need to share with report users that includes a specific set of parameters.  
  
The following steps outline the procedure for saving a report to a management pack:  
  
1.  Run a report from the Generic Report Library or from another management pack, such as the SQL Server management pack. Specify the parameters you want to for the report and click **Run**.  
  
2.  When the report renders, validate that it contains the information you need.  
  
3.  On the **File** menu, click **Save to management pack**.  
  
4.  Follow the instructions in the wizard to save the report.  
  
After the wizard completes, the management pack is saved to Operations Manager and then later deployed to the report server and is made available for all report operators.  
  
> [!NOTE]  
> Be aware of the following when saving reports:  
>   
> -   Reports can be saved to a management pack from **Favorite Reports**.  
> -   Reports cannot be saved to a management pack from authored reports.  
>   
> Management packs can be exported and imported into other management groups and the reports will work only when these management groups share the same data warehouse.  
>   
> Only users who are members of the  authorization can save reports to management packs.  


## How to export a Report

After a report has been run, you can export the report into one of several formats supported by SQL Server Reporting Services.  To learn about what formats are supported by SQL Server Reporting Services, please review [Export Reports](https://msdn.microsoft.com/library/dd239307.aspx)
  
> [!NOTE]  
> Operations Manager Reporting must be installed before you can run a report.  
  
If you want to manage and distribute reports securely, you can export reports to Microsoft Windows SharePoint Services, which offers digital rights management. Consult your network security administrator.  
  
1.  After a report has been run, in the toolbar, click the **File** menu, point to **Export**, and then click the format you want to export the file to.  
  
2.  In the **Save As** dialog box, select the folder where you want to save the report, and then click **Save**.  


## Next steps

- Review the [Operations Manager Reports library](manage-reports-installed-during-setup.md) to understand what reports are available to help you explore the operational data and configuration information in your management group and follow the [How to create reports in Operations Manager](manage-reports-create-reports.md) to create reports for your operational needs. 

- See [How to Schedule Reports](../om/manage/how-to-configure-modify-report-schedules.md) to learn how to schedule report delivery for reports available in Operations Manager.  

- If you are having issues where reports are not returning any data, review [How to Troubleshoot Reports that Return No Data](https://support.microsoft.com/kb/2573329).


  
