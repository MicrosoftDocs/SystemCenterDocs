---
title: About Data Warehouse Module Deployment
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c7dd72b4-65f1-426b-a700-d54afe55af44
---
# About Data Warehouse Module Deployment
Data warehouse module deployment in Service Manager starts when a [!INCLUDE[smshort](Token/smshort_md.md)] management server is registered to a data warehouse management server. The following sections describe module parts, functions, and schedule.

## Management Pack Synchronization
Management pack synchronization is the process by which the data warehouse discovers what classes and relationships exist in source systems. This process is also referred to as MPSync. For every management pack that defines a class or relationship, the data warehouse creates extract job modules to retrieve the data for that class or relationship from the corresponding source. Such management packs and their associated jobs are synchronized between the systems.

Only sealed management packs, and their corresponding data, are synchronized into the data warehouse. If you alter a management pack, you must increase the version number and you cannot introduce any changes that might cause errors; otherwise, the management pack will fail to import. For example, you cannot remove classes, remove properties, or remove relationships. Similarly, you cannot change data types in unsupported ways. For example, you cannot modify a string property to become a numeric property.

By default, the MPSync Orchestration job runs every 30 minutes.

It is possible that multiple sources may refer to the same management pack. The version in the source system must be the same or higher version than that in the data warehouse, otherwise registration will fail.

It is possible to remove management packs from the data warehouse. However, keep the following points in mind:

1.  Removing management packs does not delete the data from the data warehouse as it does in the  [!INCLUDE[smshort](Token/smshort_md.md)] database; instead, the database view that users are granted access to is dropped.

2.  If you reimport a management pack after you have removed the corresponding management pack, the historical data is exposed once again.

    > [!NOTE]
    > Only sealed management packs are synchronized from [!INCLUDE[smshort](Token/smshort_md.md)] to the data warehouse. An exception to this is list items, also known as enumerations. Groups or queues are synchronized to the data warehouse, regardless of whether they are in a sealed or unsealed management pack.

Management packs that are imported from [!INCLUDE[smshort](Token/smshort_md.md)] are [!INCLUDE[smshort](Token/smshort_md.md)]–specific and data warehouse specific. The [!INCLUDE[smshort](Token/smshort_md.md)] management packs provide awareness of what the [!INCLUDE[smshort](Token/smshort_md.md)] database is structured like, and the data warehouse management packs drive the structure and processes of the data warehouse databases.

## Report Deployment
The management pack synchronization process imports management packs from [!INCLUDE[smshort](Token/smshort_md.md)], and it defines how those management packs shape the structure, move the data, and copy reports for the data warehouse and reporting. After those management packs are synchronized between [!INCLUDE[smshort](Token/smshort_md.md)] and the data warehouse, the data is retrieved and reports are deployed for user consumption.

Sequentially, report deployment occurs in the following process:

1.  After all identified management packs are synchronized with data warehouse, management pack synchronization triggers the report deployment workflow.

2.  Because the DWStagingandConfig database is the final destination of the management packs that have been synchronized, the deployment workflow queries the DWStagingandConfig database for any new or changed reports to deploy or any reports to remove.

3.  The deployment workflow then publishes any new or updated reports to the SQL Server Reporting Services \(SSRS\) server through the SSRS web services.

4.  SSRS stores the reports and appropriate metadata.

5.  Schema deployment workflow is triggered by management pack synchronization.

6.  Once again, information that causes schema changes is retrieved from the DWStagingandConfig database based on the newly synchronized management packs that are causing the changes.

7.  Schema changes are deployed to the DWRepository database.

8.  Any necessary changes to extract, transform, and load \(ETL\) modules are made to the DWStagingandConfig database.

Management packs that contain only [!INCLUDE[smshort](Token/smshort_md.md)]–specific information do not cause the deployment activities to execute. They are only be triggered for new data warehouse and reporting\-specific elements.

## Understanding the ETL Processes
After the data warehouse schema and reports are deployed, the DWDataMart database is populated with actual data for reporting purposes. This is done by the ETL processes. These three processes each serve their own specific purpose:

-   **Extract** is designed specifically for processing large volumes of data from multiple sources, and it allows for moving data into an area that is built for manipulating the data.

-   **Transform** is designed for optimization of complex logic and integration operations. This process is where most of the ETL work occurs.

-   **Load** is designed for transferring the data that has already been processed into its target destination in a bulk manner.

One of the main reasons for having three different databases is so that you can optimize your hardware environment more easily. In high\-volume environments, the DWStagingandConfig and DWRepository databases must be on computer hardware that is optimized for read\/write I\/O. However, the computer hardware hosting the DWDatamart database must be optimized for read I\/O. With that difference in mind, you can separate the DWDatamart to a different server or drive from the DWStagingandConfig and DWRepository databases. However, the DWStagingandConfig and DWRepository databases must remain on the same server.

At a high level, ETL occurs in the processes described in the following sections. If you plan on authoring management packs that are used for custom reporting, you will probably need to know more about these processes in depth.

### Extract
The extract process starts on a scheduled interval. Extract is the process that retrieves raw data from your online transaction processing system \(OLTP\) store, which in this case is the  [!INCLUDE[smshort](Token/smshort_md.md)] database.

1.  The extract process queries [!INCLUDE[smshort](Token/smshort_md.md)] for the delta data that has accumulated since the last time the extract process ran.

2.  The new data is written into the DWStagingandConfig database in the same basic form as it is in the [!INCLUDE[smshort](Token/smshort_md.md)] database.

### Transform
The transform process starts on a scheduled interval. Transform is the process that moves the raw data from the DWStagingandConfig database. It also does any cleansing, reformatting, and aggregation that is required to alter the raw data into the final format for reporting. This transformed data is written into the DWRepository database.

### Load
The load process starts on a scheduled interval. The load process queries for the data from the DWRepository database. The transformed data from DWRepository is inserted into the DWDatamart database. The DWDatamart is the database that is used for all end\-user reporting needs.


