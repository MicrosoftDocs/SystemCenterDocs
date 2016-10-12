---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  Registering Source Systems to the System Center Data Warehouse
ms.technology:  service-manager
ms.assetid:  7f48a1c7-dc88-447d-8bde-8af76783e2d3
---

# Registering Source Systems to the System Center Data Warehouse

>Applies To: System Center 2016 - Service Manager

The data warehouse in Service Manager retrieves data from one or more data sources. These data sources are the transactional processing systems that produce and govern data that you will eventually want to measure and analyze. For example, incidents and change requests are created and managed in Service Manager, software updates and power policies are managed in Configuration Manager, and other systems produce and govern other data sets.

Registering the data warehouse creates a relationship between the data warehouse server and the source system so that information can flow between them. In Service Manager, you can register to Service Manager, Operations Manager, and Configuration Manager directly. You can also use the updated software development kit (SDK) layer on top of the data warehouse, which enables you to push data into the data warehouse directly from other sources. For example, you might want to push data from your Human Resources computer system in the data warehouse.

## How to Register the System Center Data Warehouse to Operations Manager

You can use the following procedures in Service Manager to register the System Center Data Warehouse to Operations Manager and then validate the registration.

### To register the data warehouse to Operations Manager

1.  Register System Center Data Warehouse to Service Manager Source.

2.  Wait for the MPSync job to complete.

3.  Using an account that is a member of the Service Manager and data warehouse management administrators group, log on to the computer that hosts the Service Manager console.

4.  In the Service Manager console, select **Data Warehouse**.

5.  In the **Administration** pane, expand **Data Warehouse**, and then select **Data Sources**.

6.  In the **Tasks** list, click **Register data source**.

7.  In the Register Data Source Wizard, on the **Before You Begin** page, click **Next**.

8.  On the **Data Source Type**  page, select **Operations Manager**.

9. Under **Specify a Root Management Server** area, type the following information:

    1.  For **Root Management server name**, type the server name.

    2.  For **Operational database server**, type the database server name.

    3.  For **Database name**, type the name of the database.

10. Click **Next**.

11. On the **Credentials** page, you can accept the default entry in the **Run as account** list, and then click **Next**, or you can enter credentials from a user or group of your choice.

    > [!IMPORTANT]
    > The account that you specify will be assigned administrative credentials on the Service Manager management server and granted Read permission on the Service Manager database. You can specify different credentials from other Service Manager management groups when you are registering with the data warehouse.

12. On the **Summary** page, you can review the settings that you have chosen. Click **Finish**.

13. On the **Result** page, when **Data source registration complete.** appears, click **Finish**.

### To validate the Operations Manager registration process

-   In the **Data Sources** view, the new data source appears in the list of data sources, with the data source type of **Operations Manager**. You might have to refresh your view to see the new data source.

## How to Register the System Center Data Warehouse to Configuration Manager


You can use the following steps in Service Manager to register Configuration Manager with the System Center Data Warehouse and then validate the registration.

### To register Configuration Manager with the data warehouse

1.  By using an account that is a member of the Service Manager and data warehouse management administrators group, log on to the computer that hosts the Service Manager console.

2.  In the Service Manager console, select **Data Warehouse**.

3.  In the **Administration** pane, expand **Data Warehouse**, and then select **Data Sources**.

4.  In the **Tasks** list, click **Register data source**.

5.  In the Register Data Source Wizard, on the **Before You Begin** page, click **Next**.

6.  On the **Data Source Type**  page, select **Configuration Manager**.

7.  Under **Specify a Central Site Server**, type the following information:

    1.  For **Central Site server name**, type the site server name.

    2.  For **Database name**, type the name of the database.

8.  Click **Next**.

9. On the **Credentials** page, you can accept the default entry in the **Run as account** list, and then click **Next**, or you can enter credentials from a user or group of your choice.

    > [!IMPORTANT]
    > The account that you specify will be assigned administrative credentials on the Service Manager management server and granted Read permission on the Service Manager database. You can specify different credentials from other Service Manager management groups when you are registering with the data warehouse.

10. On the **Data Selection** page, choose the domains to extract, and then click **Next**. For example, select **System Center Configuration Manager Connector Configuration** and **System Center Configuration Manager Power Management Connector**.

11. On the **Summary** page, you can review the settings that you have chosen. Click **Finish**.

12. On the **Result** page, when **Data source registration complete** appears, click **Finish**.

### To validate the Configuration Manager registration process

-   In the **Data Sources** view, the new data source appears in the list of data sources, with the data source type of **Configuration Manager**. You might have to refresh your view to see the new data source.

## How to Register the System Center Data Warehouse to a Service Manager Source


You can use the following procedures in Service Manager to register the System Center Data Warehouse with a Service Manager management group and then validate the registration. This makes it possible to host multiple Service Manager management groups in a single data warehouse.

### To register the data warehouse with another Service Manager management group

1.  By using an account that is a member of the Service Manager and data warehouse management administrators group, log on to the computer that hosts the Service Manager console.

2.  In the Service Manager console, select **Data Warehouse**.

3.  In the **Administration** pane, expand **Data Warehouse**, and then select **Data Sources**.

4.  In the **Tasks** list, click **Register data source**.

5.  In the Register Data Source Wizard, on the **Before You Begin** page, click **Next**.

6.  On the **Data Source Type**  page, select **Service Manager**.

7.  Under **Specify a Service Manager Server**, type the following information:

    1.  For **Service Manager server name**, type the server name.

8.  Click **Next**.

9. On the **Credentials** page, you can accept the default entry in the **Run as account** list, and then click **Next**, or you can enter credentials from a user or group of your choice.

    > [!IMPORTANT]
    > The account that you specify will be assigned administrative credentials on the Service Manager management server and granted Read permission on the Service Manager database. You can specify different credentials from other Service Manager management groups when registering with the data warehouse.

10. On the **Summary** page, you can review the settings that you have chosen. Click **Finish**.

11. On the **Result** page, when **Data source registration complete.** appears, click **Finish**.

### To validate the  Service Manager registration process

-   In the **Data Sources** view, the new data source appears in the list of data sources, with the data source type of **Service Manager**. You might have to refresh your view to see the new data source.

## How to Manage Data Import Jobs for Operations Manager and Configuration Manager


You can use the following procedure to manage data warehouse data import jobs in Service Manager. Data import jobs are like other data warehouse jobs, and you can manage them with the Service Manager console and also with Windows PowerShell cmdlets. Methods of management include:

-   Revising the processing schedule to hourly, daily, or weekly

-   Suspending a job

-   Resuming a suspended, or Not Started, job

### To manage data import jobs and change a job schedule

1.  In the Service Manager console, click **Data Warehouse**, expand **Data Warehouse**, and then click **Data Warehouse Jobs**.

2.  In the **Data Warehouse Jobs** pane, select a job name, and then under **Tasks**, click **Properties**.

3.  In the job properties dialog box that appears, you can view the current schedule. You can change the schedule to one of your choice. For example, change the schedule to **Daily** and run the job at **1:00 AM**, and then click **OK**.

4.  You can optionally **Suspend** jobs, and you can **Resume** any that are suspended or Not Started.

## Troubleshooting System Center Data Warehouse Errors

This section describes steps you can take to troubleshoot System Center data warehouse errors in Service Manager.

### Using the Operations Manager event log on the Data Warehouse server to troubleshoot errors
Service Manager event logs are found in the Operations Manager event log. Evaluating events in the log is useful because most errors from the data warehouse are found in this event log. Events in the log are from two different sources: Deployment and Data Warehouse.

Events with a source of **Deployment** are usually generated during management pack deployment, which includes report deployment or assembling the data warehouse, for example, by creating outriggers, dimensions, and fact tables. Errors in the event log usually include instructions about how to recover from the errors. For example, you might read instructions suggesting that you stop and then restart the Service Manager services. The three services on a data warehouse management server are:

-   System Center Data Access Service

-   Microsoft Monitoring Agent

-   System Center Management Configuration

When you start and stop Service Manager services, you must stop and start all three services.

After the data warehouse is deployed, events are more likely to have a source of **Data Warehouse**. These events are created by jobs within the normal course of operations like extract, transform, and load (ETL) jobs; the MPSync job; and the DWMaintenance job.

### Using the Service Manager console to troubleshoot errors
In the Service Manager console, click **Data Warehouse Jobs** and you will see ETL job and MPSync job status. If your deployment was successful and your data warehouse is correctly registered to at least one Service Manager management group, you see at least five jobs. Every job should have the status **Running** or **Not Started**.

If you see a job status listed as **Failed**, you can select the job, and then in the **Tasks** pane, click **Modules** to find out which job module has failed. Then, you can examine the  Operations Manager event log on the data warehouse server to determine why the module failed.

In the **Data Warehouse** workspace, you can click **Management Packs** in the left pane. That is where you can view all the management packs in the data warehouse and the status of their deployment. When you import a management pack to Service Manager, the MPSync job synchronizes it to the data warehouse, where the MPSync job derives its name from management pack synchronization. When you get the list of management packs in the data warehouse, you can find out if your management pack has been deployed successfully or not.

If your management pack has defined data warehouse-specific elements, such as outriggers, dimensions, fact tables, or reports, that management pack must be successfully deployed before the new tables and reports will be ready to use.

### Using Windows PowerShell to troubleshoot errors
The Windows PowerShell cmdlets in the following table provide detailed information about the data warehouse jobs.

|Command|Description|
|-----------|---------------|
|Get-SCDWMgmtGroup|This command tells you which sources are currently registered with the data warehouse. You should expect to see at least two different DataSourceName values.|
|Get-SCDWJob|This command lists the data warehouse job status of the current batch. Using the command, you can check whether the jobs are enabled or not, which jobs are running, and when they started.<br /><br />When the MPSync or DWMaintenance jobs start, they disable all of the ETL jobs. You will see the **Is Enabled** column set to **False** for each of the ETL jobs. This means that even if the ETL job status shows it is running, it actually is not running. When the MPSync or DWMaintenance job completes, the ETL jobs are automatically enabled and resume processing.<br /><br />Jobs normally have the **Not Started** status, unless the previous batch has completed. If you prefer, you can use the **Get-SCDWJob** command to view the last few batches of a specific job.|
|Get-SCDWJob -JobName *Specific job name* -NumberOfBatches *number* |Use this command to see the latest job, specified by *Specific job name*, completed, when it started, and when it ended. You can calculate how long it ran and what the next batch ID and status is. The job batch ID is always incremental.|
|Get-SCDWJobModule|This command provides detailed information about the specific modules within the job. This is very useful when you see job failures and you want to find out what caused the failure.|

### Troubleshooting Common Data Warehouse Issues
This list is not exhaustive, but it covers most of the common problems that you are likely to encounter.

#### Reports are not deployed after registering the data warehouse
**Symptoms**

When you open the Service Manager console, a dialog box appears indicating that the Reporting Service is unavailable. Another symptom is that the **Reporting** workspace button appears in the Service Manager console; however, there are no reports displayed in the workspace. Another symptom is that no reports have been deployed to the Reporting Services server.

Other aspects of the data warehouse deployment might appear to have gone smoothly. For example, in the Service Manager console, when you click **Data Warehouse**, and then click **Data Warehouse Jobs**, you see two extract jobs, a transform and load job, and an MPSync job.

**Troubleshooting Steps**

To troubleshoot this problem, complete the following steps.

Step 1: Check the deployment status of your management packs:

1.  In the Service Manager console, click **Data Warehouse**.

2.  Click **Management Packs**, and in the search **Filter** box, type **report**. This filters results to report-related management packs.

3.  Check the deployment status (last column) of the following management packs. None of the management packs should have a status of **Failed**.

    -   ServiceManager.ActivityManagement.Report.Library

    -   ServiceManager.ProblemManagement.Report.Library

    -   ServiceManager.IncidentManagement.Report.Libraryxxx

    -   ServiceManager.ConfigurationManagement.Report.Library

    -   ServiceManager.ChangeManagement.Report.Library

Step 2: Check the event log for error messages that mention the assembly Microsoft.EnterpriseManagement.Reporting.Code.dll file.

If any of the above five management packs failed deployment:

1.  On the data warehouse management server, open the Operations Manager event log.

2.  Filter the events with **Event Sources** as **Deployment** and **Event Level** as **Error**.

3.  If there are error messages in the event log that indicate **cannot load Assembly Microsoft.EnterpriseManagement.Reporting.Code.dll**, review the following items:

    1.  Your installation of SQL Server Reporting Services (SSRS) may be on a different server than the data warehouse management server.

    2.  If your SSRS installation is on the same server as the data warehouse management server, restart the SSRS service.

4.  Restart SSRS:

    1.  Log on to the server where SSRS is installed.

    2.  Open  **Reporting Services Configuration Manager**.

    3.  In the **Reporting Services Configuration Connection** window, click **Connect**.

    4.  In the **Reporting Server Status** window, click **Stop**, and then click **Start**.

    5.  Click **Exit**.

Step 3: Redeploy any failed report management packs:

1.  In the Service Manager console, click **Data Warehouse**.

2.  Click **Management Packs**, and then in the search filter, type **report**.

3.  For each of the management packs listed in step 1, in the **Tasks Pane**, click **Restart Deployment**.

    > [!NOTE]
    > If the deployment status of a management pack is listed as **Completed**, the **Restart Deployment** option is unavailable.

After the deployment status of the report management packs has updated from **Failed** to **Completed**, open the Service Manager console. Reports should display in the **Reporting** workspace. You may have to restart the Service Manager console to view the reports because the console caches the list of reports.

#### Jobs fail after importing a custom management pack
**Symptom**

One or more data warehouse jobs start failing after importing a custom management pack and synchronizing it to the data warehouse.

**Troubleshooting Steps**

To troubleshoot this problem, complete the following steps:

1.  Check the event log to ensure that the root cause is the custom management pack:

    1.  On data warehouse management server, open the Operations Manager event log.

    2.  Find the event that is related to the job failure.

    3.  Determine if the failure is related to the custom management pack you imported.

2.  If the failure is related to the custom management pack, you should remove it and let the rest of the data warehouse operate as usual. You can fix the management pack and reimport it later:

    1.  Uninstall the custom management pack using the Service Manager console.

    2.  Run the MP Sync job.

    3.  Verify that the custom management pack is listed in **Data Warehouse** under **Management Packs**.

    4.  After the MP Sync job is completed, resume the failed job either from the Service Manager console or with a Windows PowerShell cmdlet.

3.  Fix and reimport the custom management pack:

    1.  Remove the custom management pack and recover from the failure using step 2, shown previously.

    2.  Fix the custom management pack.

    3.  Import the fixed custom management pack into Service Manager, and then run the MP Sync job to sync it to the data warehouse.

#### Data warehouse is not receiving new data, or jobs seem to take too long to complete
**Symptom**

You do not see data or new data in any of your reports. Another symptom is that ETL jobs are taking too long to run and the jobs do not show a status of **Not Started**.

**Troubleshooting Steps**

To troubleshoot this problem, complete the following steps:

1.  Use the Windows PowerShell cmdlet **Get-SCDWJob** to determine if all ETL jobs are enabled. Start Windows PowerShell, and then type **Get-SCDWJob**.

2.  If the ETL jobs are disabled and either the MPSyncJob or DWMaintenance jobs are running, you will have to wait awhile to get the job status again because these two background jobs disable the ETL jobs. However, if the two jobs are listed as **Not Started** and the ETL jobs are disabled, you can use the **Enable-SCDWJob** cmdlet to enable each of them, for example:

    ```
    Enable-SCDWJob -JobName Transform.Common
    ```

3.  If the MPSync and DWMaintenance ETL jobs are all enabled and running but their individual batch ID has not changed for a long time, or if you use the **Get-SCDWJobModule** cmdlet for specific jobs and you do not see that any module is actually running, check the event log and see if there are any error messages. Sometimes the error message might be many days old and you might need to review many days-worth of events.

4.  Check if the three services: System Center Data Access Service, Microsoft Monitoring Agent, and System Center Management Configuration on the data warehouse management server are actually running. On the data warehouse management server, click **Start**, click **Run**, and then type **Services.msc**. In **Services** verify that the following services are running: System Center Data Access Service, Microsoft Monitoring Agent, and System Center Management Configuration.

    If any of the services are not running, restart all three services. In addition, if all services are actually running, events from the Event Source Data Warehouse and OpsMgr SDK Service are sent to the Operations Manager event log. You can use this information as another source to verify whether all the services are running. If you do not see events from the Event Source Data Warehouse and OpsMgr SDK Service for a long time, you should restart all three services.

#### Custom data warehouse extensions do not appear in the data warehouse
**Symptom**

After importing your management pack, which defines some dimensions or fact tables to Service Manager, the MPSync job has run several times, but you still do not see your dimension or fact tables in the DataMart.

**Troubleshooting Steps**

Ensure that your management pack is sealed. The MPSync Job can import only sealed management packs from Service Manager into the data warehouse. If you have not sealed your management pack, seal it, and then import it using the Service Manager.

Ensure that your management pack is synced to the data warehouse by completing the following steps:

1.  Open the Service Manager console.

2.  Click **Data Warehouse**.

3.  Click **Management Packs**, and then locate your management pack in the list of management packs. To do this, use the search feature by typing your management pack name in the search box. If you do not see your management pack:

    1.  It might have failed to import into the data warehouse management server. Go to the data warehouse management server, open the Operations Manager event log and then filter the events with **Event Sources** as **OpsMgr SDK Service**.

    2.  The MPSync job may not have run yet. It runs on a recurring schedule, which is, by default, once every hour. You can modify the schedule with Windows PowerShell. To speed up management pack synchronization, after you import your management pack you can manually resume the MPSync job, either from the Service Manager console or by using Windows PowerShell.

Check the deployment status of your management pack:

1.  Open the Service Manager console.

2.  Click **Data Warehouse**.

3.  Click **Management Packs**, and then find your management pack in the list of management packs. To do this you can search for your management pack name.

4.  Check the deployment status of your management pack. If the deployment status is **Failed**:

    1.  On the data warehouse management server, open the Operations Manager event log, and then filter the events with **Event Sources** as **Deployment**.

    2.  If there is an error message, the message usually indicates what went wrong. If after you make any needed fixes to the management pack and the error still occurs, you can uninstall this management pack using the Service Manager console. After the MPSync job runs, the management pack is uninstalled from data warehouse management server.

#### Management packs are stuck in Pending Association status after registering to the data warehouse
**Symptom**

Some management packs remain in **Pending Association** status several hours after registering Service Manager with the data warehouse and several (up to four or more) hours have passed. You can determine the time elapsed by opening the Service Manager console and navigating to **Data Warehouse**, **Data Warehouse Jobs**, **MPSync Job**, and then clicking **Details** from the **Tasks** pane.

**Troubleshooting Steps**

To troubleshoot this problem, complete the following steps:

1.  View the **Details** of the MPSync job. Review each batch ID for the problem management pack in the **MPSyncJob** dialog box. In the **MP Sync Job** dialog box, click the **Management Pack** column name to sort the list according to management pack name. Find any management packs with **Pending Association** status. In the list of management packs, check to see if, in the later batch, the management pack status is listed as **Associated**, for example:

    -   For Batch ID 136, Management Pack Microsoft.SystemCenter.ConfigurationManager is Pending Association.

    -   For Batch ID 207, Management Pack Microsoft.SystemCenter.ConfigurationManager is Associated.

    This indicates the management pack is associated properly in batch 207, even though it ran into an error in batch 136. Because it recovered in batch 207, the management pack is correctly associated and the synchronization completed successfully.

2.  If in the **MP Sync Job** dialog box, the Pending Association status for a management pack repeats for every batch, you will have to troubleshoot further to determine the reason why the management pack fails to associate. You should start by looking for deployment failures in other management packs that your management pack depends on.

    In the Service Manager console, click **Data Warehouse**, click **Management Packs**, and then click the **Deployment Status** column heading. If you see any management pack with a deployment status of **Failed** or **Not Started**, this is usually due to a management pack dependency. Because management packs can depend on others, any failure can cause other management packs to fail deployment. Any impacted management pack has the **Not Started** status.

3.  Find the deployment failures in the event log. Open the Operations Manager Event log on the data warehouse, filter the event log to the events where the Event Source is **Deployment** and Event Level is **Warning** or **Error**.

4.  If there is an error message similar to the following message, you will have to unregister the data warehouse from Service Manager, reinstall the data warehouse, and then reregister the Service Manager management server to the data warehouse management server:

    ```
    Deployment Execution Infrastructure has retried the maximum number of times and is giving up on this execution step.
    MP Element ID:  DerivedManagementPack.SystemDerivedMp.ServiceManager.ActivityManagement.Library.Datawarehouse
    MP name: ServiceManager.ActivityManagement.Library.Datawarehouse
    MP version: 7.0.5826.0
    Operation: Install
    Error message:  Cannot find resource with ID TransformActivityStatusResource
    ```

#### ETL jobs fail due to login credentials problems
**Symptom**

Some or all ETL jobs have failed. The Operations Manager event log on the data warehouse management server indicates that the ETL job failure is related to a login user failure.

**Troubleshooting Steps**

To troubleshoot this problem, check if the password for each Run As account has changed or expired. You can update the account using the following steps:

1.  Navigate to **Data Warehouse**, **Security**, **Run As Accounts**, and then click the related run as account. Click **Properties** in the **Tasks** pane, update the **Password** field in the window, and then click **OK**.

2.  If this Run As account is an Operational System Account, you also have to update the services that are running under the account:

    1.  On the data warehouse management server, click **Start**, click **Run**, and then type **Services.msc**.

    2.  In **Services**, update the passwords for the services that run under the account, for example, System Center Data Access Service and System Center Management Configuration.

    3.  Restart the services.

        > [!NOTE]
        > The MP Sync job and Extract jobs can use a different Run As account other than Operational System Account. This Run As account is created when Service Manager is registered to a data warehouse.

It is easy to update the password if it is expired. However it is more difficult to update the system if you change the Run As account. We do not recommend that you modify Run As accounts.

If the job failure is not related to the password, make sure that the Run As account for the failed job can be used to connect to the target database. For example, ensure that the Extract job Run As account can be used to connect to the Service Manager database. If not, make sure that the Structured Query Language (SQL) service that is hosting the database is running.
