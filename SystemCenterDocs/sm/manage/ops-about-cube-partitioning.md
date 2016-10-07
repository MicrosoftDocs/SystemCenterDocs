---
title: About Cube Partitioning
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 59124728-3fea-4acf-b17d-839ebefbf092
---

# About Cube Partitioning

>Applies To: System Center 2016 - Service Manager

Each measure group in a cube is divided into partitions, where a partition defines a portion of the fact data that is loaded into a measure group. SQL Server Analysis Services \(SSAS\) on SQL&nbsp;Server Standard Edition allows only one partition per measure group, while multiple partitions are allowed in the Enterprise Edition. Partitions are completely transparent to the end user, but they have an important impact on performance and scalability. For example, partitions can be processed separately and in parallel. They can have different aggregation designs. You can reprocess a partition without affecting all the other partitions in a measure group. Also, SSAS automatically scans only the partitions that contain the necessary data for a query, which can vastly improve query performance.  

 Cube partitioning is performed on every data warehouse maintenance job run, which is hourly by default. The specific process module that runs is named ManageCubePartitions. It always runs after the CreateMartPartitions step. This dependency data is stored in the infra.moduletriggercondition table.  

 The main dynamic link library \(DLL\), which handles partitioning, is in the warehouse utility DLL, Microsoft.EnterpriseManagement.Warehouse.Utility, in the PartitionUtil class. Specifically, there is a ManagePartitions\(\) method in the class that handles all partition maintenance. The data warehouse maintenance DLL, Microsoft.EnterpriseManagement.Warehouse.Maintenance, and the data warehouse online analytical processing \(OLAP\) DLL, Microsoft.EnterpriseManagement.Warehouse.Olap, both call into Microsoft.EnterpriseManagement.Warehouse.Utility to handle partitions during maintenance and cube deployment. This is why actual partition handling is in the common warehouse utility DLL to avoid duplicating logic or code.  

 Cube Partitioning Maintenance performs the following tasks:  

-   Create partitions  

-   Delete partitions  

-   Update partition boundaries  

 To do this, the Structured Query Language \(SQL\) table etl.TablePartition is read to determine all the fact partitions that have been created for a measure group. The following actions occur:  

1.  Start cube processing for each measure group in the cube  

2.  Get all partitions from the etl.TablePartition table for the measure group  

3.  Delete any partitions that exist in the measure group but that are missing from the etl.TablePartition table  

4.  Add any new partitions that have been created and that exist only in the etl.TablePartition table  

5.  Update any partition that might have changed by matching each partition to the RangeStartDate and RangeEndDate in the etl.TablePartition table  

 Remember the following about cube processing:  

-   Only measure groups that are targeted at facts contain multiple partitions in SQL&nbsp;Server Standard Edition. By default, all measure groups and dimensions contain only one partition. Therefore, the partition does not have any boundary conditions.  

-   The partition boundaries are defined by a query binding that is based on datekeys that match up to the datekeys for the corresponding fact partition in the etl.TablePartition table.  
