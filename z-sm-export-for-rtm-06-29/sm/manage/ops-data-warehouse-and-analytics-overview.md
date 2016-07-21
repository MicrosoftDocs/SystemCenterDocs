---
title: Data Warehouse and Analytics Overview
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddc8e977-6df4-4840-bc6a-59a85c52f155
 

















---
# Data Warehouse and Analytics Overview
The data warehouse in System Center 2012 - Service Manager provides three primary functions:  
  
1.  Offload data from the main Service Manager database to improve performance of the Service Manager database  
  
2.  Long\-term data storage  
  
3.  Provide data for reports  
  
 The data warehouse that ships with Service Manager is actually its own management group. It has essentially all the System Center common platform pieces that are present in other System Center components, such as System CenterÂ&nbsp;2012 - Operations Manager. These components are built on the common platform, which in turn consists of the following:  
  
-   A model\-based database for storing configuration information about the data warehouse and for staging the data after it has been extracted from the Service Manager database. In the data warehouse management group, this instance of the mode\-based database is named DWStagingAndConfig.  
  
-   The management server, which consists of the following:  
  
    -   System Center Data Access service  
  
    -   System Center Management service  
  
        > [!NOTE]  
        >  ForSystem Center 2012 R2 Service Manager, the System Center Management service was renamed to Microsoft Monitoring Agent.  
  
    -   System Center Management Configuration service  
  
 In addition to its base that is built on the System Center common platform, the Service Manager data warehouse has two other databases:  
  
-   DWRepository-where the transformed data is stored and optimized for reporting purposes.  
  
-   DWDataMart-where the transformed data is loaded and where, ultimately, reports query from.  
  
 The data warehouse was designed to:  
  
-   Be fully extensible by means of management packs.  
  
-   Utilize data warehousing best practices, such as dimensional modeling with facts and dimensions.  
  
-   Operate at very large scale.  
  
 The data warehouse in System Center 2012 - Service Manager was designed and built with the intention of being a platform component that enables System Center users to collocate data from all System Center products to gain comprehensive insight across their information technology \(IT\) investments.  
  
## The Difference between OLTP and OLAP \(Performing vs. Analyzing Transactions\)  
 Online transaction processing \(OLTP\) systems are designed for fast writes against small units of work-for example, for the fast creation of a single incident. In contrast, online analytical processing \(OLAP\) data warehouses are designed to facilitate fast analysis across large sets of data-for example, quickly determining service level agreement \(SLA\) adherence across all incidents created in the last year.  
  
## Data Warehouse and Analytics Elements  
 The data warehouse and analytics elements of System Center 2012 - Service Manager consist of the System Center common model, data warehouse databases, OLAP cubes, management pack orchestration processes, and the Service Manager software development kit \(SDK\). The following sections describe each of these elements in further detail.  
  
## System Center Common Model and Data Warehouse Database Schema  
 Diagrams that represent the System Center common model and the data warehouse database schema are available for System Center 2012 - Service Manager. The database schema is based on the common management pack model, which means the relational database objects and relationships benefit from class inheritance.  
  
 If you are not familiar with developing management packs, writing custom queries against the data warehouse can be intimidating. However, the schema diagrams are very useful to help get you started. You can download the Visio diagrams, SystemCenterCommonModel\-SCSM2010.vsd and DWDataMart.vsd, as part of the [Service Manager Job aids](http://go.microsoft.com/fwlink/p/?LinkID=186291) \(SM\_job\_aids.zip\). The different types of tables in the data warehouse are color coded in the schema diagram.  
  
## Service Manager Data Warehouse Databases  
 The data warehouse in Service Manager comprises the following databases:  
  
-   DWStagingAndConfig-where data is extracted from source systems, such as Service Manager and Operations Manager, is initially stored.  
  
-   DWRepository-where extracted source data is transformed into the reporting optimized structure.  
  
-   DWDataMart-where published data is stored and gets consumed by the reports. This is also where data is stored for an extended period of time to facilitate historical reporting and analysis.  
  
## OLAP Cubes  
 As mentioned previously, an OLAP cube is used for online analytical processing, and it is a data structure that provides fast analysis of data. You can think of it as helping manipulate and analyze data from multiple perspectives. The cube data structure can help overcome some limitations of relational databases.  
  
 System Center 2012 - Service Manager includes a number of predefined OLAP cubes that users can view in Microsoft Excel and also as SharePoint dashboards. Authors can create their own OLAP cubes for customized data sources and include the cubes in custom management packs.  
  
## Service Manager Software Development Kit  
 The System Center 2012 - Service Manager SDK contains information that you might need when you are authoring with Service Manager to extend the data warehouse so that it can manage your own customized data. Before you can utilize the capabilities of the data warehouse, such as OLAP cube processing for customized data, you must first create a custom management pack and import it. Your custom management pack bundle will contain a definition for your data model and, possibly, OLAP cube definitions.  
  
 You can learn more about using the SDK to create your own custom management pack for Service Manager in the [Authoring Guide for System Center 2012 \- Service Manager](http://go.microsoft.com/fwlink/p/?LinkID=210314). Additionally, you can download the [System Center 2012 \- Service Manager 2012 SDK](http://go.microsoft.com/fwlink/p/?LinkID=196797) at the Microsoft Download Center.
