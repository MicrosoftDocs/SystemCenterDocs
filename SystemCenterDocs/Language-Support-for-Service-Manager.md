---
title: Language Support for Service Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 890ad168-21bb-4fc2-a669-5f9e1196cea3
---
# Language Support for Service Manager
It is assumed in this guide that you are installing [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] on a computer where no previous version of [!INCLUDE[smshort12](Token/smshort12_md.md)] is installed. For information about upgrading [!INCLUDE[smshort12](Token/smshort12_md.md)], see the [Upgrade Guide for Service Manager 2012 - System Center](http://go.microsoft.com/fwlink/p/?LinkID=209667).

Including English, [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] supports a total of 21 languages. There are some search\-related issues with six languages: Czech, Danish, Finnish, Greek, Polish, and Turkish. For more information about these issues, see the section "Search Issues" in this topic.

Setting your Windows locale on a computer that hosts a [!INCLUDE[smcons](Token/smcons_md.md)] to one of the supported languages results in [!INCLUDE[smshort12](Token/smshort12_md.md)] being displayed in that language. In addition to the languages that [!INCLUDE[smshort12](Token/smshort12_md.md)] supports, you must also consider the ability to search and sort data in the [!INCLUDE[smshort12](Token/smshort12_md.md)] databases. The ability to search and sort data in a specific language is defined by the collation settings in Microsoft SQL Server. For more information about SQL Server collations, see the section "Microsoft SQL Server 2008 with SP1" in [System Requirements for System Center 2012 - Service Manager](assetId:///847fcf88-bee5-49e5-a783-92ed432db3a4) in this guide.

The information in the following table represents the approved collations and the locale identifiers that were tested for [!INCLUDE[smshort12](Token/smshort12_md.md)]. In the list of collations in this table, “CI” indicates case\-insensitive, and “AS” indicates accent\-sensitive.

|Windows locale|Collation|
|------------------|-------------|
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
|Norwegian \(Bokmål, Norway\)|Norwegian\_100\_CI\_AS|
|Polish \(Poland\)|Polish\_100\_CI\_AS|
|Portuguese \(Brazil\)|Latin1\_General\_100\_CI\_AS|
|Portuguese \(Portugal\)|Latin1\_General\_100\_CI\_AS|
|Russian|Cyrillic\_General\_100\_CI\_AS|
|Spanish\_Modern\_Sort|Modern\_Spanish\_100\_CI\_AS|
|Swedish \(Sweden\)|Finnish\_Swedish\_100\_CI\_AS|
|Turkish \(Turkey\)|Turkish\_100\_CI\_AS|

## Search Issues
This section describes search issues, sort issues, and word\-break issues with some of the languages that are supported in [!INCLUDE[smshort12](Token/smshort12_md.md)].

### Greek, Czech, and Finnish Languages
For these languages, full\-text search is not supported in SQL Server 2008. Therefore, sorting and searching activities in these languages do not function correctly.

### Danish, Polish, and Turkish Languages
Full\-text search does not function in SQL Server 2008 or SQL Server 2008 R2 for these languages. You can load a licensed third\-party word breaker that enables full\-text search to function correctly. If you have [!INCLUDE[smcons](Token/smcons_md.md)]s using the Danish, Polish, or Turkish languages, regardless of the language collation that you have selected for your SQL Server installation, you have to install a third\-party word breaker.

For more information, see the following links for the version of SQL Server that you are using:

-   [SQL Server 2008](http://go.microsoft.com/fwlink/?LinkId=205800)

-   [SQL Server 2008 R2](http://go.microsoft.com/fwlink/p/?LinkID=205557)

### Turkish Language
None of the Turkish collations is supported in [!INCLUDE[smshort12](Token/smshort12_md.md)]. The Latin1\_General\_100\_CI\_AS collation was used for testing with the Turkish language. As a result, some search and sort operations in [!INCLUDE[smshort12](Token/smshort12_md.md)] will be affected for some Turkish characters.


