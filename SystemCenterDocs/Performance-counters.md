---
title: Performance counters
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3865a73-6613-46d0-88c8-6ef2a38919c4
---
# Performance counters
You can use performance counters when monitoring [!INCLUDE[dpm2012long](Token/dpm2012long_md.md)]. The following table summarizes the counters. To open the Performance tool to work with counters, click **Start**, point to **Administrative Tools**, and then click **Performance**. On the **Action** menu, click **Help**.

### DPM performance counters

|Performance Object and Counter|Description|Value That Might Indicate a Problem|Possible Causes|
|----------------------------------|---------------|---------------------------------------|-------------------|
|Memory: Avail\/MBytes|Measures the memory that is available to processes running on the specified [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server. The Avail\/MBytes value is the sum of memory assigned to the standby \(cached\), free, and zero\-paged lists.|< 50 megabytes \(MB\).<br /><br />Indicates low memory on [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server.|-   One or more applications are consuming large amounts of memory.<br />-   Multiple [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] jobs are running simultaneously.<br />-   The [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server does not have sufficient memory to handle the current [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] workload.|
|Processor: % Processor Time|Measures the percentage of time the processor was busy during the sampling interval.|> 95% for more than 10 minutes.<br /><br />Indicates very high CPU usage on the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server.|-   Multiple [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] jobs are running simultaneously. Synchronization with consistency check jobs are particularly CPU\-intensive.<br />-   On\-the\-wire compression has been enabled on the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server. On\-the\-wire compression allows faster data throughput without negatively affecting network performance. However, it places a large processing load on both the protected computer and the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server.<br />-   A runaway process is exhausting system resources.<br />-   The [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server does not have sufficient processing capacity to handle the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] workload.|
|Physical Disk: Current Disk Queue Length \(for all instances\)|Measures the number of disk requests that are currently waiting and the requests currently being serviced.|> 80 requests for more than 6 minutes.<br /><br />Indicates possibly excessive disk queue length.|-   Multiple [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] jobs that are running simultaneously are placing a high demand on disk resources.<br />-   Disk performance needs tuning.<br />-   Disk resources on the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server are not sufficient for the current [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] workload.|

## See Also
[Tweak performance settings](Tweak-performance-settings.md)


