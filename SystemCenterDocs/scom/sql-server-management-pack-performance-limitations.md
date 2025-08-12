---
ms.assetid: bba9d228-4b0b-4d37-9423-dd54c9499bcf
title: Monitoring Performance and Limitations in Management Pack for SQL Server
description: This article explains monitoring performance metrics and limitations in Management Pack for SQL Server
author: Anastas1ya
ms.author: jsuri
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Monitoring Performance and Limitations

Management Pack for SQL Server occupies certain amount of memory and CPU capacity in order to monitor your SQL environment. The following table provides statistics on memory and CPU consumption per SKU type, depending on the number of databases being monitored.

>[!NOTE]
>The metrics below are applicable to Management Pack for SQL Server only; capacities that are consumed by other resources aren't considered in this table. Also, Management Pack for SQL Server supports monitoring of no more than 2300 databases on a single instance and no more than 50 SQL Server instances on a single machine.

|SKU type|Total v-cores|RAM (GB)|SQL Server edition|Number of monitored databases per DB Engine|Database supports In-Memory OLTP*|Total CPU utilization|Total memory reserved|
|-|-|-|-|-|-|-|-|
|Standard DS3_v2|4|14|2012 SP4 Enterprise|300|No|3%|36%|
|Standard DS3_v2|4|14|2014 SP3 Enterprise|300|Yes|4%|50%|
|Standard DS3_v2|4|14|2016 SP1 Enterprise|300|Yes|6%|57%|
|Standard DS3_v2|4|14|2017 Enterprise|300|Yes|10%|64%|
|Standard DS3_v2|4|14|2019 Enterprise|300|Yes|8%|64%|
|Standard DS3_v2|4|14|2012 SP4 Enterprise|600|No|4%|50%|
|Standard DS3_v2|4|14|2014 SP3 Enterprise|600|Yes|7%|64%|
|Standard DS3_v2|4|14|2016 SP1 Enterprise|600|Yes|12%|79%|
|Standard DS3_v2|4|14|2017 Enterprise|600|Yes|14%|86%|
|Standard DS3_v2|4|14|2019 Enterprise|600|Yes|51%|88%|
|Standard D8s_v3|8|32|2012 SP4 Enterprise|1000|No|9%|44%|
|Standard D8s_v3|8|32|2014 SP3 Enterprise|1000|Yes|10%|47%|
|Standard D8s_v3|8|32|2016 SP1 Enterprise|1000|Yes|9%|63%|
|Standard D8s_v3|8|32|2017 Enterprise|1000|Yes|9%|72%|
|Standard D8s_v3|8|32|2019 Enterprise|1000|Yes|8%|78%|
|Standard D16as_v4|16|64|2012 SP4 Enterprise|2000|No|5%|19%|
|Standard D16as_v4|16|64|2014 SP3 Enterprise|2000|Yes|60%|25%|
|Standard D16as_v4|16|64|2016 SP1 Enterprise|2000|Yes|11%|70%|
|Standard D16as_v4|16|64|2017 Enterprise|2000|Yes|26%|78%|
|Standard D16as_v4|16|64|2019 Enterprise|2000|Yes|10%|55%|

*The **Database supports In-Memory OLTP** column indicates whether databases of the given SKU type have [Memory-optimized tables](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdocs.microsoft.com%2Fsql%2Frelational-databases%2Fin-memory-oltp%2Foverview-and-usage-scenarios&data=04%7C01%7Cv-tdzakhov%40microsoft.com%7C81a55efbd8ac4fd6e88608d97391236c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637667889479347597%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C1000&sdata=J6M4FzU8FvlTMXi7hXz3ra%2FDK7u9MLgTPQiZNY4itP0%3D&reserved=0).
