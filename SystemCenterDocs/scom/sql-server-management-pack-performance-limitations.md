---
ms.assetid: bba9d228-4b0b-4d37-9423-dd54c9499bcf
title: Monitoring Performance and Limitations
description: This article explains monitoring performance metrics and limitations in Management Pack for SQL Server
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 9/2/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Monitoring Performance and Limitations

Management Pack for SQL Server occupies certain amount of memory and CPU capacity in order to monitor your SQL environment. The following table provides statistics on memory and CPU consumption, depending on the number of databases being monitored by different SKU types.

>[!NOTE]
>Metrics below are applicable to Management Pack for SQL Server only; capacities that are consumed by other management packs and resources are not considered in this table. Also, Management Pack for SQL Server is capable of monitoring 2300 databases per instance and no more than 50 instances per SQL server.

|SKU type|Total v-cores|RAM (GB)|SQL Server edition|Number of monitored databases per DB Engine|Database supports In-Memory OLTP|Total CPU utilization|Total memory reserved|
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
|Standard D16as_v4|16|64|2012 SP4 Enterprise|2000|No|||
|Standard D16as_v4|16|64|2014 SP3 Enterprise|2000|Yes|||
|Standard D16as_v4|16|64|2016 SP1 Enterprise|2000|Yes|||
|Standard D16as_v4|16|64|2017 Enterprise|2000|Yes|||
|Standard D16as_v4|16|64|2019 Enterprise|2000|Yes|||