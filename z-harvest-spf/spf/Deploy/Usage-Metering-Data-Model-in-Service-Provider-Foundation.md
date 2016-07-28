---
title: Usage Metering Data Model in Service Provider Foundation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4feebc8a-0622-4261-94d1-c63b3476c856
author:bwren
manager:cfreemanwa
---
# Usage Metering Data Model in Service Provider Foundation
This topic describes how Service Provider Foundation provides usage metering data to portals and clients that connect to its usage metering endpoint.  
  
> [!NOTE]  
> For updated information about usage metering andWindows Azure Pack for Windows Server , see the TechNet wiki article [How to Integrate Your Billing System with the Usage Metering System](http://blogs.technet.com/b/systemcenter/archive/2013/08/01/how-to-integrate-your-billing-system-with-the-usage-metering-system.aspx).  
  
## Overview of usage metering  
Usage metering consists of the following technologies and resources that participate as components of the usage metering system:  
  
-   Data generator  
  
    A resource provider, such as a virtual machine cloud resource provider, that collects and exposes usage metric information. The data is obtained from virtual machines that a tenant uses, thereby creating various categories of metrics including disk capacity and memory usage.  
  
-   Data collector  
  
    The program used by a portal application to periodically collect usage information and store it in the usage database. The portal hoster implements usage metering by using REST\-based JSON queries on a scheduled basis. The data collector expects usage data to be made available according to a data contract adhered to by all the resource providers.  
  
-   Usage database  
  
    The data warehouse repository of usage data, which may be purged of older records after a specified number of days.  
  
-   Usage API  
  
    The code used to transmit and parse usage data. This is a RESTful API and is the only way to extract the data from the usage database. Using JSON queries, service providers can easily adapt usage data into their billing system.  
  
Note that Service Provider Foundation is not listed because it is not required to implement usage metering. Rather, the role of Service Provider Foundation is to collect metrics from all the data warehouses and aggregate them for billing and analysis purposes.  
  
Service Provider Foundation provides usage metering data to any client, such asWindows Azure Pack for Windows Server , that wants to collect it. IaaS metrics inWindows Azure Pack for Windows Server  are provided by VM Clouds resource provider. This data comprises all the usage metering metrics for all the virtual machines that a tenant uses, provided that those virtual machines are being monitored by System Center 2012 Operations Manager  and that the data is being stored in Operations Manager Data Warehouses monitored by an Operations Manager management server.  
  
## Submitting queries  
To obtain usage metering data with a URL that contains a JSON query, as shown the following example:  
  
`https://SPFserver.contoso.com:8090/usage/usage?lastID=0&batchsize=1000`  
  
In the first call, the `lastID` should be zero. There is no limit on the size of a batch. Note that if a batch size is not equal to all the data available, Service Provider Foundation will fulfill other usage metering requests from other clients and then return to that client to provide its next batch.  
  
## Data pulling model  
Service Provider Foundation implements a data pulling model for obtaining metrics. Clients request data in batches. To track the batches and requests, usage metering uses a bookmark that can be either zero \(which means there has been no data collected since the start of tenant's subscription\) or a value that identifies the last record of the batch.  Service Provider Foundation provides this bookmark to be used for subsequent requests by the client.  
  
For each collection cycle, the client collector requests another batch of metered data using the current bookmark as the starting point for the next batch. If the previous batch request returned an empty result set \(because Service Provider Foundation found no usage records to supply\) the collector uses a bookmark of 0.  
  
The result set of usage metering records is provided to the collector in a well\-known data contract.  
  
## Metering Metrics  
The virtual machine usage metrics in the following tables are aggregated using at hour timespan intervals. Service Provider Foundation gathers these metrics for every virtual machine for every tenant subscription registered and aggregates the values.  
  
A record of usage data consists of the following parts:  
  
-   EventID - A new unique Event ID \(watermark\) that is associated with the last record time in returning a batch of usage records to the collector.  
  
-   Resource Id - The measurement of the usage activity.  
  
-   StartTime, EndTime - The start and end times of the hour in which the data was aggregated.  
  
-   ServiceType - Either "Cloud" or "VirtualMacine".  
  
-   SubscriptionID - The subscription ID of the tenant.  
  
-   Properties - These are information fields that define the following:  
  
    -   Subscriber - Subscriber ID.  
  
    -   Metered Service - Either "VM Utilization" or "Cloud Utilization"  
  
    -   VMName - ID of the virtual machine  
  
    -   VNIC - ID of the virtual network adapter.  
  
The following lists the metrics for the four areas of usage metering: memory, CPU, disk, and network. Each table lists the applicable resource IDs that define the metrics of usage data, and includes an example of a record for each type of usage measurement.  
  
**Memory**  
  
**Resource ID:**  MemoryAllocated\-Min; MemoryAllocated\-Max  
  
**Definition:**  Lowest and highest allocated memory size.  
  
```json  
['53'] (  
    EventId =  "54"  
    ResourceId =  "MemoryAllocated-Max"  
    StartTime =  "2012-11-21T00:00:00"  
    EndTime =  "2012-11-21T01:00:00"  
    ServiceType =  "VirtualMachine"  
    SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
    Properties (  
        Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Metered Service =  "VM Utilization"  
        VMName =  "8ce64f27-4764-4d3a-911e-840d32f1d70b"  
    )  
    Resources (  
        MemoryAllocated =  "1024"  
    )  
)  
```  
  
**Resource ID:**  MemoryConsumed\-Min; MemoryConsumed\-Max ; MemoryConsumed\-Median  
  
**Definition:**  Lowest, highest, and median consumed memory size.  
  
```  
['14'] (  
    EventId =  "15"  
    ResourceId =  "MemoryConsumed-Median"  
    StartTime =  "2012-11-20T23:00:00"  
    EndTime =  "2012-11-21T00:00:00"  
    ServiceType =  "VirtualMachine"  
    SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
    Properties (  
        Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Metered Service =  "VM Utilization"  
        VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
    )  
    Resources (  
        MemoryConsumed =  "1024"  
    )  
)  
```  
  
**CPU**  
  
**Resource ID:**  CPUAllocationCount\-Min; CPUAllocationCount\-Max  
  
**Definition:**  Lowest and highest number of allocated CPU cores.  
  
```  
['60'] (  
    EventId =  "61"  
    ResourceId =  "CPUAllocationCount-Max"  
    StartTime =  "2012-11-21T00:00:00"  
    EndTime =  "2012-11-21T01:00:00"  
    ServiceType =  "VirtualMachine"  
    SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
    Properties (  
        Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Metered Service =  "VM Utilization"  
        VMName =  "8ce64f27-4764-4d3a-911e-840d32f1d70b"  
    )  
    Resources (  
        CPUAllocationCount =  "1"  
    )  
)  
```  
  
**Resource ID:**  Median average in percentage of CPU consumption.  
  
**Definition:**  Lowest and highest number of allocated CPU cores.  
  
```  
['10'] (  
    EventId =  "11"  
    ResourceId =  "CPUPercentUtilization-Median"  
    StartTime =  "2012-11-20T23:00:00"  
    EndTime =  "2012-11-21T00:00:00"  
    ServiceType =  "VirtualMachine"  
    SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
    Properties (  
        Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Metered Service =  "VM Utilization"  
        VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
    )  
    Resources (  
        CPUPercentUtilization =  "0"  
    )  
)  
```  
  
**Disk**  
  
**Resource ID:**  CrossDiskIOPerSecond\-Min; CrossDiskIOPerSecond\-Max; CrossDiskIOPerSecond\-Median  
  
**Definition:**  Lowest, highest, and median input\/output per second \(IOPS\) across all attached disks.  
  
```  
['18'] (  
    EventId =  "19"  
    ResourceId =  "CrossDiskIOPerSecond-Median"  
    StartTime =  "2012-11-20T23:00:00"  
    EndTime =  "2012-11-21T00:00:00"  
    ServiceType =  "VirtualMachine"  
    SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
    Properties (  
        Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Metered Service =  "VM Utilization"  
        VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
    )  
    Resources (  
        CrossDiskIOPerSecond =  "8"  
    )  
)  
```  
  
**Resource ID:**  CrossDiskSizeAllocated\-Min; CrossDiskSizeAllocated\-Max  
  
**Definition:**  Lowest, highest, and median input\/output per second \(IOPS\) across all attached disks.  
  
```  
['18'] (  
    EventId =  "19"  
    ResourceId =  "CrossDiskIOPerSecond-Median"  
    StartTime =  "2012-11-20T23:00:00"  
    EndTime =  "2012-11-21T00:00:00"  
    ServiceType =  "VirtualMachine"  
    SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
    Properties (  
        Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Metered Service =  "VM Utilization"  
        VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
    )  
    Resources (  
        CrossDiskIOPerSecond =  "8"  
    )  
)  
```  
  
**Network**  
  
**Resource ID:**  PerNICKBSentPerSecond\-Min; PerNICKBSentPerSecond\-Max; PerNICKBSentPerSecond\-Median; PerNICKBSentPerSecond\-Average  
  
**Definition:**  Lowest, highest, median, and average number bytes sent per second on a network adapter  
  
```  
['3'] (  
    EventId =  "4"  
    ResourceId =  "PerNICKBSentPerSecond-Average"  
    StartTime =  "2012-11-20T23:00:00"  
    EndTime =  "2012-11-21T00:00:00"  
    ServiceType =  "VirtualMachine"  
    SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
    Properties (  
        Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Metered Service =  "VM Utilization"  
        VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
        VNIC =  "B4091DAB-F5A3-49C0-9099-49085B03C1A0"  
    )  
    Resources (  
        PerNICKBSentPerSecond =  "0"  
    )  
)  
```  
  
**Resource ID:**  PerNICKBReceivedPerSecond\-Min; PerNICKBReceivedPerSecond\-Max; PerNICKBReceivedPerSecond\-Median; PerNICKBReceivedPerSecond\-Average  
  
**Definition:**  Lowest, highest, median, and average number bytes received per second on a network adapter  
  
```  
['5'] (  
    EventId =  "6"  
    ResourceId =  "PerNICKBReceivedPerSecond-Max"  
    StartTime =  "2012-11-20T23:00:00"  
    EndTime =  "2012-11-21T00:00:00"  
    ServiceType =  "VirtualMachine"  
    SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
    Properties (  
        Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Metered Service =  "VM Utilization"  
        VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
        VNIC =  "B4091DAB-F5A3-49C0-9099-49085B03C1A0"  
    )  
    Resources (  
        PerNICKBReceivedPerSecond =  "0"  
    )  
)  
```  
  
## Example data result set  
The following data is from an example result set of a 100 metering data records as rendered from a JSON viewer. Only the first 5 and last 5 are show here.  
  
```  
$json => Array (100)  
(  
    ['0'] (  
        EventId =  "1"  
        ResourceId =  "PerNICKBSentPerSecond-Min"  
        StartTime =  "2012-11-20T23:00:00"  
        EndTime =  "2012-11-21T00:00:00"  
        ServiceType =  "VirtualMachine"  
        SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Properties (  
            Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
            Metered Service =  "VM Utilization"  
            VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
            VNIC =  "B4091DAB-F5A3-49C0-9099-49085B03C1A0"  
        )  
        Resources (  
            PerNICKBSentPerSecond =  "0"  
        )  
    )  
    ['1'] (  
        EventId =  "2"  
        ResourceId =  "PerNICKBSentPerSecond-Max"  
        StartTime =  "2012-11-20T23:00:00"  
        EndTime =  "2012-11-21T00:00:00"  
        ServiceType =  "VirtualMachine"  
        SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Properties (  
            Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
            Metered Service =  "VM Utilization"  
            VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
            VNIC =  "B4091DAB-F5A3-49C0-9099-49085B03C1A0"  
        )  
        Resources (  
            PerNICKBSentPerSecond =  "0"  
        )  
    )  
    ['2'] (  
        EventId =  "3"  
        ResourceId =  "PerNICKBSentPerSecond-Median"  
        StartTime =  "2012-11-20T23:00:00"  
        EndTime =  "2012-11-21T00:00:00"  
        ServiceType =  "VirtualMachine"  
        SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Properties (  
            Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
            Metered Service =  "VM Utilization"  
            VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
            VNIC =  "B4091DAB-F5A3-49C0-9099-49085B03C1A0"  
        )  
        Resources (  
            PerNICKBSentPerSecond =  "0"  
        )  
    )  
    ['3'] (  
        EventId =  "4"  
        ResourceId =  "PerNICKBSentPerSecond-Average"  
        StartTime =  "2012-11-20T23:00:00"  
        EndTime =  "2012-11-21T00:00:00"  
        ServiceType =  "VirtualMachine"  
        SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Properties (  
            Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
            Metered Service =  "VM Utilization"  
            VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
            VNIC =  "B4091DAB-F5A3-49C0-9099-49085B03C1A0"  
        )  
        Resources (  
            PerNICKBSentPerSecond =  "0"  
        )  
    )  
    ['4'] (  
        EventId =  "5"  
        ResourceId =  "PerNICKBReceivedPerSecond-Min"  
        StartTime =  "2012-11-20T23:00:00"  
        EndTime =  "2012-11-21T00:00:00"  
        ServiceType =  "VirtualMachine"  
        SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Properties (  
            Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
            Metered Service =  "VM Utilization"  
            VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
            VNIC =  "B4091DAB-F5A3-49C0-9099-49085B03C1A0"  
        )  
        Resources (  
            PerNICKBReceivedPerSecond =  "0"  
        )  
    )  
    ['5'] (  
        EventId =  "6"  
        ResourceId =  "PerNICKBReceivedPerSecond-Max"  
        StartTime =  "2012-11-20T23:00:00"  
        EndTime =  "2012-11-21T00:00:00"  
        ServiceType =  "VirtualMachine"  
        SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Properties (  
            Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
            Metered Service =  "VM Utilization"  
            VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
            VNIC =  "B4091DAB-F5A3-49C0-9099-49085B03C1A0"  
        )  
        Resources (  
            PerNICKBReceivedPerSecond =  "0"  
        )  
    )  
  
    */ . . . skipping records 6-94 . . . */  
  
    ['95'] (  
        EventId =  "96"  
        ResourceId =  "PerNICKBReceivedPerSecond-Max"  
        StartTime =  "2012-11-21T01:00:00"  
        EndTime =  "2012-11-21T02:00:00"  
        ServiceType =  "VirtualMachine"  
        SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Properties (  
            Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
            Metered Service =  "VM Utilization"  
            VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
            VNIC =  "B4091DAB-F5A3-49C0-9099-49085B03C1A0"  
        )  
        Resources (  
            PerNICKBReceivedPerSecond =  "0"  
        )  
    )  
    ['96'] (  
        EventId =  "97"  
        ResourceId =  "PerNICKBReceivedPerSecond-Median"  
        StartTime =  "2012-11-21T01:00:00"  
        EndTime =  "2012-11-21T02:00:00"  
        ServiceType =  "VirtualMachine"  
        SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Properties (  
            Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
            Metered Service =  "VM Utilization"  
            VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
            VNIC =  "B4091DAB-F5A3-49C0-9099-49085B03C1A0"  
        )  
        Resources (  
            PerNICKBReceivedPerSecond =  "0"  
        )  
    )  
    ['97'] (  
        EventId =  "98"  
        ResourceId =  "PerNICKBReceivedPerSecond-Average"  
        StartTime =  "2012-11-21T01:00:00"  
        EndTime =  "2012-11-21T02:00:00"  
        ServiceType =  "VirtualMachine"  
        SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Properties (  
            Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
            Metered Service =  "VM Utilization"  
            VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
            VNIC =  "B4091DAB-F5A3-49C0-9099-49085B03C1A0"  
        )  
        Resources (  
            PerNICKBReceivedPerSecond =  "0"  
        )  
    )  
    ['98'] (  
        EventId =  "99"  
        ResourceId =  "CPUPercentUtilization-Min"  
        StartTime =  "2012-11-21T01:00:00"  
        EndTime =  "2012-11-21T02:00:00"  
        ServiceType =  "VirtualMachine"  
        SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Properties (  
            Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
            Metered Service =  "VM Utilization"  
            VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
        )  
        Resources (  
            CPUPercentUtilization =  "0"  
        )  
    )  
    ['99'] (  
        EventId =  "100"  
        ResourceId =  "CPUPercentUtilization-Max"  
        StartTime =  "2012-11-21T01:00:00"  
        EndTime =  "2012-11-21T02:00:00"  
        ServiceType =  "VirtualMachine"  
        SubscriptionId =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
        Properties (  
            Subscriber =  "75700cd5-893e-4f68-ada7-50ef4668acc6"  
            Metered Service =  "VM Utilization"  
            VMName =  "885339cd-59c2-4312-ab94-1f1d42e38861"  
        )  
        Resources (  
            CPUPercentUtilization =  "0"  
        )  
    )  
)  
```  
  
## See Also  
[Configure Usage Metering in Service Provider Foundation](../../spf/Deploy/Configure-Usage-Metering-in-Service-Provider-Foundation.md)  
[Administering Service Provider Foundation](../../spf/Deploy/Administering-Service-Provider-Foundation.md)  
[Deploying Service Provider Foundation](../../spf/Deploy/Deploying-Service-Provider-Foundation.md)  
  
