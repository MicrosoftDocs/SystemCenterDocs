---
title: Use the Reporting Workspace in Operations Manager
title: Use the Reporting workspace in Operations Manager
description: This article describes how to use the Operations Manager Operations console to view and administer reports.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 03/31/2025
ms.date: 04/02/2025
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
ms.assetid: dbfffaab-d49c-42a5-bbb3-77cbeae9b841
---

# Use the Reporting Workspace in Operations Manager
# Use the Reporting workspace in Operations Manager




System Center Operations Manager provides extensive reporting capabilities, including multiple report libraries that you can select from to customize reports for your specific requirements. Reports perform a query against the data warehouse database and return the results in an easy-to-read format.  

> [!IMPORTANT]  
> Users must be a member of the Report Operator Users role to run reports. 

This article discusses the Reporting Workspace in Operations Manager.

## Reporting  
Reporting in the Reporting workspace contains all reports installed with Operations Manager, as well as those reports included in management packs that you've imported.  

The report library contains generic reports (for example, Availability and Configuration Changes reports). Generic reports have no specified context. The context for the report is defined in the parameter header, located at the top of the Report window. For a list of reports included with Operations Manager, see [Operations Manager reports library](manage-reports-installed-during-setup.md).  

## Authored reports  
Authored reports are based on the existing reports from the report library. You configure a report with prepopulated parameters, and then make it available to other users.  

After you run a report, select **File**, and select **Publish** to publish the report with the configured parameters to **Authored Reports**.  

## Schedule reports  
You can schedule configured reports to run on a one-time or recurring basis.  

After you run a report, select **File**, and select **Schedule** to configure the report subscription. For more information, see [Configure and modify report schedules](manage-reports-config-modify-schedules.md).

::: moniker range="=sc-om-2019"
> [!NOTE]
> - The following feature is applicable for 2019 UR2 and later.
> - This feature is available in Operations Manager 2012 web console, which is now supported in 2019 UR2.

::: moniker-end

::: moniker range=">=sc-om-2019"

## Favorite reports in Web console

In Operations Manager, you can run and view favorite reports under **Web Console** > **My Workspace**. For more information, see [Favorite reports in Web console](favorite-reports-web-console.md).

::: moniker-end

## Next steps

* Review [How to create reports in Operations Manager](manage-reports-create-reports.md) to learn how to reports for your operational needs.

* [How to Run, Save, and Export a Report](manage-reports-run-save-export.md) walks you through how to preview your reports, save them with specific report parameters to minimize repeated entry of information or to simplify the experience for your report users, and how to export the report to different file formats.
