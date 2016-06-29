---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Language Support for Service Manager
ms.technology:  service-manager
ms.assetid:  890ad168-21bb-4fc2-a669-5f9e1196cea3
---

# Language Support for Service Manager

>Applies To: System Center 2016 Technical Preview - Service Manager

It is assumed in this guide that you are installing System Center 2016 Technical Preview - Service Manager on a computer where no previous version of Service Manager is installed. For information about upgrading Service Manager, see the [Upgrade Guide for Service Manager 2012 - System Center](http://go.microsoft.com/fwlink/p/?LinkID=209667).

Including English, System Center 2016 Technical Preview - Service Manager supports a total of 21 languages. There are some search-related issues with six languages: Czech, Danish, Finnish, Greek, Polish, and Turkish. For more information about these issues, see the section "Search Issues" in this topic.

Setting your Windows locale on a computer that hosts a Service Manager console to one of the supported languages results in Service Manager being displayed in that language. In addition to the languages that Service Manager supports, you must also consider the ability to search and sort data in the Service Manager databases. The ability to search and sort data in a specific language is defined by the collation settings in Microsoft SQL Server.

The information in the following table represents the approved collations and the locale identifiers that were tested for Service Manager. In the list of collations in this table, `_CI_` indicates case-insensitive, and `_AS_` indicates accent-sensitive.

|Windows locale|Collation|
|------------------|-------------|
|English|Latin1_General_100_CI_AS|
|English|SQL_Latin1_General_CP1_CI_AS|
|English|Latin1_General_CI_AS|
|Chinese_PRC|Chinese_Simplified_Pinyin_100_CI_AS|
|Chinese (Traditional, Taiwan)|Chinese_Traditional_Stroke_Count_100_CI_AS|
|Czech (Czech Republic)|Czech_100_CI_AS|
|Danish (Denmark)|Danish_Norwegian_CI_AS|
|Dutch (Netherlands)|Latin1_General_100_CI_AS|
|Finnish (Finland)|Finnish_Swedish_100_CI_AS|
|French|French_100_CI_AS|
|German_Standard|Latin1_General_100_CI_AS|
|Greek (Greece)|Greek_100_CI_AS|
|Hungarian|Hungarian_100_CI_AS|
|Italian_Standard|Latin1_General_100_CI_AS|
|Japanese|Japanese_XJIS_100_CI_AS|
|Korean|Korean_100_CI_AS|
|Norwegian (Bokmål, Norway)|Norwegian_100_CI_AS|
|Polish (Poland)|Polish_100_CI_AS|
|Portuguese (Brazil)|Latin1_General_100_CI_AS|
|Portuguese (Portugal)|Latin1_General_100_CI_AS|
|Russian|Cyrillic_General_100_CI_AS|
|Spanish_Modern_Sort|Modern_Spanish_100_CI_AS|
|Swedish (Sweden)|Finnish_Swedish_100_CI_AS|
|Turkish (Turkey)|Turkish_100_CI_AS|

## Search Issues
This section describes search issues, sort issues, and word-break issues with some of the languages that are supported in Service Manager.

### Greek, Czech, and Finnish Languages
For these languages, full-text search is not supported in SQL Server 2008. Therefore, sorting and searching activities in these languages do not function correctly.

### Danish, Polish, and Turkish Languages
Full-text search does not function in SQL Server 2008 or SQL Server 2008 R2 for these languages. You can load a licensed third-party word breaker that enables full-text search to function correctly. If you have Service Manager consoles using the Danish, Polish, or Turkish languages, regardless of the language collation that you have selected for your SQL Server installation, you have to install a third-party word breaker.

For more information, see the following links for the version of SQL Server that you are using:

-   [SQL Server 2008](http://go.microsoft.com/fwlink/?LinkId=205800)

-   [SQL Server 2008 R2](http://go.microsoft.com/fwlink/p/?LinkID=205557)

### Turkish Language
None of the Turkish collations is supported in Service Manager. The Latin1_General_100_CI_AS collation was used for testing with the Turkish language. As a result, some search and sort operations in Service Manager will be affected for some Turkish characters.
