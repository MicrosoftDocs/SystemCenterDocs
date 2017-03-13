---
title: Cube processing overview
description: Provides an overview of Service Manager OLAP cube processing.
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
ms.assetid: 83f586d7-14f3-498f-9212-92e34c480359
---

# Service Manager OLAP cube processing overview

>Applies To: System Center 2016 - Service Manager

When an online analytical processing \(OLAP\) cube has been deployed and all its partitions have been created, it is ready to be processed so that it is viewable. Processing a cube is the final step after extract, transform, and load \(ETL\) runs. These steps occur as follows:  

1.  Extract: Extract data from the source system  

2.  Transform: Apply functions to conform data to a standard dimensional schema  

3.  Load: Load the data into the data mart for consumption  

4.  Process: Load the data from the data mart into the OLAP cube for browsing  

 Processing of an OLAP cube occurs when all the aggregations for the cube are calculated and the cube is loaded with these aggregations and data. Dimension and fact tables are read, and the data is calculated and loaded into the cube. When you design an OLAP cube, processing must be carefully considered because of the potentially significant effect that processing might have in a production environment where millions of records may exist. A full process of all partitions in such an environment might take anywhere from days to even weeks, which might render the Service Manager infrastructure and cubes unusable to end users. One recommendation is to disable the processing schedule of any cubes that are not being used to reduce the overhead on the system.  

 OLAP cube processing consists of two separate tasks:  

1.  Dimension processing  

2.  Partition processing  

 Each OLAP cube has a corresponding processing job in the Service Manager console, and it runs on a user\-configurable schedule. Each type of processing task is described in the following sections.  

## Dimension processing  
 Whenever a new dimension is added to the SQL Server Analysis Server \(SSAS\) database, a full process must be run on the dimension to bring it to a fully processed state. After a dimension has been processed, however, there is no guarantee that it will be processed again when another cube that targets the same dimension is processed. By not automatically reprocessing the dimension prevents Service Manager from reprocessing every dimension for every cube. This is especially true if the dimension has been recently processed, because it is unlikely that new data exists that has not yet been processed. To optimize processing efficiency, there is a singleton class, which is defined in the Microsoft.SystemCenter.Datawarehouse.OLAP.Base management pack, that is named Microsoft.SystemCenter.Warehouse.Dimension.ProcessingInterval. The following is an example of this class:  

```  
<!-- This singleton class defines the minimum interval of time in minutes that must elapse before a shared dimension is reprocessed. -->   
<ClassType ID="Microsoft.SystemCenter.Warehouse.Dimension.ProcessingInterval" Accessibility="Public" Abstract="false" Base="AdminItem!System.AdminItem" Singleton="true">  
<Property ID="IntervalInMinutes" Type="int" Required="true" DefaultValue="60"/>  
</ClassType>  
```  

 This singleton class contains a property, *IntervalInMinutes*, which describes how often to process a dimension. By default this property is set to 60 minutes. For example, if a dimension was processed at 3:05 P.M. and another cube that targets the same dimension is processed at 3:45 P.M., the dimension will not be reprocessed. One drawback to this approach is the increased likelihood of dimension key errors. A retry mechanism handles dimension key errors to reprocess the dimension and then the cube partition. For more information about processing failures, see the "Common Problems with Debugging and Troubleshooting" section in the [Troubleshooting OLAP Cubes](ops-troubleshooting-olap-cubes.md) topic.  

 After a dimension has been fully processed, incremental processing with *ProcessUpdate* is executed. The only other time that *ProcessFull* is executed is when a dimension schema changes, because it results in the dimension returning to an unprocessed state. Remember that if *ProcessFull* is performed on a dimension, all affected cubes and their partitions will subsequently exist in an unprocessed state and they will have to be fully processed on their next scheduled run.  

## Partition processing  
 Partition processing must be carefully considered because reprocessing a large partition is very slow and it consumes many CPU resources on the server that hosts SSAS. Partition processing generally takes longer than dimension processing. Unlike dimension processing, processing a partition has no side effects on other objects. The only two types of processing that are performed on System Center 2016 - Service Manager OLAP cubes are ProcessFull and ProcessAdd.  

 Similar to dimensions, creating new partitions in an OLAP cube requires a ProcessFull task for the partition to be in a state where it can be queried. Because a ProcessFull task is an expensive operation, you should perform a ProcessFull task only when necessary; for example, when you create a partition or when a row has been updated. In scenarios in which rows have been added and no rows have been updated, Service Manager can perform a ProcessAdd task. To do this, Service Manager uses watermarks and other metadata. Specifically, the etl.cubepartition table and the etl.tablepartition table are queried to determine what type of processing to perform.  

 The following diagram illustrates how Service Manager determines what type of processing to perform based on the watermark data.  

 ![Diagram of cube processing](../media/ops-cubeprocessing.png)  

 When a ProcessAdd task is performed, Service Manager limits the scope of the query using watermarks. For example, if the InsertedBatchId value is 100 and the WatermarkBatchId value is 50, the query loads data only from the data mart where the InsertedBatchId is greater than 50 and less than 100.  

 Finally, it is important to note that Service Manager does not support manual processing of OLAP cubes using SSAS or Business Intelligence Development Studio. Processing cubes outside of the methods that are provided in System Center 2016 - Service Manager, including the Service Manager console and Service Manager cmdlets, will not update the watermark tables. Therefore, it is possible that data integrity problems might occur. If you have accidentally reprocessed the cube manually, one possible workaround is to unprocess the OLAP cube manually in the same manner. Then, the next time Service Manager processes the cube, it will automatically perform a ProcessFull task because partitions will be in an unprocessed state. This will update all watermarks and metadata correctly so that any possible data integrity problems will be fixed.  
