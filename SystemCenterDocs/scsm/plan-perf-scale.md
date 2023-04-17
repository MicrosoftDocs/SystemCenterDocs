---
title: Plan for System Center - Service Manager performance and scalability
description: This article describes general performance and scalability planning guidance for System Center - Service Manager.
manager: mkluck
ms.prod: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 01/23/2018
ms.technology: service-manager
ms.topic: article
ms.custom: UpdateFrequency3
---

# Plan for System Center - Service Manager performance and scalability

::: moniker range=">= sc-sm-1801 <= sc-sm-1807"

[!INCLUDE [eos-notes-service-manager.md](../includes/eos-notes-service-manager.md)]

::: moniker-end


This article describes general performance and scalability planning guidance for System Center - Service Manager. While Service Manager is built to meet a performance standard on minimum recommended hardware, the hardware requirements for your specific scenario may be higher or lower than the generalized guidelines presented here. This article also describes considerations for Service Manager software.  

 Service Manager is a three\-tiered application, consisting of a database, a data access module, and a console:  

-   Every Service Manager deployment topology—from the largest to smallest—includes all three tiers, whether physically or virtually.  
-   The smallest deployment topology that is supported requires two servers, either physical servers or virtual servers. The largest deployment topology contains more than four servers.  
-   The servers host the Service Manager console and Service Manager database on the management server. The data warehouse management server hosts the Service Manager data warehouse.  

## Service Manager Sizing Helper Tool

 The Service Manager Sizing Helper tool can help you size the hardware and software pieces that you will deploy using the details in this guide. The tool is included in the [Service Manager job aids](https://go.microsoft.com/fwlink/p/?LinkID=232378) documentation set \(SM\_job\_aids.zip\). Although the tool was created for a previous version of Service Manager, its recommendations are still valid.

Specifically, the sizing tool:  

- Helps to give you an idea of the type of hardware, such as individual computers, CPUs, free and used hard drive space, and RAID level, that is needed for different usage and deployment scenarios. Usage is indicated by the number of configuration items in the Service Manager database, work items per month, and days of data in the data warehouse.  
- Provides topology diagrams for each scenario. The diagrams map the hardware to scenarios such as single\-physical\-server, two\-server, four\-server, and more\-than\-four\-server scenarios.  
- Helps you calculate free and used hard drive space that is necessary for a scenario based on your input. The calculation is an estimate, not a fixed value that you must meet.  

## Next steps

[Plan for Service Manager hardware performance](plan-hardware-perf.md).
