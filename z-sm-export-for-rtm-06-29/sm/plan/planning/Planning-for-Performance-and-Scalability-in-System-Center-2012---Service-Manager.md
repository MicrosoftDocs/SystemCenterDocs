---
title: Planning for Performance and Scalability in System Center 2012 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e89257d-9ec5-411f-b1a4-0b856917ab9d
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Planning for Performance and Scalability in System Center 2012 - Service Manager
This section describes general performance and scalability planning guidance for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)]. While [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] is built to meet a performance standard on minimum recommended hardware, the hardware requirements for your specific scenario may be higher or lower than the generalized guidelines presented here. This section also describes considerations for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] software.  
  
 [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] is a three\-tiered application, consisting of a database, a data access module, and a console:  
  
-   Every [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] deployment topology—from the largest to smallest—includes all three tiers, whether physically or virtually.  
  
-   The smallest deployment topology that is supported requires two servers, either physical servers or virtual servers. The largest deployment topology contains more than four servers.  
  
-   The servers host the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] and [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database on the management server. The data warehouse management server hosts the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse.  
  
## [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Sizing Helper Tool  
 The [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Sizing Helper tool can help you size the hardware and software pieces that you will deploy using the details in this guide. The tool is included in the [Service Manager job aids](http://go.microsoft.com/fwlink/p/?LinkID=232378) documentation set \(SM\_job\_aids.zip\).  
  
 Specifically, the sizing tool:  
  
1.  Helps to give you an idea of the type of hardware, such as individual computers, CPUs, free and used hard drive space, and RAID level, that is needed for different usage and deployment scenarios. Usage is indicated by the number of configuration items in the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database, work items per month, and days of data in the data warehouse.  
  
2.  Provides topology diagrams for each scenario. The diagrams map the hardware to scenarios such as single\-physical\-server, two\-server, four\-server, and more\-than\-four\-server scenarios.  
  
3.  Helps you calculate free and used hard drive space that is necessary for a scenario, based on your input. The calculation is an estimate, not a fixed value that you must meet.  
  
## Planning for Performance and Scalability Topics  
  
-   [Hardware Performance](../../../sm/plan/planning/Hardware-Performance.md)  
  
     Contains general guidelines to consider when you are planning for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] hardware performance.  
  
-   [Service Manager Performance](../../../sm/plan/planning/Service-Manager-Performance.md)  
  
     Contains general guidelines to consider when you are planning for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] software performance.  
  
-   [Configurations for Deployment Scenarios](../../../sm/plan/planning/Configurations-for-Deployment-Scenarios.md)  
  
     Describes hardware and software configurations for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] deployment scenarios.  
  
## Other Resources for This Component  
  
-   TechNet Library main page for [System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220655)  
  
-   [Planning Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209672)  
  
-   [Deployment Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209670)  
  
-   [Administrator’s Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209669)  
  
-   [Operations Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220656)