---
title: Maintaining OLAP Cubes
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b350f9b3-622d-49b4-849a-5e6bf0e199fa
 

















---
# Maintaining OLAP Cubes
The information in the following sections describes maintenance best practices for online analytical processing \(OLAP\) cubes.  
  
## Periodically Reprocess Analysis Services Dimensions  
 SQL Server Analysis Services \(SSAS\) best practices recommend that SSAS dimensions should be fully processed periodically. Fully processing the dimensions rebuilds indices and optimizes the data storage of multidimensional data, which improves query and cube performance that can degrade over time. This is similar to periodically defragmenting a hard disk on a computer.  
  
 However, a drawback to fully processing an SSAS dimension is that all affected OLAP cubes become unprocessed, and they must also be fully processed to return them to the state in which you can query them. System Center 2012 - Service Manager does not explicitly fully process on SSAS dimensions. Therefore, you must decide when to perform this maintenance task.  
  
## Memory Considerations  
 If you run all data warehouse extraction, transformation, and load \(ETL\) operations and OLAP cube functions on one server, carefully consider the memory needs of the operating system, data warehouse, and SSAS to ensure that the server can handle all the data\-intensive operations that can run concurrently. This is especially important because processing OLAP cubes is a memory\-intensive operation.  
  
 For more information, review hardware requirements and guidelines in the [Planning Guide for System Center 2012 \- Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209672). Also review the [SQL Server 2008 R2 Analysis Services Operations Guide](http://go.microsoft.com/fwlink/p/?LinkId=246715).  
  
## See Also  
 [Understanding OLAP Cubes](../../../sm/manage/operate/Understanding-OLAP-Cubes.md)
