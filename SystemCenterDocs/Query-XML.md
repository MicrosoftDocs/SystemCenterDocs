---
title: Query XML
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79b4b836-e45c-4e2e-b32c-758a82b70eb3
---
# Query XML
The Query XML activity is used to perform an XPath query on an XML file. You can use this activity to search for a string in an XML file.

## Configuring the Query XML Activity
Before you configure the Query XML activity, you need to determine the following:

-   The XML file name or Block of XML that you want to search.

-   The query you will use to perform the search.

Use the following information to configure the Query XML activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**XML File**|Select either this option or the XML Text option. Type the path or URL of the XML file that you want to search in, or click the ellipsis button **\(...\)** and browse for it.|
|**XML Text**|Select either this option or the XML File option. Type the name of the element in the XML text that you want to search in.|
|**XPath Query**|Type the XPath query for your search.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Escaped Query Result|The result of the query.|
|Escaped XML Attributes|The attributes found in the element tag of the query result.|
|The input XML file|The name of the XML file that you are searching in. This item is blank if you used the Block of XML option.|
|The input XML text|The XML text that you searched in. This item is blank if you used the XML File option.|
|The XPath query.|The XPath query that was used in the search.|
|Node count|The number of results published from the query.|

