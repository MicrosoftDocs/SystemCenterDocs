---
title: Troubleshoot OLAP cubes
description: Explains how you can troubleshoot Service Manager OLAP cubes.
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
ms.assetid: dfabe723-15b7-40e0-923a-66819be1e93c
---

# Troubleshoot Service Manager OLAP cubes

>Applies To: System Center 2016 - Service Manager

The following sections describe common problems that you might need to troubleshoot online analytical processing \(OLAP\) data cubes in the Service Manager data warehouse.  

## Processing failures  
 Although safeguards exist in the DWRepository database to ensure data integrity, they cannot completely prevent the possibility of a processing error. The most common processing error is a DimensionKeyNotFound exception. Because SQL&nbsp;Server Analysis Server \(SSAS\) dimensions are processed every 60 minutes by default, it is possible that, while processing the fact's measure group, the dimension keys do not yet exist. In this case, by default the processing logic reprocesses the SSAS dimensions using a ProcessUpdate task and then reprocesses the fact up to two times to resolve the key errors.  

 There are some uncommon situations in which the reprocessing might fail. The following are possible causes of this failure:  

-   Only the data warehouse Repository enforces foreign keys to ensure the integrity of the data. The data mart does not have any foreign keys for performance considerations. Because the load process bulk moves the data from the repository to the data mart using ActiveX Data Objects methods, it is possible that the fact data may have been loaded before the dimension keys as a result of a timing problem. To resolve this problem, the load process must be run again to move the existing dimension keys.  

-   In multiple data mart situations, all the dimensions of each data mart target the primary data warehouse data mart. This is to reduce the size and processing time of the OLAP cubes. It is possible, however, for facts in the Operations Manager or Configuration Manager data marts to target dimension keys that do not yet exist in the primary data warehouse data mart. In this case, you must run the load job on the primary data mart to resolve the processing failure for cubes that target the Operations Manager or Configuration Manager data marts.  

## Troubleshoot MDX customizations  
 Because many cube customizations require a working knowledge of Multidimensional Expressions \(MDX\), it is common for syntax errors to occur in the initial MDX expression that is used for OLAP cube customization. Multiple attempts may be necessary before the expression is suitable for your needs. You should test the MDX expression on the OLAP cube using Business Intelligence Development Studio \(BIDS\) or SSAS, without saving the changes, before you add the MDX expression to the OLAP cube using a CubeExtension or defining it in the SystemCenterCube element.  

 However, if you do have an error in the MDX expression when you add it in a management pack by using a CubeExtension, you can uninstall the cube extension to revert any changes that were made on the OLAP cube. If the expressions are defined using a SystemCenterCube element, you must uninstall the management pack and then manually delete the OLAP cube from SSAS before you make any corrections and redeploy the OLAP cube management pack. Because of this, you should define cube customizations by using the CubeExtension element.  

## OLAP Cube management pack deployment failures  
 You may have a situation in which you want to browse the *WorkItems Assigned To User* measure group and then you want to slice on all users in a particular department. When you attempt to perform filter on *UserDim*, nothing happens or no data is returned. This might be very confusing because *UserDim* has a relationship to the measure group.  

 In this situation, remember that the same database dimension can have multiple roles in the multidimensional model. We call these dimensions role\-playing dimensions. For example, the time dimension can be used multiple times in an OLAP cube that describes flight information. The different role\-playing dimensions in this case could be *Departure Time* and *Arrival Time*, where both target the *Time* dimension.  

 In a *WorkItems Assigned To User* example, the given role\-playing name of the user dimension is actually *AssignedToUser*. If the user filtered by this particular dimension instead of "UserDim", they would return the correct information.  

 BIDS has a useful feature called a Dimension Usage tab that shows the relationships between dimensions and OLAP cubes so that you can determine which dimensions you can use to slice and dice the OLAP cube. Furthermore, in the *WorkItems Assigned To User* example, *UserDim* has no relationship to the *WorkItemAssignedToUser* measure group, while *UserDim\(AssignedToUser\)* does have a relationship to the measure group where the join attribute is UserDimKey. In this case, you can see the role\-playing name is highlighted within the parentheses of the Dimension Usage tab.  

 Service Manager does not have a Dimension Usage tab capability. Therefore, you will have to look at BIDS to determine exactly which dimensions can filter on a particular cube.  

## Failure to process OLAP cubes on a remote SSAS server  
 In certain situations, processing an OLAP cube on a remote SSAS server might fail because the firewall has not been configured properly. The default instance of SSAS uses TCP\/IP port 2383, and this port must be unblocked in the firewall to allow access. To unblock the port, run the following command\-line instructions:  

```  
C:\Windows\system32>set port=2383   
C:\Windows\system32>netsh advfirewall firewall add rule name="Analysis Services" protocol=TCP dir=in localport=2383 action=allow  
```  

## OLAP cube processing stops  
 There can be many causes for OLAP cube processing to stop. You must first ensure that the server has enough RAM, especially in situations in which the data warehouse and the SSAS server are hosted on the same server, so that there is enough memory to run data warehouse extraction, transformation, and load \(ETL\) and cube processing jobs concurrently. A few potential solutions are listed here:  

1.  There are known deadlock problems in Microsoft SQL&nbsp;Server&nbsp;2008 Analysis Services. The workaround is to increase the number of threads in the processing thread pool before the processing stops. If the system is already stopped, the workaround is to restart both the System Center Management service and the Analysis Services service and then reset the cube processing workitem to a status of 3, which means not started, so that the Service Manager workflow engine can restart it.  

    > [!NOTE]  
    >  To determine the relevant cube processing workitem, you can run the following queries on the DWStagingAndConfig database. Note that these queries are shown individually; however, you can easily join them together in one query:  

    ```  
    select processId from infra.process where processname like 'Process.{CubeName}'  
    select batchid from infra.batch where processId = {ProcessId from previous query}  
    select * from infra.workitem(nolock) where BatchId = {BatchId from previous query}  
    update infra.workitem set statusid = 3 where workitemId = {workitemId from previous query)  

    ```  

2.  Check the CoordinatorExecutionMode property on the SSAS service, and ensue that it is set properly. You can read more about this problem on the [SQL Server forums](https://go.microsoft.com/fwlink/p/?LinkId=403946).  

## The DWMaintenance task stops on the ManageCubePartitions or ManageCubeTranslations step  
 In this situation, the most common cause is a nonresponsive SSAS server. The workaround is the same for the first step in the previous section, "OLAP Cube Processing Stops." To determine the relevant cube processing workitem, you can run the following queries on the DWStagingAndConfig database. Note that these queries are shown individually; however, you can easily join them together in one query:  

```  
select processid from infra.process where processname = 'DWMaintenance'  
select * from infra.ProcessModule where ProcessId = {ProcessId from previous query} (Note the ProcessModuleId where the VertexName is ManageCubePartitions/ManageCubeTranslaions)  
Select * from infra.batch where ProcessId = {ProcessId from previous query} (Note the BatchId from the largest batch)  
select * from infra.WorkItem where BatchId = {BatchId from previous query}  
update infra.workitem set statusid = 3 where workitemId = {workitemId for the step that is hung with the corresponding processmoduleid for ManageCubePartitions/ManageCubeTranslations)  

```  

## Next steps

- [Create an OLAP cube using a management pack](create-olap-cube-mps.md).
