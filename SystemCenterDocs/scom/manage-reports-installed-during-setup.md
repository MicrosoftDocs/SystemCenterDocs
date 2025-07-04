---
ms.assetid: 90b8bc0b-1a4a-4273-a51a-a33142230d60
title: Operations Manager Reports Library
description: This article summarizes the default reports included with Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency2
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# Operations Manager reports library



System Center Operations Manager provides the reports described in the following tables. For more information on a report, in the **Reporting** workspace, click the report and view the **Report Details**. For information on reports that are provided by other management packs, see the respective management pack guides.  

> [!NOTE]  
> When you first install Operations Manager, it may take several minutes for all report libraries to appear in **Reporting**.  

## Microsoft Generic Report Library  

::: moniker range="=sc-om-2019"

>[!NOTE]
> Reports **Management pack history**, **Management pack objects**, and **Overrides tracking** are available from 2019 UR2 and later.

::: moniker-end


|Report|Description|  
|----------|---------------|  
|Alert Logging Latency|This report helps to isolate issues in monitoring with Operations Manager by showing the logging latency of an alert for selected objects over time.|  
|Alerts|This report shows alerts raised during the selected report duration and for given filter parameters for selected objects.|  
|Availability|This report shows the time in state for selected objects during the selected report duration. Time in state is summarized by default as per the objects' availability monitors.|  
|Configuration Changes|This report shows the changes in configuration for selected objects over time.|  
|Custom Configuration|This report shows configuration data filtered by all entered parameters.|  
|Custom Event|This report shows event data filtered by all selected parameters.|  
|Event Analysis|This report shows a table of events and a count by server filtered by all entered parameters.|  
|Health|This report shows the time in state for selected objects during the selected report duration. Time in state is summarized by default as per the objects' overall entity health.|  
|Most Common Alerts|This report shows the most common alerts raised during the selected report duration and for given filter parameters for selected objects.|  
|Most Common Events|This report shows the most common events raised during the selected report duration and for given filter parameters for selected objects.|  
|Overrides|This report shows overrides configured in or applied to selected management packs over time.|  
|Performance|This report shows selected objects and performance counter values graphically over time.|  
|Performance Detail|This report shows selected objects and performance counter values graphically over time.|  
|Performance Top Instances|This report shows the top or bottom **N** instances for selected objects and a specific performance counter rule.|  
|Management pack history |This report generates the list of all the management packs, which are either imported or deleted on any management server in your management group. You can filter the report by date, action and username.|  
| Management pack objects |This report tracks and generates the list of all management pack objects, which are newly created or deleted from the management server. This report also tracks edits on management pack objects such as renaming a group/monitor/rule or adding/deleting a member in the group etc.|  
|Overrides tracking |This report tracks the overrides in detail, and supports fields such as Management pack name, Object name, Object type, Affected Property, Old value, New value, Target of the object type and Date.|  

## Client Monitoring Views Library  

|Report|Description|  
|----------|---------------|  
|Top N Applications|This report shows the top **N** applications based on their crash count and provides details for each application.|  
|Top N Applications Growth and Resolution|This report shows the top **N** applications based on their growth percentile computed against two specified time intervals.|  
|Top N Error Groups|This report shows the top **N** error groups based on their crash count.|  
|Top N Error Groups Growth and Resolution|This report shows the top **N** error groups based on their growth percentile computed against two specified time intervals.|  

## Microsoft Data Warehouse Reports  

|Report|Description|  
|----------|---------------|  
|Data Warehouse Availability|This report shows the availability of the data warehouse components based on the monitor **Data Warehouse Connectivity and Processes State**.|  
|Data Warehouse Events|This report shows data warehouse\-related events to help determine data warehouse health.|  
|Data Warehouse Properties|This report shows data warehouse properties and grooming settings.|  

## Microsoft ODR Report Library  

|Report|Description|  
|----------|---------------|  
|Alerts Per Day|This report shows the number of alerts generated per day from each rule or monitor that alerted within the report period \(by default one week\).|  
|Instance Space|This report shows the number of instances of each class \(for example, Exchange Servers\) that are created in your management group.|  
|Management Group|This report shows the operating system version used in the Operations Manager infrastructure \(management servers\).|  
|Management Packs|This report shows the versions of each management pack that is installed in your environment. It also summarizes all the overrides you've defined in your environment, as well as custom rules and monitors you've authored.|  
|Most Common Alerts|This report shows the most common alerts generated within the report period \(by default one week\). It also shows this data by management pack.|  

## System Center Core Monitoring Reports  

|Report|Description|  
|----------|---------------|  
|Agent Counts by Date, Management Group and Version|This report shows detail information for agent accounts during specified time interval.|  
|Agents by Health State|This report shows lists of agents organized by health state.|  
|Data Volume by Management Pack|This report shows the volume of data generated by management packs. The purpose of this report is to provide insight into which management packs are driving the data volumes in your environment so that you can establish baselines and identify opportunities for tuning.&nbsp; From this report, you can obtain more specific details per management pack by clicking one of the counts cells in the table at the top of the report to open the Data Volume by Workflow and Instance report for the management packs.|  
|Data Volume by Workflow and Instance|This report shows the volume of data generated, organized by workflows \(discoveries, rules, monitors, etc.\), as well as by instances.|  

## Microsoft Service Level Report Library  

|Report|Description|  
|----------|---------------|  
|Service Level Tracking Summary Report|This report shows whether the configured Service Level Objectives \(SLOs\) met their respective goals, for selected service levels.|  

## Web Application Availability Monitoring Solutions Library  

|Report|Description|  
|----------|---------------|  
|Test Availability|This report shows availability reported by an individual test &nbsp;over time.|  
|Test Performance|This report shows selected objects and performance counter values over time to relate how well a web application has performed.|  
|Web Application Availability|This report shows how available the web application was.&nbsp; The web application availability is the rollup of all tests defined in your web application.|  

## Application Monitoring Reports  

|Report|Description|  
|----------|---------------|  
|Application Failure Analysis|This report provides detailed failure analysis for a selected application.|  
|Application Performance Analysis|This report provides detailed performance analysis for a selected application|  
|Application Status|This report provides daily, weekly, and monthly application status summaries.|  
|Problems Distribution Analysis|This report shows the distribution of performance, connectivity, security and code problems across all monitored applications, highlighting the applications that are most problematic.|  
|Summary Failure Analysis|This report provides a breakdown of problems by application.|  
|Summary Performance Analysis|This report provides a breakdown of performance violations by application.|  
|Summary User Analysis|This report highlights the application users who experience most of the problems.|  
|\(Client Side Monitoring\) Application AJAX Calls Analysis|This report provides detailed failure analysis for a selected application.|  
|\(Client Side Monitoring\) Application Analysis|This report provides an overview of activity, performance and exception statistics for a selected application.|  
|\(Client Side Monitoring\) Application Status|This report provides daily, weekly and monthly application status summaries.|  
|\(Client Side Monitoring\) Client Latency Distribution|This report provides an analysis of client side performance in relation to network latency.|  
|\(Client Side Monitoring\) Load Time Analysis Based on Subnet|This report provides an analysis of client side performance based on client subnets.|  
|\(Client Side Monitoring\) Summary Performance Analysis|This report provides an analysis of performance violations by application.|  
|\(Client Side Monitoring\) Summary Size Analysis|This report provides an analysis of content size across multiple applications and shows the correlation between content size and load time.|  
|\(Client Side Monitoring\) Summary User Analysis|This report highlights the application users who experience most of the problems.|  
|\(Problem Analysis Reports\) Application Activity Breakdown|This report shows application activity trends for a selected period in relation to an application's activity during a previous period and average application activity.|  
|\(Problem Analysis Reports\) Application Daily Activity|This report shows application activity trends for a selected day in relation to an application's activity during a previous period and average application activity.|  
|\(Problem Analysis Reports\) Application Failure Breakdown by Functionality|This report shows the list of application requests that experience most of the problems.|  
|\(Problem Analysis Reports\) Application Failure Breakdown by Resources|This report provides failure analysis for distributed applications based on the application components and external resource dependencies.|  
|\(Problem Analysis Reports\) Application Heavy Resources Analysis|This report provides performance analysis for distributed applications based on the application components and external resource dependencies.|  
|\(Problem Analysis Reports\) Application Slow Request Analysis|This report shows the breakdown of application performance violations based on application requests.|  
|\(Problem Analysis Reports\) Day of Week Utilization|This report shows application activity trends and application resource utilization trends for a selected period.|  
|\(Problem Analysis Reports\) Hour of Day Utilization|This report shows application activity trends and application resource utilization trends for a selected period.|  
|\(Problem Analysis Reports\) Utilization Trend|This report shows application activity trends and application resource utilization trends for a selected period.|  
|\(Resource Utilization Analysis\) Application CPU Utilization Analysis|This report highlights applications that have the heaviest CPU utilization and provides a breakdown of CPU utilization based on the servers which host the application.|  
|\(Resource Utilization Analysis\) Application IO Utilization Analysis|This report highlights applications that have the heaviest IO utilization and provides a breakdown of IO utilization based on the servers which host each application.|  
|\(Resource Utilization Analysis\) Application Memory Utilization Analysis|This report highlights applications that have the heaviest memory utilization and provides a breakdown of memory utilization based on the servers which host each application.|  
|\(Resource Utilization Analysis\) Application Request Utilization Analysis|This report provides an analysis of application based on the volume of processed requests.|  
|\(Resource Utilization Analysis\) Computer Application Load Analysis|This report provides an analysis of servers based on the volume of processed requests.|  
|\(Resource Utilization Analysis\) Computer CPU Utilization Analysis|This report highlights servers that have the heaviest CPU utilization and provides a breakdown of CPU utilization based on the monitored applications running on each server.|  
|\(Resource Utilization Analysis\) Computer IO Utilization Analysis|This report highlights servers that have the heaviest IO utilization and provides a breakdown of IO utilization by monitored applications running on each server.|  
|\(Resource Utilization Analysis\) Computer Memory Utilization Analysis|This report highlights servers that have the heaviest memory utilization and provides a breakdown of memory utilization based on the monitored applications running on each server.|  

::: moniker range="sc-om-2019"
>[!NOTE]
> With Operations Manager 2019 UR2, you can track the changes done in management packs using the *management pack history*, *management pack objects* and *Overrides tracking* reports. [Learn more](management-pack-change-tracking.md).

::: moniker-end


## Next steps

- Review [How to create reports in Operations Manager](~/scom/manage-reports-create-reports.md) to learn how create reports for your operational needs.

- [How to Run, Save, and Export a Report](manage-reports-run-save-export.md) walks you through how to preview your reports, save them with specific report parameters to minimize repeated entry of information or to simplify the experience for your report users, and how to export the report to different file formats.  

- See [How to Configure and Modify Report Schedules](manage-reports-config-modify-schedules.md) to learn how to schedule report delivery for reports available in Operations Manager.  
