---
title: Using and Managing Standard Reports
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c083343-c3b2-47a6-8cd9-ca5fc0a99a05
---

# Using and Managing Standard Reports

>Applies To: System Center 2016 - Service Manager

This section describes how to use standard reports in Service Manager.  

 The simple reporting infrastructure that is included in Service Manager is built on SQL&nbsp;Server Reporting Services \(SSRS\), where data is accessed from the Service Manager data warehouse. The SSRS infrastructure provides for basic reporting functionality, such as report\-level security, report subscriptions, browser\-based access to reports, linked reports, and customization. This reporting functionally is similar to the experience that is included with System Center Operations Manager.  

 The Reporting workspace contains the catalog of reports that users can run on demand. Reports are viewable for all Service Manager console users. If users can view work items and have permission to the SystemCenter and ServiceManager folders on the SSRS server, they can also view reports in work item task lists. Like in Operations Manager, you can run a report in context. For example, you can select a computer in a view in the console and then run the Computer Details report about that computer. Any user can export report data from a report they view. Exported reports are saved in a variety of file formats.  

 For more information about SSRS, see [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=238589). If you want to see the relationship between high\-level processes and services that are involved between Service Manager and SSRS, refer to the Service Manager architecture diagram \(ArchitectureDiagram.vsd\) that is included in the Service Manager job aids \(SM\_job\_aids.zip\). Because the architecture diagram is too large to see properly in this guide, you can download it and the other jobs aids from the [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkID=186291).  

## How to View the Standard Report Catalog

You can use the following procedure to view the catalog of reports that is available in Service Manager.  

### To view the report catalog  

1.  In the Service Manager console, click **Reporting**.  

2.  Expand **Reports**, and then click a folder. For example, click **Incident Management**.  

 The reports that are available appear in the results pane of the **Report** console.  

## How to Add Permissions for Standard Reports

By default, all System Center 2016 - Service Manager users have access to reports through the Reporting workspace. However, before users who do not have administrator permissions can view the Reporting workspace, you must add permissions through SQL&nbsp;Server Reporting Services \(SSRS\).  

 You can grant access at the root level, which enables a user to view the Reporting workspace and all the reports in Service Manager. You can also grant restricted access to specific report folders, such as the Incident report folder, or to individual reports.  

 The following procedure describes how to grant SSRS access for all the Service Manager reports to an Active&nbsp;Directory group \(woodgrove\\SCSMReportAccess\).  

### To add SSRS permissions  

1.  On the computer on which SRSS is installed, start Report Manager. For example, open `http://ReportServerName:80/Reports`.  

2.  Locate the folder or report for which you want to grant access permission. For example, locate the SystemCenter and ServiceManager root folders.  

3.  Click **Security**.  

4.  Click **Edit Item Security**.  

5.  The following message appears: "Item security is inherited from a parent item. Do you want to apply security settings for this item that are different from those of the Home parent item?"  

     Click **OK**.  

6.  Click **New Role Assignment**.  

7.  Type the name of the Active&nbsp;Directory group or user in the **Group or user name** box. For example, type **woodgrove\\SCSMReportAccess**.  

8.  Set the roles for the group or user. Select the **Browser** check box to grant access to run reports.  

9. Click **OK**.   

## How to Run a Standard Report

You can use the following procedure to run a report in Service Manager. In this procedure, you run an incident management report to determine how many incidents were resolved in the previous week.  

> [!NOTE]  
>  Before you can run a report, the extract, transform, and load \(ETL\) process must be complete. For more information about the ETL process and about how to schedule it to run, see [How to Enable Data Warehouse Jobs Schedules](admin-how-to-enable-disable-data-warehouse-job-schedules.md).  
>   
>  The Service Manager data warehouse does not create dimensions for classes or relationships in unsealed management packs. If you are using an unsealed management pack, you will not see any data from that management pack in your reports. Because of this, the best practice is to model all classes and relationships in sealed management packs.  
>   
>  For this example, you must have previously created an incident. Otherwise, the report will return no data.  

### To run a report  

1.  In the Service Manager console, click **Reporting**.  

2.  Expand **Reports**, and then expand a report folder. For example, expand **Incident Management**.  

3.  Click the name of the report you want to run. For example, click the **List of Incidents** report.  

4.  In the **Tasks** list, click **Run Report**.  

5.  Click **Parameter Control Header** to display the parameter controls for the report. Use these parameters to customize the report.  

     Each report has a set of parameters you can use to search and filter for the specific items you want to include in the report. For example, in the **List of Incidents** report, you can set the following parameters:  

    -   **Date Filter**. You can search by the date the incident was created, by the date it was resolved, or by the date it was closed.  

    -   **Assigned To**  

    -   **Priority**  

    -   **ID**  

    -   **Description**  

    -   **Resolution Description**  

    -   **Contact Method**  

    -   **Source**  

    -   **Status**  

    -   **Classification Category**  

    -   **Support Group**  

    -   **Urgency**  

    -   **Impact**  

    -   **Resolution Category**  

6.  In the **Start Date** list, select the date one week before the current date \(today\), and then click anywhere in the form.  

7.  Optionally, specify other criteria that you want to filter.  

8.  In the **Tasks** list, click **Run Report**.  

9. In the report, review the data to ensure the incident information that you want to view is displayed. If you do not see the information you expect, revise the criteria, and then run the report again by clicking **Run Report**.  

     In reports that show lists or additional detail, such as the associated subreports in the List of Incidents report, you might see multiple rows that contain the same information. This is because an instance can have multiple types; for example, a computer is a Computer, a Windows Computer, and a Managed Windows Computer. The level of detail for these reports is per type per instance. Therefore, these multiple types result in multiple rows.  

    > [!NOTE]  
    >  If there is no data in the report, ensure that the ETL process is complete. A delay might occur between the start of the process and when data is available for reports.

## How to Export Standard Report Data

You can use the following procedure to export a report into several different types of files so that you can use the data from the reports in different tools. For example, you can export the report data into a comma\-separated value \(CSV\) file and then import it into Microsoft&nbsp;Office&nbsp;Excel.  

### To open the report and then export the report data  

1.  In the Service Manager console, click **Reporting**.  

2.  Expand **Reports**, and then click any view. For example, click **Incident Management**.  

3.  In the **Incident Management** view, select the **List of Incidents** report, and then in the **Tasks** list, click **Run Report**.  

4.  Click **Parameter Control Header** to display the parameter controls for the report. Use these parameters to customize the report.  

5.  In the **Start Date** list, select the date one week before the current date \(today\), and then click anywhere in the form.  

6.  Optionally, specify other criteria that you want to filter.  

7.  In the **Tasks** list, click **Run Report**.  

8.  In the **List of Incidents** report, review the data to ensure the incident information that you want to view is displayed. If you do not see the information you expect, revise the criteria, and then run the report again by clicking **Run Report**.  

9. Click the **Export** icon, and then select the format in which you want to save the report. In the list, select one of the following:  

    -   **XML file with report data**  

    -   **CSV \(comma delimited\)**  

    -   **Acrobat \(PDF\) file**  

    -   **MHTML \(web archive\)**  

    -   **Excel**  

    -   **TIFF file**  

    -   **Word**  

10. Save the file to the desktop with a file name of your choice, and then close the report form.  

## How to Create a Standard Linked Report in Service Manager

You can use the following procedure to create a linked report.  

 A linked report is a shortcut to a report-it is similar to a program shortcut on your desktop. A linked report is derived from publicly defined reports from any management pack. A linked report retains some of the original report's properties, such as the report layout. Other properties of the linked report, such as parameters and subscriptions, can be different from the original report.  

### To create a linked report  

1.  In the **Reporting** view, select the report you want to use as the basis for the linked report, and then, in the **Tasks** pane, click **Run Report**.  

2.  In the **Report** window, click **Save as Linked Report** in the **Task** pane.  

3.  Type a name and an optional description for the new linked report.  

4.  Select a management pack for the linked report.  

5.  Click **Select Folder**, and then select the folder in which you want to save the report.  

6.  Click **OK**.  

7.  Close the report.  

 After the next data warehouse synchronization, the new linked report is displayed in the folder where you saved it. For information about scheduling a data warehouse synchronization job, see [How to Schedule a Data Warehouse Job](admin-how-to-schedule-a-data-warehouse-job.md).  

> [!NOTE]  
>  You might have to close and reopen the console after the synchronization job is complete to see the report.  

## How to Add a Standard Report to the Service Manager Favorite Reports Folder

You can use the following procedure to add a report to the Favorite Reports folder in Service Manager.  

 After you have run several reports and determined the best parameters to use to customize the report contents, you can save a report to the Favorite Reports folder. This enables you to run the report directly from the **Reporting** view without having to specify parameters.  

### To save a report to the Favorite Reports folder  

1.  In the **Reporting** view, select the report that you want to use as the basis for the saved report, and then, in the **Tasks** pane, click **Run Report**.  

2.  In the report window, click **Save as Favorite Report** under **Tasks**.  

3.  Type a name for the report, and then click **OK**.  

4.  Close the report window.  

5.  In the **Reporting** navigation tree, click **Favorite Reports**.  

 The new report is displayed.  

## How to Configure Standard Report Subscriptions

You can set up subscriptions to your reports in Service Manager through SQL&nbsp;Server Reporting Services \(SSRS\) Report Manager. Configuring a subscription to a report enables you to automate the delivery of a report. Report subscriptions can be sent through email, stored on the report server, or even posted to a Microsoft SharePoint site.  

### To create report subscriptions  

-   Complete the procedures in the [Subscriptions and Delivery \(Reporting Services\)](http://go.microsoft.com/fwlink/p/?LinkID=158830) topic.   

# How to Schedule a Standard Service Manager Report

In Service Manager, you can schedule a linked report to run on a regular basis to ensure that the information is up to date. To do this, use SQL&nbsp;Server Reporting Services \(SSRS\) Report Manager. In SSRS Report Manager, you can schedule reports to run one time or on a continuous basis at intervals of hours, days, weeks, or months. You can do the following:  

-   Schedule report delivery in a standard or data\-driven subscription.  

-   Schedule report history so that new snapshots are added to the report history at regular intervals.  

-   Schedule time to refresh the data of a report snapshot.  

-   Schedule the expiration of a cached report to occur at a predefined time so that it can be refreshed later.  

 To configure a schedule for a report, complete the procedure in the [Scheduling Reports, Shared Datasets, and Subscriptions](http://go.microsoft.com/fwlink/?LinkId=158822).  

## How to Add Non-Service Manager Reports to the Report Catalog

You can display SQL Server Reporting Services \(SSRS\) reports from any source using the Reporting workspace in the Service Manager console. The Reports workspace in Service Manager displays the folders and reports that are contained in the System Center\\Service Manager folder on the SSRS server. Therefore, you can add any reports that you want to the folder. For example, you might have a financial report that you want to view from the Reporting workspace.  

### To add a custom report to the report catalog  

1.  On the server that hosts SSRS, open Report Manager. For example, open `http://ReportServerName:80/Reports`.  

2.  Navigate to the System Center\\ServiceManager reports folder, create a new folder, and give it a name. For example, name the folder **Financial Management**.  

3.  In the new folder, click **New Data Source**, and then add the data source of the new report.  

4.  Add the new report that uses the new data source.  

5.  Open the Service Manager console, select the **Reporting** workspace, and then navigate to the folder that contains the report.  

6.  In the **Tasks** pane, click **Run Report**.   

## Standard Reports Available in Service Manager

The following reports are available in Service Manager.  

|Report area|Report name|Description|  
|-----------------|-----------------|-----------------|  
|Activity management|List of Activities|Provides a list of activities within a certain time frame that meet the specified criteria. The data in the report includes the type of activity, the current status, and the priority.|  
|Activity management|List of Manual Activities|Provides a list of all the manual activities within a certain time frame that also meet the specified criteria. The data in the report includes the current status, stage, priority, and user to whom the activity is assigned.|  
|Activity management|List of Review Activities|Provides a list of all the review activities within a certain time frame that meet the specified criteria. The data in this report includes the current status, stage, approval condition, and approval threshold.|  
|Activity management|Manual Activity Detail|Provides detailed information about a specific manual activity, including the title, description, status, and affected customers.|  
|Activity management|Review Activity Detail|Provides detailed information about a specific review activity, including the title, description, status, reviewers, and approval condition.|  
|Activity management|Activity Distribution|Provides the number of activities during a specified time frame. The data in this report includes the activity status, type, and stage. You can filter the data by status, stage, or type.|  
|Change management|Change Management KPI Trend|Provides the number and current state \(in progress, completed, failed, or canceled\) of change requests during a specified time frame. You can filter the data returned in this report by day, week, month, quarter, or year.|  
|Change management|List of Change Requests|Provides a list of change requests within a certain time frame. The data in this report includes the current status, category, and user to whom the request is assigned.|  
|Change management|Change Request Detail|Provides detailed information about a specific change request, including the title, description, status, change creator, and template.|  
|Configuration management|Computer Detail|Provides detailed configuration information for a specific computer.|  
|Configuration management|Computer Inventory|Provides a list of computers available in the management group. **Note:**  The Computer Inventory report might contain more total computers than actually exist in a single Service Manager management group. This situation is uncommon but possible when you have more than one management group share a data warehouse. More specifically, if you manually create a computer in one management group and manually create a computer with the same name in another management group, the data warehouse cannot reconcile the two manually\-created computers. Because this situation does not occur when computers are discovered by a connector, you can avoid multiple computers appearing in the report by deleting the manually\-created computer configuration item and then discover it by using a connector.|  
|Configuration Management|Software Update Compliance Trend|Provides detailed information for software update compliance. You can filter this data by classification or category, and by day, week, month, quarter, or year.|  
|Incident management|Incident Analyst|Provides key performance metrics for a specified analyst. The data in this report includes the number of incidents assigned to the analyst, the number of incidents resolved by the analyst, the number of incidents worked on by the analyst, and any labor logged against an incident.|  
|Incident management|Incident Details|Provides detailed information for a specific incident, including the title, description, classification, affected services, affected configuration items, and related activities.|  
|Incident management|Incident KPI Trend|Provides the number of incidents, including the number of incidents past their targeted resolution time, the number of escalated incidents, the average time to resolution, the labor minutes per incident, and the size of the incident backlog. You can filter this data by classification or category, and by day, week, month, quarter, or year.|  
|Incident management|Incident Resolution|Provides the number of incidents, including the number of incidents past their targeted resolution time and the average time to resolution. You can filter the data by day, week, month, quarter or year.|  
|Incident management|List of Incidents|Provides a list of all incidents within a certain time frame. The data in this report includes the users to whom incidents are assigned, when the incidents were created, and the current status of the incidents.|  
|Problem management|Configuration Items \(CIs\) with Most Incidents|Provides a list of the configuration items that have at least the number of incidents associated with them, as specified by the value you enter for **Incidents per Configuration Item** during the specified time frame. This report also includes the number of change requests and problems associated with the specific configuration item.|  
|Problem management|List of Problems|Provides a list of all problems within a certain time frame.|  
|Problem management|Problem detail|Provides detailed information for a specific problem.|  
|Release management|List of Release Records|Provides a list of all release records within a certain time frame.|  
|Release management|Release Record Detail|Provides detailed information for a specific release record.|  
|Service Management|Service KPI Trend|Provides key metrics across services, groups and collections for Service Manager, Operations Manager, and Configuration Manager. This report enables trending and flexible grouping.|  
|Service Management|Service Summary|Provides a scorecard\-like report that includes a comprehensive view of the health of a service, including period\-over\-period analytic capabilities.|  
