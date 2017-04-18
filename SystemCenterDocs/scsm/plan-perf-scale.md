---
title: Planning for Service Manager performance and scalability
description: This article describes general performance and scalability planning guidance for Service Manager.
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
ms.assetid: 5e89257d-9ec5-411f-b1a4-0b856917ab9d
---

# Planning for System Center 2016 - Service Manager performance and scalability

>Applies To: System Center 2016 - Service Manager

This article describes general performance and scalability planning guidance for System Center 2016 - Service Manager. While Service Manager is built to meet a performance standard on minimum recommended hardware, the hardware requirements for your specific scenario may be higher or lower than the generalized guidelines presented here. This section also describes considerations for Service Manager software.  

 Service Manager is a three\-tiered application, consisting of a database, a data access module, and a console:  

-   Every Service Manager deployment topology-from the largest to smallest-includes all three tiers, whether physically or virtually.  
-   The smallest deployment topology that is supported requires two servers, either physical servers or virtual servers. The largest deployment topology contains more than four servers.  
-   The servers host the Service Manager console and Service Manager database on the management server. The data warehouse management server hosts the Service Manager data warehouse.  

## Service Manager Sizing Helper Tool

 The Service Manager Sizing Helper tool can help you size the hardware and software pieces that you will deploy using the details in this guide. The tool is included in the [Service Manager job aids](http://go.microsoft.com/fwlink/p/?LinkID=232378) documentation set \(SM\_job\_aids.zip\). Although the tool was created for a previous version of Service Manager, its recommendations are still valid for System Center 2016 - Service Manager.

Specifically, the sizing tool:  

- Helps to give you an idea of the type of hardware, such as individual computers, CPUs, free and used hard drive space, and RAID level, that is needed for different usage and deployment scenarios. Usage is indicated by the number of configuration items in the Service Manager database, work items per month, and days of data in the data warehouse.  
- Provides topology diagrams for each scenario. The diagrams map the hardware to scenarios such as single\-physical\-server, two\-server, four\-server, and more\-than\-four\-server scenarios.  
- Helps you calculate free and used hard drive space that is necessary for a scenario, based on your input. The calculation is an estimate, not a fixed value that you must meet.  

## Next steps

- Review [Plan for Service Manager hardware performance](../sm/plan/plan-hardware-performance.md) to learn about general guidelines to consider when you are planning for Service Manager hardware performance.
