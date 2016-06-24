---
title: Using and Managing Standard Reports
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 89cef640-a705-4755-96b1-cedb54ff79db
---
# Using and Managing Standard Reports
This section describes how to use standard reports in System Center 2016 Technical Preview - Service Manager.

The simple reporting infrastructure that is included in both System Center 2016 Technical Preview - Service Manager and System Center 2016 Technical Preview - Service Manager is built on SQL Server Reporting Services (SSRS), where data is accessed from the Service Manager data warehouse. The SSRS infrastructure provides for basic reporting functionality, such as report-level security, report subscriptions, browser-based access to reports, linked reports, and customization. This reporting functionally is similar to the experience that is included with Operations Manager.

The Reporting workspace contains the catalog of reports that users can run on demand. Reports are viewable for all Service Manager console users. If users can view work items and have permission to the SystemCenter and ServiceManager folders on the SSRS server, they can also view reports in work item task lists. Like in  Operations Manager, you can run a report in context. For example, you can select a computer in a view in the console and then run the Computer Details report about that computer. Any user can export report data from a report they view. Exported reports are saved in a variety of file formats.

For more information about SSRS, see [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=238589). If you want to see the relationship between high-level processes and services that are involved between Service Manager and SSRS, refer to the Service Manager architecture diagram (ArchitectureDiagram.vsd) that is included in the Service Manager job aids (SM_job_aids.zip). Because the architecture diagram is too large to see properly in this guide, you can download it and the other jobs aids from the [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkID=186291).

## To use standard reports

-   Vew the Standard Report Catalog.

-   Add permissions for standard reports.

-   Run standard reports.

-   Export a standard report.

-   Create a standard linked report.

-   Add a standard report to the Service Manager Favorite Reports folder.

-   Configure standard report subscriptions.

-   Schedule a standard Service Manager report.

-   Add reports to the report catalog that were not created in Service Manager.

-   Review the [Standard Reports Available in Service Manager](Standard-Reports-Available-in-Service-Manager.md)


