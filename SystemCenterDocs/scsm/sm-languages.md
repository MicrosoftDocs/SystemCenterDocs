---
title: Languages supported by System Center - Service Manager
description: Describes the languages that System Center - Service Manager supports.
manager: evansma
ms.prod: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 01/23/2018
ms.technology: service-manager
ms.topic: reference
---

# Languages supported by System Center - Service Manager

::: moniker range=">= sc-sm-1801 <= sc-sm-1807"

[!INCLUDE [eos-notes-service-manager.md](../includes/eos-notes-service-manager.md)]

::: moniker-end

It is assumed in this article that you are installing System Center - Service Manager on a computer where no previous version of Service Manager is installed.

 Including English,  Service Manager supports a total of 21 languages. Setting your Windows locale on a computer that hosts a Service Manager console to one of the supported languages results in Service Manager being displayed in that language. In addition to the languages that Service Manager supports, you must also consider the ability to search and sort data in the Service Manager databases. The ability to search and sort data in a specific language is defined by the collation settings in Microsoft SQL Server. Learn more about [SQL Server support](supported-configs.md).  

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
