---
ms.assetid: 113f2b4e-8f48-43da-9f31-2a2bf1d78ec5
title: Run, Save, and Export a Report
description: This article describes how to run, save and export a report in Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
ms.update-cycle: 1095-days
---

# Run, save, and export a report



You can view a report in Operations Manager by selecting it, entering the required parameters, and executing it.  Once you run it, you can also choose to save the configuration to a linked report, which deploys that report with different settings. You can export a report to another file format, such as PowerPoint, Image, PDF, Microsoft Word, or Microsoft Excel for your reporting users.  

Before exporting or saving the report parameters, you must first run the report.


## Run a report from the Reporting pane  

Use the following procedure to run a report from the Reporting workspace. In this example, you'll run an availability report.  

1.  Sign in to the computer with an account that is a member of the Operations Manager Report Operators role.  

2.  In the Operations console, select **Reporting**.  

3.  In the **Reporting** workspace, expand **Reporting**, and select **Microsoft Generic Report Library**.  

4.  In the **Reports** pane, right-click one of the reports (for example, **Availability**) and select **Open**.  

5.  In the **Report** view, in the **Parameter** area, select the down arrow in the **From** box, point to **This week**, and select **Sunday**.  

6.  Select the down arrow in the **To** box, point to **This week**, and select **Saturday**.  

7.  Select **Use business hours**.  

    > [!NOTE]  
    > You can further specify the time frame for the report in the additional options in the **Parameter** area.  

8.  Select **Add Object**.  

9. In the **AddObject** dialog, in the **ObjectName** text box, enter the computer name for a computer that you want to report availability, and select **Search**.  

10. In the **Available items** list, select the computer you want to run a report for, select **Add**, and select **OK**.  

11. Select **Run** to display the Availability Report.  

12. For a more detailed report, such as a report showing a graph for every day, select the horizontal bar graph under the **Availability Tracker**.  

13. In the toolbar, select **View**, point to **GoTo**, and select **Back to Parent Report** to return to the original report.  

14. Select **Close** to close the report.  

## Save a report   

When you run a report, you can save the report to **Favorite Reports**, or you can save it into an existing management pack. A report saved to **Favorite Reports** is only visible to you. Saving a report to an unsealed management pack is useful if you need to share with report users that include a specific set of parameters.  

The following steps outline the procedure for saving a report to a management pack:  

1.  Run a report from the Generic Report Library or from another management pack, such as the SQL Server management pack. Specify the parameters you want to for the report and select **Run**.  

2.  When the report renders, validate that it contains the information you need.  

3.  On the **File** menu, select **Save to management pack**.  

4.  Follow the instructions in the wizard to save the report.  

After the wizard completes, the management pack is saved to Operations Manager and then later deployed to the report server and is made available for all the report operators.  

> [!NOTE]  
> Be aware of the following when saving reports:  
>   
> -   Reports can be saved to a management pack from **Favorite Reports**.  
> -   Reports can't be saved to a management pack from authored reports.  
>   
> Management packs can be exported and imported into other management groups and the reports will work only when these management groups share the same data warehouse.  
>   
> Only users who are members of the Report Operators group can save reports to management packs.  


## Export a report

After a report has been run, you can export the report into one of several formats supported by SQL Server Reporting Services. To learn about what formats are supported by SQL Server Reporting Services, review [Export Reports](/sql/reporting-services/report-builder/export-reports-report-builder-and-ssrs).

> [!NOTE]  
> Operations Manager Reporting must be installed before you can run a report.  

If you want to manage and distribute reports securely, you can export reports to Microsoft Windows SharePoint Services, which offers digital rights management. Consult your network security administrator.  

1.  After a report has been run, in the toolbar, select the **File** menu, point to **Export**, and select the format in which you want to export the file.  

2.  In the **Save As** dialog, select the folder where you want to save the report, and select **Save**.  


## Next steps

- Review the [Operations Manager Reports library](~/scom/manage-reports-installed-during-setup.md) to understand what reports are available to help you explore the operational data and configuration information in your management group and follow the [How to create reports in Operations Manager](~/scom/manage-reports-create-reports.md) to create reports for your operational needs.

- To learn how to schedule report delivery for reports available in Operations Manager, see [How to Schedule Reports](manage-reports-config-modify-schedules.md).  

- If you're having issues where reports aren't returning any data, review [How to Troubleshoot Reports that Return No Data](https://support.microsoft.com/kb/2573329).
