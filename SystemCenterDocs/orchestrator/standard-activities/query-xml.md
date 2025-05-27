---
title: Query XML 
description: This article describes the Query XML activity that is used to perform an XPath query on an XML file.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 79b4b836-e45c-4e2e-b32c-758a82b70eb3
caps.latest.revision: 12
author: jyothisuri
ms.author: jsuri
---
# Query XML

The Query XML activity is used to perform an XPath query on an XML file. You can use this activity to search for a string in an XML file.  

## Configure the Query XML Activity

 Before you configure the Query XML activity, you need to determine the following:  

- The XML file name or Block of XML that you want to search.  

- The query you'll use to perform the search.  

Use the following information to configure the Query XML activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**XML File**|Select either this option or the XML Text option. Enter the path or URL of the XML file that you want to search in, or select the ellipsis **(...)** and browse for it.|  
|**XML Text**|Select either this option or the XML File option. Enter the name of the element in the XML text that you want to search in.|  
|**XPath Query**|Enter the XPath query for your search.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Escaped Query Result|The result of the query.|  
|Escaped XML Attributes|The attributes found in the element tag of the query result.|  
|The input XML file|The name of the XML file that you're searching in. This item is blank if you used the Block of XML option.|  
|The input XML text|The XML text that you searched in. This item is blank if you used the XML File option.|  
|The XPath query.|The XPath query that was used in the search.|  
|Node count|The number of results published from the query.|
