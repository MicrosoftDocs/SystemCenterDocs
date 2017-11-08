---
title: Data warehouse reporting and analytics
description: Provides an overview about data warehouse reporting and analytics in Service Manager.
manager: carmonm
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
ms.assetid: 90c721f6-6b0e-4c35-ac85-3fb2e4134ecc
---

# Data warehouse reporting and analytics in Service Manager

Service Manager reports enable you to collect and view data and trends from across the business environment. For example, you can generate a report that shows the number of incidents that occur in a specific time frame. You can then use that information to calculate the cost of each incident \(in hours\) and also to identify any trends and take preventative measures to reduce the cost and occurrence of incidences.  

 Standard reports are viewable for all Service Manager console users in the Reporting workspace. If users can view work items and have permission to the SystemCenter and ServiceManager folders on the SQL&nbsp;Server Reporting Services \(SSRS\) server, they can also view reports in work item task lists. Any user can export report data from a report they view. Exported reports are saved in a variety of file formats.  

## Overview

The data warehouse in Service Manager provides three primary functions:  

1.  Offload data from the main Service Manager database to improve performance of the Service Manager database  

2.  Long\-term data storage  

3.  Provide data for reports  

 The data warehouse that ships with Service Manager is actually its own management group. It has essentially all the System Center common platform pieces that are present in other System Center components, such as System Center - Operations Manager. These components are built on the common platform, which in turn consists of the following:  

-   A model\-based database for storing configuration information about the data warehouse and for staging the data after it has been extracted from the Service Manager database. In the data warehouse management group, this instance of the mode\-based database is named DWStagingAndConfig.  

-   The management server, which consists of the following:  

    -   System Center Data Access service  

    -   Microsoft Monitoring Agent  

    -   System Center Management Configuration service  

 In addition to its base that is built on the System Center common platform, the Service Manager data warehouse has two other databases:  

-   DWRepository-where the transformed data is stored and optimized for reporting purposes.  

-   DWDataMart-where the transformed data is loaded and where, ultimately, reports query from.  

 The data warehouse was designed to:  

-   Be fully extensible by means of management packs.  

-   Utilize data warehousing best practices, such as dimensional modeling with facts and dimensions.  

-   Operate at very large scale.  

 The data warehouse in Service Manager was designed and built with the intention of being a platform component that enables System Center users to collocate data from all System Center products to gain comprehensive insight across their information technology \(IT\) investments.  

### The difference between OLTP and OLAP \(performing vs. analyzing transactions\)  
 Online transaction processing \(OLTP\) systems are designed for fast writes against small units of work-for example, for the fast creation of a single incident. In contrast, online analytical processing \(OLAP\) data warehouses are designed to facilitate fast analysis across large sets of data-for example, quickly determining service level agreement \(SLA\) adherence across all incidents created in the last year.  

### Data warehouse and analytics elements  
 The data warehouse and analytics elements of Service Manager consist of the System Center common model, data warehouse databases, OLAP cubes, management pack orchestration processes, and the Service Manager software development kit \(SDK\). The following sections describe each of these elements in further detail.  

### System Center Common Model and data warehouse database schema  
 Diagrams that represent the System Center common model and the data warehouse database schema are available for Service Manager. The database schema is based on the common management pack model, which means the relational database objects and relationships benefit from class inheritance.  

 If you are not familiar with developing management packs, writing custom queries against the data warehouse can be intimidating. However, the schema diagrams are very useful to help get you started. You can download the Visio diagrams, SystemCenterCommonModel\-SCSM2010.vsd and DWDataMart.vsd, as part of the [Service Manager Job aids](https://go.microsoft.com/fwlink/p/?LinkID=186291) \(SM\_job\_aids.zip\). The different types of tables in the data warehouse are color coded in the schema diagram.  

## Data warehouse databases  
 The data warehouse in Service Manager comprises the following databases:  

-   DWStagingAndConfig-where data is extracted from source systems, such as Service Manager and Operations Manager, is initially stored.  

-   DWRepository-where extracted source data is transformed into the reporting optimized structure.  

-   DWDataMart-where published data is stored and gets consumed by the reports. This is also where data is stored for an extended period of time to facilitate historical reporting and analysis.  

### OLAP cubes  
 As mentioned previously, an OLAP cube is used for online analytical processing, and it is a data structure that provides fast analysis of data. You can think of it as helping manipulate and analyze data from multiple perspectives. The cube data structure can help overcome some limitations of relational databases.  

Service Manager includes a number of predefined OLAP cubes that users can view in Microsoft Excel and also as SharePoint dashboards. Authors can create their own OLAP cubes for customized data sources and include the cubes in custom management packs.  

## Software Development Kit (SDK)
 The Service Manager SDK contains information that you might need when you are authoring with Service Manager to extend the data warehouse so that it can manage your own customized data. Before you can utilize the capabilities of the data warehouse, such as OLAP cube processing for customized data, you must first create a custom management pack and import it. Your custom management pack bundle will contain a definition for your data model and, possibly, OLAP cube definitions.  

## Next steps

 - You can learn more about using the SDK to create your own custom management pack for Service Manager in the [Authoring Guide for System Center 2016 - Service Manager](author-with-sm.md).
 - [Learn about](standard-reports.md) using standard reports.
