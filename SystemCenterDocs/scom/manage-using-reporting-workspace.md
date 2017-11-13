---
title: Using the Reporting Workspace in Operations Manager
description: This article describes how to use the Operations Manager Operations console to view and administer reports. 
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 11/10/2017
ms.custom: na
ms.prod: system-center-2016
ms.technology: operations-manager
ms.topic: article
ms.assetid: dbfffaab-d49c-42a5-bbb3-77cbeae9b841
---

# Using the Reporting Workspace in Operations Manager
System Center - Operations Manager provides extensive reporting capabilities, including multiple report libraries that you can select from to customize reports for your specific requirements. Reports perform a query against the data warehouse database and return the results in an easy-to-read format.  
  
> [!IMPORTANT]  
> Users must be a member of the Report Operator Users role to run reports.  
  
## Reporting  
Reporting in the Reporting workspace contains all reports installed with Operations Manager, as well as those reports included in management packs that you have imported.  
  
The report library contains generic reports (for example, Availability and Configuration Changes reports). Generic reports have no specified context. The context for the report is defined in the parameter header, located at the top of the Report window.  For a list of reports included with Operations Manager, review [Operations Manager reports library](manage-reports-installed-during-setup.md).  
  
## Authored Reports  
Authored reports are based on existing reports from the report library. You configure a report with prepopulated parameters and then make it available to other users.  
  
After you run a report, click **File**, and then click **Publish** to publish the report with the configured parameters to **Authored Reports**.  
  
## Favorite Reports  
You can save configured reports to **Favorite Reports** to make them continually available to you and to save you the time of reconfiguring a report you run frequently.  
  
After you run a report, click **File**, and then click **Save to favorites** to save the report.  
  
## Scheduled Reports  
You can schedule configured reports to run on a one-time or recurring basis.  
  
After you run a report, click **File**, and then click **Schedule** to configure the report subscription. For more information, see [Scheduling Reports](manage-reports-config-modify-schedules.md).  
  
## Next steps

* Review [How to create reports in Operations Manager](manage-reports-create-reports.md) to learn how create reports for your operational needs. 
  
* [How to Run, Save, and Export a Report](manage-reports-run-save-export.md) walks you through how to preview your reports, save them with specific report parameters to minimize repeated entry of information or to simplify the experience for your report users, and how to export the report to different file formats. 