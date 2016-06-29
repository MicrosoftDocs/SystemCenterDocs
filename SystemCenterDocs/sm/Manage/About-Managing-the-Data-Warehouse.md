---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  About Managing the Data Warehouse
ms.technology:  service-manager
ms.assetid:  8b67ae1f-e1e7-4e2e-8bf5-99f831f035b0
---

# About Managing the Data Warehouse

>Applies To: System Center 2016 Technical Preview - Service Manager

In Service Manager, there are seven data warehouse jobs that run at various times to maintain the data warehouse, as listed in the following table.

|Data warehouse job|Description|
|----------------------|---------------|
|MPSyncJob|This job synchronizes all the management packs from the Service Manager source. These management packs define the content of the data warehouse. This job starts to run as soon as you register the Service Manager management group, and it takes several hours to complete on its initial run.|
|DWMaintenance|This job performs data warehouse maintenance, such as indexing and updating statistics. This job will run automatically after the MPSyncJob has finished.|
|Entity (or Grooming)|Grooming functions typically involve activities on the data warehouse that remove data based on a configurable time period. **Note:** For this release of Service Manager, grooming functions are handled as a workflow. Settings for this job are not configurable.|
|Extract|This job retrieves data from the Service Manager database. This job queries the Service Manager database for the delta data from its last run and writes this new data into the DWStagingAndConfig database in the data warehouse. There are two extract jobs in Service Manager: one for the Service Manager management group and the other for the data warehouse management group.|
|Transform|This job takes the raw data from the staging area and does any cleansing, reformatting, and aggregation that is required to get it into the final format for reporting. This transformed data is written into the DWRepository database.|
|Load|This job queries the data from the DWRepository database and inserts it into the DWDatamart database. The DWDatamart is the database that is used for all end user reporting needs.|



In order to manage the data warehouse, which is primarily used by reporting, you must perform maintenance tasks on these jobs. For example, you can view their status, pause and resume, set a schedule, enable and disable schedules, and troubleshoot data warehouse jobs. You can perform all of these maintenance tasks by using Windows PowerShell cmdlets. In addition, you can perform some of these tasks through the Service Manager console.

During deployment, you registered the Service Manager management group as discussed in Register Service Manager Management Group in the Service Manager Deployment Guide. As a result of that action, management pack deployment started and MPSyncJob started. You should not start or resume any data warehouse jobs until MPSyncJob has finished, as shown in the **Data Warehouse Jobs** pane in the Service Manager console.

## Job Schedule and Frequency
The schedule for a job defines when a job starts. Frequency refers to how often the job runs after it has started. Regardless of schedule and frequency, a job does not run unless the schedule for that job has been enabled. Except for the Entity (Grooming) job, each job has a default scheduled start time, which is midnight. The following table lists the scheduled start time, frequency, and default schedule setting.

|Data warehouse job|Scheduled start time|Frequency|Enabled by default?|
|----------------------|------------------------|-------------|-----------------------|
|MPSyncJob|Midnight|Every hour|Yes|
|DWMaintenance|Midnight|Every hour|Yes|
|Extract|Midnight|Every 5 minutes|Yes|
|Transform|Midnight|Every 30 minutes|Yes|
|Load|Midnight|Every hour|Yes|

In this release of Service Manager, grooming functions are handled as a workflow. Settings for this job are not configurable.

## Windows PowerShell Cmdlets
The Service Manager Windows PowerShell module contains cmdlets that are used in this scenario to manage data warehouse functions on the server that hosts the data warehouse. You must run all Windows PowerShell cmdlets as an administrator. To view the Windows PowerShell Help, type the **get-help** command, followed by the name of the cmdlet for which you want help. For example, type `get-help Set-SCDWJobSchedule`. The following cmdlets are used in this scenario:

-   **Get-SCDWJobSchedule** Displays the schedule for a data warehouse job.

-   **Get-SCDWJob** Displays status for all recurring Service Manager data warehouse jobs.

-   **Get-SCDWMgmtGroup** Shows details for a management group that is registered with the data warehouse.

-   **Remove-SCDWMgmtGroup** Removes a management group from the data warehouse.

-   **Set-SCDWJobSchedule** Sets the schedule for data warehouse jobs.

-   **Enable-SCDWJobSchedule** Enables a data warehouse job schedule.

-   **Disable-SCDWJobSchedule** Disables a data warehouse job schedule. Job schedules are disabled by default.

## Getting Started with Data Warehouse Jobs
When you register with the Service Manager data warehouse, the MPSyncJob starts running. This job can take several hours to complete its initial run. When this job is complete, you can see two extract jobs listed in the Data Warehouse Jobs pane. One extract job is listed as **Extract_<data warehouse management group name\>**, and the other extract job is listed as **Extract_<Service Manager management group name\>**. When both of these extract jobs appear, you know that the initial run of the MPSyncJob is complete and that you can now proceed with the subsequent maintenance tasks.
