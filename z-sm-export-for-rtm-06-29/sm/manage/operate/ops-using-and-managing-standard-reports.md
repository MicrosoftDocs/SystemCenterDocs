---
title: Using and Managing Standard Reports
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c083343-c3b2-47a6-8cd9-ca5fc0a99a05
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Using and Managing Standard Reports
This section describes how to use standard reports in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)].  
  
 The simple reporting infrastructure that is included in both [!INCLUDE[smlong](../../../sm/deploy/upgrade/includes/smlong_md.md)] and [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] is built on SQL Server Reporting Services \(SSRS\), where data is accessed from the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse. The SSRS infrastructure provides for basic reporting functionality, such as report\-level security, report subscriptions, browser\-based access to reports, linked reports, and customization. This reporting functionally is similar to the experience that is included with System Center Operations Manager 2007 R2.  
  
 The Reporting workspace contains the catalog of reports that users can run on demand. Reports are viewable for all [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] users. If users can view work items and have permission to the SystemCenter and ServiceManager folders on the SSRS server, they can also view reports in work item task lists. Like in [!INCLUDE[om12short](../../../sm/deploy/upgrade/includes/om12short_md.md)], you can run a report in context. For example, you can select a computer in a view in the console and then run the Computer Details report about that computer. Any user can export report data from a report they view. Exported reports are saved in a variety of file formats.  
  
 For more information about SSRS, see [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=238589). If you want to see the relationship between high\-level processes and services that are involved between [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] and SSRS, refer to the Service Manager architecture diagram \(ArchitectureDiagram.vsd\) that is included in the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] job aids \(SM\_job\_aids.zip\). Because the architecture diagram is too large to see properly in this guide, you can download it and the other jobs aids from the [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkID=186291).  
  
## Standard Reporting Topics  
  
-   [How to View the Standard Report Catalog](../../../sm/manage/operate/How-to-View-the-Standard-Report-Catalog.md)  
  
     Describes how to view the Standard Report Catalog.  
  
-   [How to Add Permissions for Standard Reports](../../../sm/manage/operate/How-to-Add-Permissions-for-Standard-Reports.md)  
  
     Describes how to add permissions for standard reports.  
  
-   [How to Run a Standard Report](../../../sm/manage/operate/How-to-Run-a-Standard-Report.md)  
  
     Describes how to run standard reports.  
  
-   [How to Export Standard Report Data](../../../sm/manage/operate/How-to-Export-Standard-Report-Data.md)  
  
     Describes how to export a standard report.  
  
-   [How to Create a Standard Linked Report in Service Manager](../../../sm/manage/operate/How-to-Create-a-Standard-Linked-Report-in-Service-Manager.md)  
  
     Describes how to create a standard linked report.  
  
-   [How to Add a Standard Report to the Service Manager Favorite Reports Folder](../../../sm/manage/operate/How-to-Add-a-Standard-Report-to-the-Service-Manager-Favorite-Reports-Folder.md)  
  
     Describes how to add a standard report.  
  
-   [How to Configure Standard Report Subscriptions](../../../sm/manage/operate/How-to-Configure-Standard-Report-Subscriptions.md)  
  
     Describes how to configure standard report subscriptions.  
  
-   [How to Schedule a Standard Service Manager Report](../../../sm/manage/operate/How-to-Schedule-a-Standard-Service-Manager-Report.md)  
  
     Describes how to schedule a standard [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] report.  
  
-   [How to Add Non\-Service Manager Reports to the Report Catalog](../../../sm/manage/operate/How-to-Add-Non-Service-Manager-Reports-to-the-Report-Catalog.md)  
  
     Describes how to add reports to the report catalog that were not created in [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
-   [Standard Reports Available in Service Manager](../../../sm/manage/operate/Standard-Reports-Available-in-Service-Manager.md)  
  
     Lists the standard reports that are available in [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
## Other Resources for This Component  
  
-   TechNet Library main page for [System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220655)  
  
-   [Operations Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220656)  
  
-   [Administrator's Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209669)  
  
-   [Planning Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209672)