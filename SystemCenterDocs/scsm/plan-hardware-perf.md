---
title: Plan for hardware performance
description: Describes planning considerations for Service Manager hardware performance.
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
ms.assetid: 6c28cc61-e50c-4d3b-a26e-9410267278c6
---

# Plan for Service Manager hardware performance

An important part of System Center 2016 - Service Manager performance depends on a hardware configuration and deployment topology that is planned to handle the needs of your organization. The following sections provide general guidelines to consider when you are planning for adequate hardware performance.  

## Hardware performance  

The following are the hardware bottlenecks that are most noticeable in Service Manager, with a significant load and amount of data in the Service Manager database:  

1.  The most common bottleneck is memory and I/O on the computer that is running Microsoft SQL Server. If you have the resources, investing in more memory and a faster I/O subsystem to improve SQL Server I/O will achieve better performance.  
2.  If you expect to have many consoles connecting to a management server, you can improve performance to handle peak load by investing in additional CPUs and memory for the management server or by installing a secondary Service Manager management server.  

Be aware of the recommended minimum hardware for each role, as described in this document.  

### The role of virtual machines  

Many organizations use virtual machines to host Windows Server applications. Service Manager server roles, such as the management server and data warehouse server, are no exceptions. The use of virtual machines might range from all server roles being virtualized to some other combination of virtual and physical computers.  

We do not recommend any specific virtual\-to\-physical\-computer ratio because the needs of your organization are inherently unique. However, the minimum hardware requirements for each software role apply to physical computers. If you decide to virtualize a software role, you should plan to ensure that you have additional hardware resources for each virtual computer.  

Database servers are vulnerable to poor performance on virtual machines if the following planning guidance is not followed:  

-   [Running SQL Server in a Hyper\-V Environment](https://go.microsoft.com/fwlink/p/?LinkID=144622).  
-   You should never use dynamic disks on virtual machines that are intended to host SQL Server. Use fixed\-size virtual hard drives or pass\-through.  
-   Hyper\-V allows only four virtual CPUs per guest, which might constrain the Service Manager server if you have many consoles.  

### Service Manager baseline test results  

Service Manager has been baseline\-tested for performance and scalability using various deployment scenarios with the minimum recommended hardware in the form of physical computers. More specifically, the scenarios were tested with databases prepopulated and Service Manager consoles creating and updating Incidents and Change Requests in a loop.  

The database was prepopulated with information for two tests:  

-   Test 1 consisted of 20,000 computers, 20,000 users, and all the necessary configuration items, which were approximately 250,000 configuration items totaling approximately 2.5 million rows in the database. Test 1 also included 40 active Service Manager consoles.  
-   Test 2 consisted of 50,000 computers, 50,000 users, and related configuration items, which was approximately 700,000 configuration items totaling 6 million rows in the database. Test 2 also included 80 active Service Manager consoles.  

The tests delivered the following results:  

-   To meet the response\-time goals for the 50,000\-computer configuration, the SQL Server memory had to be increased from 8 gigabytes \(GB\) to 32 GB.  
-   During testing, 200 incidents and 50 change requests for the 20,000\-computer configuration and 500 Incidents and 125 Change Requests for the 50,000\-computer configuration were generated each hour, with three to four notification subscriptions and templates being processed for each incident and change request.  
-   Typically, in the baseline testing, workflows, such as notification subscription processing and template application, ran within one minute of each work item being generated.  

If your organization plans to have fewer than 20,000 supported computers and consoles and fewer workflows, your Service Manager performance should be acceptable, even if some of the Service Manager roles are hosted on virtual computers.  

 However, if you plan to add additional supported computers in the Service Manager database, you should plan to increase the amount of RAM for the Service Manager database server beyond the minimum requirements listed in this document. For example, in the baseline test 8 GB of RAM was installed in the Service Manager database server that contained records for 20,000 computers. Afterward, you should add 8 GB of RAM for each increment of 10,000 of computers that you plan to support. For example, for 50,000 computers plan for 32 GB of RAM. During testing of the 50,000\-computer configuration with 32 GB of RAM installed on the computer running SQL Server, performance was improved to a state where there was no longer any decreased effect compared to testing of the configuration before additional computers were added.  

Network latency was also tested in the baseline. Network latency was introduced between the Service Manager console and the Service Manager management server.  

> [!NOTE]  
>  The Service Manager database server and Service Manager management servers should be on a low\-latency LAN; network latency between the Service Manager database server and the Service Manager management server may lead to significant degradation of Service Manager performance.  

 The tests also delivered the following results:  

-   Where network latency was less than 100 milliseconds \(msec\), overall Service Manager console response times were found good.  
-   Where network latency was 150 to 200 msec, performance was noted as usable, with up to a 40\-percent degradation in response time in some scenarios. With latency between 150 to 200 msec, you should plan to evaluate the key scenarios for your organization and determine if Remote Desktop Connection \(RDC\) is a better option.  

    > [!NOTE]  
    >  Expanding service maps in the Service Manager console was slow with any amount of latency.  

-   When network latency exceeded 200 msec, overall Service Manager console response times were observed as poor. If your latency exceeds 200 msec, you should plan to use RDC or another similar remote access solution for operational tasks. However, because occasional administrative tasks are less common you might not need remote access for them.

## Next steps

- Review [Service Manager performance](sm-perf.md) to read general guidelines to consider when you are planning for Service Manager software performance.
