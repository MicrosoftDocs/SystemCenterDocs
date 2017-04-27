---
title: Manage the data warehouse
description: Describes how to manage the Service Manager data warehouse.
manager: carmonm
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
author: bandersmsft
ms.author: banders
ms.prod: system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology: service-manager
ms.assetid: 855110b9-cd11-4e06-8139-b21518456215
---

# Manage the Service Manager data warehouse

>Applies To: System Center 2016 - Service Manager

In order to manage the data warehouse, which is primarily used by reporting, you must perform maintenance tasks on data warehouse jobs. For example, you can view their status, pause and resume, set a schedule, enable and disable schedules, and troubleshoot data warehouse jobs. You can perform all of these maintenance tasks by using Windows PowerShell cmdlets. In addition, you can perform some of these tasks through the Service Manager console.

During deployment, you registered the Service Manager management group as discussed in Register Service Manager Management Group in the Service Manager Deployment Guide. As a result of that action, management pack deployment started and MPSyncJob started. You should not start or resume any data warehouse jobs until MPSyncJob has finished, as shown in the **Data Warehouse Jobs** pane in the Service Manager console.

There are seven data warehouse jobs that run at various times to maintain the data warehouse, as listed in the following table.

|Data warehouse job|Description|
|----------------------|---------------|
|MPSyncJob|This job synchronizes all the management packs from the Service Manager source. These management packs define the content of the data warehouse. This job starts to run as soon as you register the Service Manager management group, and it takes several hours to complete on its initial run.|
|DWMaintenance|This job performs data warehouse maintenance, such as indexing and updating statistics. This job will run automatically after the MPSyncJob has finished.|
|Entity (or Grooming)|Grooming functions typically involve activities on the data warehouse that remove data based on a configurable time period. **Note:** For this release of Service Manager, grooming functions are handled as a workflow. Settings for this job are not configurable.|
|Extract|This job retrieves data from the Service Manager database. This job queries the Service Manager database for the delta data from its last run and writes this new data into the DWStagingAndConfig database in the data warehouse. There are two extract jobs in Service Manager: one for the Service Manager management group and the other for the data warehouse management group.|
|Transform|This job takes the raw data from the staging area and does any cleansing, reformatting, and aggregation that is required to get it into the final format for reporting. This transformed data is written into the DWRepository database.|
|Load|This job queries the data from the DWRepository database and inserts it into the DWDatamart database. The DWDatamart is the database that is used for all end user reporting needs.|


## Job schedule and frequency
The schedule for a job defines when a job starts. Frequency refers to how often the job runs after it has started. Regardless of schedule and frequency, a job does not run unless the schedule for that job has been enabled. Except for the Entity (Grooming) job, each job has a default scheduled start time, which is midnight. The following table lists the scheduled start time, frequency, and default schedule setting.

|Data warehouse job|Scheduled start time|Frequency|Enabled by default?|
|----------------------|------------------------|-------------|-----------------------|
|MPSyncJob|Midnight|Every hour|Yes|
|DWMaintenance|Midnight|Every hour|Yes|
|Extract|Midnight|Every 5 minutes|Yes|
|Transform|Midnight|Every 30 minutes|Yes|
|Load|Midnight|Every hour|Yes|

In this release of Service Manager, grooming functions are handled as a workflow. Settings for this job are not configurable.

## PowerShell cmdlets
The Service Manager Windows PowerShell module contains cmdlets that are used in this scenario to manage data warehouse functions on the server that hosts the data warehouse. You must run all Windows PowerShell cmdlets as an administrator. To view the Windows PowerShell Help, type the **get-help** command, followed by the name of the cmdlet for which you want help. For example, type `get-help Set-SCDWJobSchedule`. The following cmdlets are used in this scenario:

-   **Get-SCDWJobSchedule** Displays the schedule for a data warehouse job.

-   **Get-SCDWJob** Displays status for all recurring Service Manager data warehouse jobs.

-   **Get-SCDWMgmtGroup** Shows details for a management group that is registered with the data warehouse.

-   **Remove-SCDWMgmtGroup** Removes a management group from the data warehouse.

-   **Set-SCDWJobSchedule** Sets the schedule for data warehouse jobs.

-   **Enable-SCDWJobSchedule** Enables a data warehouse job schedule.

-   **Disable-SCDWJobSchedule** Disables a data warehouse job schedule. Job schedules are disabled by default.

## Get started with data warehouse jobs
When you register with the Service Manager data warehouse, the MPSyncJob starts running. This job can take several hours to complete its initial run. When this job is complete, you can see two extract jobs listed in the Data Warehouse Jobs pane. One extract job is listed as **Extract_*data warehouse management group name***, and the other extract job is listed as **Extract_*Service Manager management group name***. When both of these extract jobs appear, you know that the initial run of the MPSyncJob is complete and that you can now proceed with the subsequent maintenance tasks.

## Data warehouse module deployment

Data warehouse module deployment in Service Manager starts when a Service Manager management server is registered to a data warehouse management server. The following sections describe module parts, functions, and schedule.

### Management pack synchronization

Management pack synchronization is the process by which the data warehouse discovers what classes and relationships exist in source systems. This process is also referred to as MPSync. For every management pack that defines a class or relationship, the data warehouse creates extract job modules to retrieve the data for that class or relationship from the corresponding source. Such management packs and their associated jobs are synchronized between the systems.

Only sealed management packs, and their corresponding data, are synchronized into the data warehouse. If you alter a management pack, you must increase the version number and you cannot introduce any changes that might cause errors; otherwise, the management pack will fail to import. For example, you cannot remove classes, remove properties, or remove relationships. Similarly, you cannot change data types in unsupported ways. For example, you cannot modify a string property to become a numeric property.

By default, the MPSync Orchestration job runs every 30 minutes.

It is possible that multiple sources may refer to the same management pack. The version in the source system must be the same or higher version than that in the data warehouse, otherwise registration will fail.

It is possible to remove management packs from the data warehouse. However, keep the following points in mind:

1.  Removing management packs does not delete the data from the data warehouse as it does in the  Service Manager database; instead, the database view that users are granted access to is dropped.
2.  If you reimport a management pack after you have removed the corresponding management pack, the historical data is exposed once again.

    > [!NOTE]
    > Only sealed management packs are synchronized from Service Manager to the data warehouse. An exception to this is list items, also known as enumerations. Groups or queues are synchronized to the data warehouse, regardless of whether they are in a sealed or unsealed management pack.

Management packs that are imported from Service Manager are Service Manager-specific and data warehouse specific. The Service Manager management packs provide awareness of what the Service Manager database is structured like, and the data warehouse management packs drive the structure and processes of the data warehouse databases.

### Report deployment
The management pack synchronization process imports management packs from Service Manager, and it defines how those management packs shape the structure, move the data, and copy reports for the data warehouse and reporting. After those management packs are synchronized between Service Manager and the data warehouse, the data is retrieved and reports are deployed for user consumption.

Sequentially, report deployment occurs in the following process:

1.  After all identified management packs are synchronized with data warehouse, management pack synchronization triggers the report deployment workflow.
2.  Because the DWStagingandConfig database is the final destination of the management packs that have been synchronized, the deployment workflow queries the DWStagingandConfig database for any new or changed reports to deploy or any reports to remove.
3.  The deployment workflow then publishes any new or updated reports to the SQL Server Reporting Services (SSRS) server through the SSRS web services.
4.  SSRS stores the reports and appropriate metadata.
5.  Schema deployment workflow is triggered by management pack synchronization.
6.  Once again, information that causes schema changes is retrieved from the DWStagingandConfig database based on the newly synchronized management packs that are causing the changes.
7.  Schema changes are deployed to the DWRepository database.
8.  Any necessary changes to extract, transform, and load (ETL) modules are made to the DWStagingandConfig database.

Management packs that contain only Service Manager-specific information do not cause the deployment activities to execute. They are only be triggered for new data warehouse and reporting-specific elements.

### Understand the ETL processes

After the data warehouse schema and reports are deployed, the DWDataMart database is populated with actual data for reporting purposes. This is done by the ETL processes. These three processes each serve their own specific purpose:

-   **Extract** is designed specifically for processing large volumes of data from multiple sources, and it allows for moving data into an area that is built for manipulating the data.
-   **Transform** is designed for optimization of complex logic and integration operations. This process is where most of the ETL work occurs.
-   **Load** is designed for transferring the data that has already been processed into its target destination in a bulk manner.

One of the main reasons for having three different databases is so that you can optimize your hardware environment more easily. In high-volume environments, the DWStagingandConfig and DWRepository databases must be on computer hardware that is optimized for read/write I/O. However, the computer hardware hosting the DWDatamart database must be optimized for read I/O. With that difference in mind, you can separate the DWDatamart to a different server or drive from the DWStagingandConfig and DWRepository databases. However, the DWStagingandConfig and DWRepository databases must remain on the same server.

At a high level, ETL occurs in the processes described in the following sections. If you plan on authoring management packs that are used for custom reporting, you will probably need to know more about these processes in depth.

#### Extract

The extract process starts on a scheduled interval. Extract is the process that retrieves raw data from your online transaction processing system (OLTP) store, which in this case is the  Service Manager database.

1.  The extract process queries Service Manager for the delta data that has accumulated since the last time the extract process ran.
2.  The new data is written into the DWStagingandConfig database in the same basic form as it is in the Service Manager database.

#### Transform

The transform process starts on a scheduled interval. Transform is the process that moves the raw data from the DWStagingandConfig database. It also does any cleansing, reformatting, and aggregation that is required to alter the raw data into the final format for reporting. This transformed data is written into the DWRepository database.

#### Load

The load process starts on a scheduled interval. The load process queries for the data from the DWRepository database. The transformed data from DWRepository is inserted into the DWDatamart database. The DWDatamart is the database that is used for all end-user reporting needs.

## Service Manager data warehouse retention

By default, data is stored in the data warehouse for 3 years for fact tables and for an unlimited period for dimension and outrigger tables. However, you can modify the retention period if you want to retain data longer or groom it out more aggressively.

### Fact table retention settings
There are 2 two types of retention settings in the data warehouse:

-   Global - The global retention period for all fact tables in the database is set to 3 years by default, which any subsequently created fact tables use as their default retention setting.
-   Individual Fact - The granular retention period for each individual fact table, uses the global setting of 3 years, unless you modify them individually.

**Global**:
The default global retention period for data stored in the Service Manager data warehouse is 3 years, so all fact tables use 3 years as the default retention setting. Any subsequently-created fact tables use this setting when created for their individual retention setting.

**Individual Fact Tables**:
Individual fact tables inherit the global retention value when created, or you can customize them to a value that differs from the default global setting. You can configure the default individual fact tables that were created during installation, individually with a specific retention value as needed.

#### To view the retention period for default tables or specific tables

- Use the **Get-SCDWRetentionPeriod** PowerShell cmdlet to get the retention period for either a specific fact table within a specific data warehouse database or the default for fact tables within the database. See [Get-SCDWRetentionPeriod](https://technet.microsoft.com/en-us/library/hh541718(v=sc.20).aspx) for detailed descriptions of available parameters and example usage.

#### To set the retention period for default tables or specific tables

- Use the **Set-SCDWRetentionPeriod** PowerShell cmdlet to set the retention period for either a specific fact table within a specific data warehouse database or the default for fact tables within the database. See [Set-SCDWRetentionPeriod](https://technet.microsoft.com/en-us/library/hh541725(v=sc.20).aspx) for detailed descriptions of available parameters and example usage.

## Reimport previously removed management packs

During development and testing of management packs that contain reports that access data warehouse information, you might need to remove the management packs and then reimport them later. However, after a management pack is uninstalled from the data warehouse, if the new management pack contains the same dimension, fact, or cube name with a schema that is different from the original, you must delete the dimension or fact table from the DWRepository and DWDataMart databases manually and also delete any referencing cube from the SQL Server Analysis Services (SSAS) database.

In addition, if a dimension or fact is already referenced by an existing data cube, you must also delete the management pack that contains the data cube and the data cube itself before uninstalling the new management pack. Because Service Manager does not remove the dimension or fact table from the DataSourceView and because dimensions are not removed from SSAS database, you must manually delete information that a data cube references. In this situation, you should use SQL Server Management Studio to remove any custom data cube that you created with the management pack from the DWASDatabase before you reregister or reinstall an updated management pack.

In general, you should avoid having the same dimension, fact, and cube name in differing schemas. Service Manager does not support this condition.

## Enable or disable data warehouse job schedules

Use the following procedure to enable the schedule for the ETL jobs as needed; you can use this procedure to enable the schedule for any of the data warehouse jobs. By default, the schedules for the extract, transform, and load (ETL) jobs are enabled. In this release of Service Manger, you can enable the schedules only by using Windows PowerShell.

### To enable a schedule for a data warehouse job by using a Windows PowerShell cmdlet

1.  On the computer that hosts the data warehouse management server, click **Start**, point to **All Programs**, click **Microsoft System Center**, click **Service Manager 2016**, and click **Service Manager Shell**.
2.  At the Windows PowerShell prompt, type the following commands, and then press ENTER after each command:

    ```
    Enable-SCDWJobSchedule -JobName Extract_<data warehouse management group name>
    ```

    ```
    Enable-SCDWJobSchedule -JobName Extract_<Service Manager management group name>
    ```

    ```
    Enable-SCDWJobSchedule -JobName Transform.Common
    ```

    ```
    Enable-SCDWJobSchedule -JobName Load.Common
    ```

3.  Type **exit**, and then press ENTER.



You can use the following procedure to disable the schedule for the extract, transform, and load (ETL) jobs; however, you can use this procedure to disable the schedule for any data warehouse job. In this release of Service Manager, you can disable the schedules only by using Windows PowerShell cmdlets.


### To disable a schedule for a data warehouse job by using Windows PowerShell cmdlets

1.  On the computer that hosts the data warehouse management server, click **Start**, point to **All Programs**, click **Microsoft System Center**, click **Service Manager 2016**, and then click **Service Manager Shell**.
2.  At the Windows PowerShell prompt, type the following commands, and press ENTER after each command:

    ```
    Disable-SCDWJobSchedule -JobName Extract_<data warehouse management group name>
    ```

    ```
    Disable-SCDWJobSchedule -JobName Extract_<Service Manager management group name>
    ```

    ```
    Disable-SCDWJobSchedule -JobName Transform.Common
    ```

    ```
    Disable-SCDWJobSchedule -JobName Load.Common
    ```

3.  Type **exit**, and then press ENTER.

## Stop and start a data warehouse job

You can stop and start data warehouse jobs that are running in Service Manager. For example, you might have to stop all of the data warehouse jobs that are running to ensure that a security update to the data warehouse management server does not interfere with any jobs that might run. After the server has been updated and restarted, you resume all the data warehouse jobs. You can stop and then start jobs by using the Service Manager console or by using Windows PowerShell cmdlets. In this example, only the extract, transform, and load (ETL) jobs are running.

> [!NOTE]
> For information about using the Service Manager Windows PowerShell cmdlets, see [Configuring and Using the Service Manager Cmdlets for Windows PowerShell](sm-cmdlets.md).

### To stop and start data warehouse jobs using the Service Manager console

1.  In the Service Manager console, click **Data Warehouse**.
2.  Expand **Data Warehouse**, and then click **Data Warehouse Jobs**.
3.  In the **Data Warehouse Jobs** pane, select a job that is running, and then click **Suspend** in the **Tasks** list.
4.  Repeat the previous step for each data warehouse job.
5.  To resume each job, select a job that is stopped in the **Data Warehouse Jobs** pane, and then click **Resume** in the **Tasks** list.

### To stop all data warehouse jobs using Windows PowerShell cmdlets

1.  On the computer that hosts the data warehouse management server, click **Start**, point to **All Programs**, click **Microsoft System Center**, click **Service Manager 2016**, and then click **Service Manager Shell**.
2.  At the Windows PowerShell prompt, type the following commands, and then press ENTER after each command:

    ```
    Stop-SCDWJob-JobName Extract_<data warehouse management group name>
    ```

    ```
    Stop-SCDWJob -JobName Extract_<Service Manager management group name>
    ```

    ```
    Stop-SCDWJob -JobName Transform.Common
    ```

    ```
    Stop-SCDWJob -JobName Load.Common
    ```

3.  Type **exit**, and then press ENTER.

### To start all data warehouse jobs using Windows PowerShell cmdlets

1.  On the computer that hosts the data warehouse management server, click **Start**, point to **All Programs**, click **Microsoft System Center**, click **Service Manager 2016**, and then click **Service Manager Shell**.
2.  At the Windows PowerShell prompt, type the following commands, and then press ENTER after each command:

    ```
    Start-SCDWJob -JobName Extract_<data warehouse management group name>
    ```

    ```
    Start-SCDWJob -JobName Extract_<Service Manager management group name>
    ```

    ```
    Start-SCDWJob -JobName Transform.Common
    ```

    ```
    Start-SCDWJob -JobName Load.Common
    ```

3.  Type **exit**, and then press ENTER.

## Schedule a data warehouse job in Service Manager

You can use the following procedure to schedule a data warehouse job in Service Manager.

You could use this procedure in a scenario where a schedule for the data warehouse jobs has been defined in Service Manager. You want to change the schedule for the data warehouse jobs to define standard maintenance windows for the Service Manager database and for the data warehouse. Use the **Set-SCDWJobSchedule** cmdlet to schedule the data warehouse jobs. The `Set-SCDWJobSchedule -ScheduleType Weekly` cmdlet and parameter combination allows jobs to run only on the days you specify. For example, the following commands define a daily or weekly schedule:

```
Set-SCDWJobSchedule -JobName Transform.Common -ScheduleType Daily -DailyFrequency  01:00:00 -DailyStart 06:00
```

```
Set-SCDWJobSchedule -JobName Transform.Common -ScheduleType Weekly -WeeklyFrequency Tuesday, Thursday -WeeklyStart 06:00
```

> [!NOTE]
> To run Windows PowerShell cmdlets, the execution policy must be set to RemoteSigned.

In the following procedure, you configure a schedule for the Transform job to run every 45 minutes, starting at 2:00 in the morning. However, you can modify the commands to set your own schedule.

### To configure a schedule for data warehouse jobs

1.  On the computer that hosts the data warehouse management server, click **Start**, point to **All Programs**, click **Microsoft System Center**, click **Service Manager 2016**, and then click **Service Manager Shell**.
2.  At the Windows PowerShell prompt, type the following command, and then press ENTER.

    ```
    Set-SCDWJobSchedule -JobName Transform.Common -ScheduleType Daily -DailyFrequency 00:45:00 -DailyStart 02:00
    ```

### To validate a data warehouse job schedule

1.  On the computer that hosts the data warehouse management server, click **Start**, point to **All Programs**, click **Microsoft System Center**, click **Service Manager 2016**, and then click **Service Manager Shell**.
2.  Type the following command, and then press ENTER:

    ```
    Get-SCDWJobSchedule
    ```

## Process all dimensions in the data warehouse

You can process all the dimensions in the data warehouse in one operation using Windows PowerShell cmdlets, instead of processing each dimension individually. On the server that hosts SQL Server Analysis Services (SSAS), use the following Windows PowerShell script. Be sure to specify the fully qualified server name. You can type each command separately, or you can save them all as a Windows PowerShell script (.ps1) file and then run the script.

Before you can use Service Manager cmdlets, you need to configure the Service Manager Shell. For information about configuring the Service Manager Shell, see [Configuring and Using the System Center 2016 - Service Manager Cmdlets for Windows PowerShell](sm-cmdlets.md).

### To process all dimensions using cmdlets

- Copy and paste the following code snippets at the prompt in a Service Manager Shell:

    ```
    [System.Reflection.Assembly]::LoadWithPartialName("Microsoft.AnalysisServices") > $NULL
    ```

    ```
    $Server = New-Object Microsoft.AnalysisServices.Server
    $Server.Connect("<FullyQualifiedServerName>")
    $Databases = $Server.Databases
    $DWASDB = $Databases["DWASDataBase"]
    $Dimensions = New-Object Microsoft.AnalysisServices.Dimension
    $Dimensions = $DWASDB.Dimensions
    ```

    ```
    foreach ($Dimension in $Dimensions){$Dimension.Process("ProcessFull")}
    ```

## View data warehouse job history

A history of data warehouse jobs is collected as they run in Service Manager. You can view this history to determine how long a job ran or to determine the last time the job ran successfully. When you display the data warehouse job history, you display the number of entries that you specify by using the *NumberOfBatches* parameter. Use the following procedure to view the last five entries in the history of a data warehouse job.

### To view the last five entries in the data warehouse job history

1.  On the computer that hosts the data warehouse management server, click **Start**, point to **All Programs**, click **Microsoft System Center**, click **Service Manager 2016**, and then click **Service Manager Shell**.
2.  Type the following command, and then press ENTER.

    ```
    Get-SCDWJob -NumberOfBatches 5
    ```

3.  Type **exit**, and then press ENTER.

## Troubleshoot a data warehouse job in Service Manager

In Service Manager, you may encounter problems related to data warehouse jobs. After the Data Warehouse Registration Wizard completes and after Reporting becomes available in the Service Manager console, you can start running reports. If, for example, the incident management report you run doesn't show updated data, you can use Windows PowerShell cmdlets to troubleshoot the problem.

You can use the first procedure to determine whether a job failed using Windows PowerShell cmdlets, and you can evaluate any error messages that this job created.

The second procedure can be used to change the default transform job timeout period. If you see that the data warehouse transform job does not complete successfully, then this may be due to the default 3-hour timeout period for the job being surpassed. This can happen due to the fact that a large volume of data is transformed in the data warehouse. To confirm that this is actually happening, you can view the Event Viewer in the Data Warehouse where messages similar to:  **Timeout expired. The timeout period elapsed prior to completion of the operation or the server is not responding.** can be seen for a module. As an example, you might see the message above for the TransformEntityRelatesToEntityFact module. To resolve the problem in this case, you can set the timeout period to be longer than the default value of 10800 seconds.

### To troubleshoot data warehouse jobs by using Windows PowerShell cmdlets

1.  On the computer that hosts the data warehouse management server, start **Windows PowerShell**.
2.  Type the following command, and then press ENTER.

    ```
    Get-SCDWJob
    ```

3.  Review the output, and locate any job with **Failed** status.
4.  Type the following command, and then press ENTER. In the command, specify the data warehouse job that failed as the value of the *JobName* parameter.

    ```
    Get-SCDWJobModule -JobName Transform.Common
    ```

5.  In the output, locate a status of "Failed," and then review the **Error Message** column for more information about why the data warehouse job failed.
6.  When you are ready to retry the failed job, in the Service Manager console, click **Data Warehouse**.
7.  Expand **Data Warehouse**, and then click **Data Warehouse Jobs**.
8.  In the **Data Warehouse Jobs** pane, select the failed job in the list, and then click **Resume** in the **Tasks** list.

### To override the default timeout period

1.  Edit the registry on the data warehouse management server and ensure that the key name **SqlCommandTimeout** under **SOFTWARE\Microsoft\System Center\2016\Common\DAL** exists and is of type DWORD. If it does not exist create it.
2.  Edit the value, which is in seconds, with a positive value.
3.  Restart the Microsoft Monitoring Agent service.
4.  You can resume the Transform.common job to see the change.
