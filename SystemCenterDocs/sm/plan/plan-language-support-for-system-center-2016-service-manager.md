---
title: Language Support for System Center 2016 - Service Manager
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
ms.assetid: 19b6c8b8-324b-43b3-afb6-06648a82df50
---

# Language Support for System Center 2016 - Service Manager

>Applies To: System Center 2016 - Service Manager

It is assumed in this guide that you are installing System Center 2016 - Service Manager on a computer where no previous version of Service Manager is installed. For information about upgrading Service Manager, see the [Upgrade Guide for Service Manager 2016 - System Center](../deploy/upgrade-upgrading-system-center-2012-service-manager-to-system-center-2016.md).  

 Including English, System Center 2016 - Service Manager supports a total of 21 languages. There are some search-related issues with six languages: Czech, Danish, Finnish, Greek, Polish, and Turkish. For more information about these issues, see the section "Search Issues" in this topic.  

 Setting your Windows locale on a computer that hosts a Service Manager console to one of the supported languages results in Service Manager being displayed in that language. In addition to the languages that Service Manager supports, you must also consider the ability to search and sort data in the Service Manager databases. The ability to search and sort data in a specific language is defined by the collation settings in Microsoft SQL Server. For more information about SQL Server collations, see the section "Microsoft SQL Server" in [Supported Configurations for System Center 2016 - Service Manager](plan-supported-configurations-for-system-center-2016-service-manager.md) in this guide.  

 The information in the following table represents the approved collations and the locale identifiers that were tested for Service Manager. In the list of collations in this table, "CI" indicates case-insensitive, and "AS" indicates accent-sensitive.  

|Windows locale|Collation|  
|--------------------|---------------|  
|English|Latin1\_General\_100\_CI\_AS|  
|English|SQL\_Latin1\_General\_CP1\_CI\_AS|  
|English|Latin1\_General\_CI\_AS|  
|Chinese\_PRC|Chinese\_Simplified\_Pinyin\_100\_CI\_AS|  
|Chinese \(Traditional, Taiwan\)|Chinese\_Traditional\_Stroke\_Count\_100\_CI\_AS|  
|Czech \(Czech Republic\)|Czech\_100\_CI\_AS|  
|Danish \(Denmark\)|Danish\_Norwegian\_CI\_AS|  
|Dutch \(Netherlands\)|Latin1\_General\_100\_CI\_AS|  
|Finnish \(Finland\)|Finnish\_Swedish\_100\_CI\_AS|  
|French|French\_100\_CI\_AS|  
|German\_Standard|Latin1\_General\_100\_CI\_AS|  
|Greek \(Greece\)|Greek\_100\_CI\_AS|  
|Hungarian|Hungarian\_100\_CI\_AS|  
|Italian\_Standard|Latin1\_General\_100\_CI\_AS|  
|Japanese|Japanese\_XJIS\_100\_CI\_AS|  
|Korean|Korean\_100\_CI\_AS|  
|Norwegian \(Bokml, Norway\)|Norwegian\_100\_CI\_AS|  
|Polish \(Poland\)|Polish\_100\_CI\_AS|  
|Portuguese \(Brazil\)|Latin1\_General\_100\_CI\_AS|  
|Portuguese \(Portugal\)|Latin1\_General\_100\_CI\_AS|  
|Russian|Cyrillic\_General\_100\_CI\_AS|  
|Spanish\_Modern\_Sort|Modern\_Spanish\_100\_CI\_AS|  
|Swedish \(Sweden\)|Finnish\_Swedish\_100\_CI\_AS|  
|Turkish \(Turkey\)|Turkish\_100\_CI\_AS|  
