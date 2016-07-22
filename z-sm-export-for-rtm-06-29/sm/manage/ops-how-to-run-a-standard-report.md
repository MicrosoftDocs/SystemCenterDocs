---
title: How to Run a Standard Report
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15cb747b-19e4-41fe-81e2-31418579457f


















---
# How to Run a Standard Report
You can use the following procedure to run a report in System Center 2012 - Service Manager. In this procedure, you run an incident management report to determine how many incidents were resolved in the previous week.  
  
> [!NOTE]  
>  Before you can run a report, the extract, transform, and load \(ETL\) process must be complete. For more information about the ETL process and about how to schedule it to run, see [How to Enable Data Warehouse Jobs Schedules](http://go.microsoft.com/fwlink/p/?LinkId=229825) in the [Administrator's Guide for System Center&nbsp;2012 \- Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209669).  
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
  
## See Also  
 [Using and Managing Standard Reports](../../../sm/manage/operate/Using-and-Managing-Standard-Reports.md)
